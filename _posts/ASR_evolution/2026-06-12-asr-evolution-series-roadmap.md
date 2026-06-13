---
lang: ko
title: "ASR의 진화 시리즈를 시작하며 — 고전 음성인식에서 Speech LLM, 그리고 On-device까지"
categories:
 - asr_evolution
toc: true
toc_label: "목차"
toc_sticky: true
---

## 왜 이 시리즈를 쓰는가

[OpenKoASR](https://gt-kim.github.io/open-korean-automatic-speech-recognition/) 리더보드를 운영하면서 수많은 ASR 모델을 같은 잣대로 평가해 왔다. Whisper 같은 대규모 모델부터 Qwen3-ASR 같은 LLM 기반 모델까지 돌려보면, 숫자 너머로 한 가지 질문이 계속 떠오른다.

**"음성인식 기술은 어디에서 와서, 지금 어디에 있고, 어디로 가는가?"**

개별 모델의 성능 비교는 리더보드가 답해준다. 하지만 CTC가 왜 등장했는지, Attention이 무엇을 해결하고 무엇을 못 풀었는지, 왜 갑자기 모두가 LLM에 음성을 꽂기 시작했는지, 그리고 그 거대한 모델들이 왜 결국 손바닥 위의 기기로 돌아오려 하는지 — 이 **큰 흐름**은 어디에도 한 번에 정리되어 있지 않다. 논문은 파편적이고, 튜토리얼은 특정 시점의 스냅샷이다.

그래서 이 시리즈를 쓴다. 고전 ASR부터 Speech LLM, On-device ASR까지를 하나의 이야기로 엮는 장기 연재이고, 완결되면 책 한 권 분량이 되도록 설계했다.

> 본격적인 기술사에 들어가기 전에, "멀티모달 LLM 시대에 음성 인식이 왜 여전히 필요한가"를 먼저 짚는 프롤로그를 따로 두었다 — [멀티모달 LLM 시대에 음성 인식은 왜 필요한가](/asr_evolution/why-asr-in-multimodal-llm-era/).

## 이 시리즈가 답하려는 세 가지 질문

이 시리즈는 세 개의 Part로 구성되며, 각 Part는 하나의 질문에 답한다.

1. **ASR은 어떻게 발전해왔는가?** — 고전 GMM-HMM에서 CTC, LAS, RNN-T를 거쳐 최신 End-to-End 모델까지, 각 기술이 무엇을 해결했고 무엇을 남겼는지.
2. **Speech LLM은 만능인가?** — Audio/Speech Encoder와 LLM의 결합이 열어준 가능성, 그리고 모델 사이즈와 Cloud 비용이라는 현실적인 벽.
3. **왜 다시 On-device인가?** — 거대 모델 시대에 역설적으로 중요해진 on-device ASR의 현재, 한계, 그리고 나아가야 할 방향.

## Part I — ASR의 발전사: 고전에서 End-to-End까지

딥러닝 이전의 음성인식은 음향모델, 발음사전, 언어모델을 정교하게 조립한 거대한 파이프라인이었다. End-to-End 모델은 이 파이프라인을 신경망 하나로 대체했지만, 그 과정은 단번에 이루어지지 않았다. 정렬(alignment) 문제를 어떻게 풀 것인가를 두고 CTC, Attention, Transducer라는 서로 다른 답이 경쟁했고, 각각의 선택이 오늘날 모델들의 구조에 그대로 새겨져 있다.

예정된 글:

1. **[고전 ASR의 해부](/asr_evolution/classic-asr-anatomy/)** — GMM-HMM, 음향모델·발음사전·언어모델, WFST 디코딩
2. **DNN-HMM 하이브리드 시대** — 딥러닝이 음향모델을 대체하다
3. **CTC** — 정렬 없는 학습의 시작, 그리고 조건부 독립 가정의 한계
4. **LAS와 Attention Seq2Seq** — 강력하지만 스트리밍이 안 되는 모델
5. **RNN-T** — 스트리밍 End-to-End의 표준이 되기까지
6. **최신 ASR** — Conformer, self-supervised learning(wav2vec 2.0, HuBERT), Whisper류 대규모 학습
7. **(정리) End-to-End ASR의 남은 숙제** — 도메인 적응, 희귀 어휘, 환각, 긴 오디오

## Part II — Speech LLM: 멀티모달의 시대

ASR의 남은 숙제 중 상당수는 "언어를 더 깊이 이해해야" 풀리는 문제다. LLM의 등장은 자연스러운 질문으로 이어졌다 — 음성 인코더를 LLM에 연결하면 되지 않을까? SALMONN, Qwen-Audio 계열을 비롯한 Speech LLM들은 실제로 인상적인 능력을 보여줬다. 하지만 모델 사이즈를 키우는 것이 정답일까? GPU 비용과 지연시간, 그리고 환각이라는 청구서가 함께 날아온다.

예정된 글:

1. **Audio/Speech Encoder의 세계** — Whisper encoder부터 음향 표현학습까지
2. **Speech를 LLM에 꽂는 법** — adapter/projector 구조와 학습 전략
3. **Speech LLM이 ASR을 넘어서는 지점** — 문맥 이해, 바이어싱, 다국어
4. **모델 사이즈만 키우면 되나?** — 스케일링의 수확체감과 환각 문제
5. **Cloud 서빙의 경제학** — RTFx, 동시성, GPU 비용으로 보는 현실
6. **(정리) Speech LLM의 구조적 한계**

## Part III — On-device ASR: 현재와 미래

Cloud의 비용과 지연, 프라이버시 문제는 결국 한 방향을 가리킨다 — 모델이 기기 위로 내려와야 한다. 하지만 on-device는 단순히 "모델을 작게 만드는" 문제가 아니다. 메모리와 전력의 물리적 한계, 한국어 같은 언어별 격차, 개인화라는 난제가 기다리고 있다. 이 Part는 [기존에 다뤘던 on-device 한국어 ASR 측정](/korean_asr/series/rtfx-ondevice-korean-asr/)의 문제의식을 이어받아, on-device ASR이 나아가야 할 방향을 그린다.

예정된 글:

1. **왜 On-device인가** — 프라이버시, 지연시간, 비용, 오프라인
2. **작게 만드는 기술** — distillation, quantization, pruning, 스트리밍 아키텍처
3. **현장의 On-device ASR** — whisper.cpp, 모바일 NPU, 빅테크 사례
4. **On-device의 벽** — 메모리·전력, 언어별 격차, 개인화
5. **미래 방향** — cloud-edge 하이브리드, on-device LLM과의 결합

## 연재 방식

- 각 글은 독립적으로 읽을 수 있게 쓰되, 순서대로 읽으면 하나의 이야기가 되도록 연결한다.
- Part I 1장부터 순서대로 연재하며, 새 글이 올라오면 이 로드맵에 링크를 건다.
- 목차는 연재하면서 다듬어질 수 있다. 다루면 좋겠다 싶은 주제가 있다면 댓글로 남겨주시면 반영을 검토한다.
- 모든 글은 [ASR의 진화 시리즈](/asr_evolution/) 페이지에 모인다.

## 누구를 위한 시리즈인가

- ASR을 처음 공부하는데 논문들 사이의 **맥락**이 궁금한 분
- Whisper나 Speech LLM을 쓰고는 있지만 그 설계가 **왜 그런 모양인지** 알고 싶은 분
- On-device 음성인식 제품을 고민하는 엔지니어와 기획자

수식은 필요한 만큼만 쓰고, 모든 개념은 "이것이 어떤 문제를 풀기 위해 등장했는가"라는 관점에서 설명할 것이다. 첫 글, 고전 ASR의 해부에서 만나자.
