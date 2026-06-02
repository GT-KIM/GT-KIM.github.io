---
title: "WER이 1.0을 넘을 때 — Transformer ASR의 반복 환각과 outlier 처리"
categories:
 - korean_asr
 - series
use_math: true
toc: true
toc_label: "목차"
toc_sticky: true
---

> ✍️ **작성 중 초안(draft)입니다.** `_drafts/`에 있어 라이브에는 발행되지 않습니다.
> `[확인 필요]`는 실제 outlier 샘플/수치로 채울 자리입니다.

[WER의 한계를 다룬 글](/korean_asr/series/wer-trap-korean-asr-metrics/)에서 WER은 0~1 사이의 비율처럼 느껴진다고 했다. 그런데 사실 WER에는 **상한이 없다.** 한 샘플의 WER이 **3.0, 5.0**도 나온다. 이번 글은 그 "괴물 샘플"의 정체 — **끝 단어 무한 반복(repetition hallucination)** — 와, OpenKoASR이 이걸 어떻게 잡아내는지를 다룬다.

## WER/CER은 1.0을 넘을 수 있다

오류율 공식을 다시 보자.

$$
\text{ErrorRate} = \frac{S + D + I}{N}
$$

분자에는 **삽입(I)**이 있다. 정답에 없는 토큰을 모델이 만들어내면 삽입이 쌓인다. 삽입에는 한계가 없으므로, 모델이 정답 길이 $N$보다 훨씬 많은 토큰을 뱉으면 **오류율은 1.0을 가뿐히 넘는다.** 정답이 10글자인데 같은 단어를 200번 반복하면 CER은 20.0이 될 수도 있다.

## 끝 단어가 무한 반복되는 현상

대표적인 실패 패턴은 이렇다.

[확인 필요] 실제 outlier 예시 인용 (results/.../predictions에서):
- 정답: `"네 그러면 회의는 내일 오후에 하겠습니다"`
- 예측: `"네 그러면 회의는 내일 오후에 하겠습니다 하겠습니다 하겠습니다 하겠습니다 ..."` (끝 어절이 수십~수백 회 반복)

문장 끝의 단어/구가 종료되지 못하고 루프에 빠진다. 사람이 보면 "앞부분은 멀쩡한데 뒤가 고장난" 결과다. 이 한 샘플이 평균 지표를 통째로 오염시킨다.

## 왜 Transformer + CE 기반 모델에서 생기나

이 현상은 모델 구조와 직접 연결된다.

- **자기회귀(Autoregressive) 디코딩 + Cross-Entropy:** Whisper, Qwen3-ASR 같은 seq2seq Transformer는 자기 출력을 다음 입력으로 먹으며 토큰을 하나씩 생성한다. 한 번 반복 모드에 들어가면 **자기 출력에 자기가 갇혀** 빠져나오지 못한다(exposure bias). 종료 토큰(EOS)을 못 찍으면 길이 한계까지 반복한다.
- **입력-출력 정렬 제약이 없다:** 디코더는 오디오 프레임 수와 출력 토큰 수를 직접 묶지 않는다. 그래서 오디오가 끝나도 토큰을 계속 만들 수 있다.

반면 **CTC / RNN-T는 구조적으로 이런 무한 반복이 어렵다.**

[확인 필요] 정확도 보강 — CTC는 프레임 단위로 출력하고 blank로 정렬하며, RNN-T도 입력 프레임에 대해 단조(monotonic) 정렬을 유지한다. 출력 길이가 입력 프레임에 묶여 있어, AR 디코더 같은 자유 생성 루프가 잘 발생하지 않는다.

| 구조 | 정렬 | 반복 환각 위험 |
| :-- | :-- | :-- |
| Transformer seq2seq (CE, AR) | 없음(attention) | **높음** — 끝 단어 무한 반복 |
| CTC | 단조, 프레임 동기 | 낮음 |
| RNN-T | 단조, 프레임 동기 | 낮음 |

즉 **WER ≥ 1.0 outlier는 우연한 노이즈가 아니라, 특정 모델 계열의 구조적 실패 모드**다.

## 평가에서 왜 문제인가, 그리고 OpenKoASR의 대응

outlier 한 샘플(WER 5.0)이 끼면 1000개 평균이 통째로 흔들린다. 모델의 *전형적* 성능을 가리는 것이다. OpenKoASR은 이를 두 가지로 처리한다.

1. **outlier 판정·제외:** `OutlierPolicy(metric="cer", threshold=1.0)` — CER이 1.0을 넘는 샘플을 평균에서 제외한다. (`--outlier_metric`, `--outlier_threshold`로 조정 가능)
2. **투명한 공개:** 제외하고 끝내지 않고, 리더보드 **`Outliers` 컬럼에 `제외 수 / 전체 수`**(예: `6 / 3000`)를 같이 표기한다.

[확인 필요] 리더보드에서 outlier 비율이 눈에 띄는 행 인용 — 모델/데이터셋별 outlier 발생률 비교 (예: tiny/base가 큰 모델보다 반복 환각이 잦은지).

## 제외가 정답일까 — 트레이드오프

여기엔 평가 철학이 걸린다.

- **제외하면:** 모델의 전형적 인식 품질을 더 정확히 본다. 하지만 "이 모델은 가끔 통째로 망가진다"는 **신뢰성 정보**를 평균에서 숨기게 된다.
- **그래서 둘 다 본다:** outlier를 평균에서 빼되 **발생률을 별도 지표로 공개**한다. 정확도(평균)와 안정성(outlier율)은 다른 질문이고, 배포 관점에선 후자가 더 치명적일 수 있다.

## 정리

- WER/CER은 삽입 때문에 **1.0을 넘을 수 있고**, 그 주범은 **끝 단어 무한 반복**이다.
- 이는 **AR Transformer + CE** 모델의 구조적 실패 모드로, **CTC/RNN-T엔 잘 없다.**
- OpenKoASR은 outlier를 **평균에서 제외하되 발생률을 투명하게 공개**해, 정확도와 안정성을 분리해서 본다.

---

- 전체 결과·재현 방법: [OpenKoASR 리더보드](https://gt-kim.github.io/open-korean-automatic-speech-recognition/) · [GitHub](https://github.com/GT-KIM/open-korean-automatic-speech-recognition)
