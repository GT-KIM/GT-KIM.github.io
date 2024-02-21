---
title: "AI Tech category test page"
categories:
 - ai_tech
---

## reference
> [Github](https://github.com/microsoft/DeepSpeed)  
> [참고 블로그(한글)](https://velog.io/@seoyeon96/%EB%A6%AC%EC%84%9C%EC%B9%98-%ED%9A%A8%EC%9C%A8%EC%A0%81%EC%9D%B8-%EB%B6%84%EC%82%B0-%ED%95%99%EC%8A%B5%EC%9D%84-%EC%9C%84%ED%95%9C-DeepSpeed-ZeRO)
## Why deepspeed?

Deepspeed의 장점은 간단하게  
1. multi-GPU training 환경을 구축하기 비교적 쉽다.
2. 적은 VRAM으로 더 큰 모델을 학습/추론할 수 있다.

## How to use?
[Huggingface Deepspeed](https://huggingface.co/docs/transformers/main_classes/deepspeed) 문서를 보면 Trainer class를 사용하는 경우 대부분의 setup에서 deepspeed를 별도의 세팅 없이 사용할 수 있다고 한다. Trainer를 사용하는 경우