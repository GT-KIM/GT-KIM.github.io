---
title: "Unsupervised real-world super resolution with cycle generative adversarial network and domain discriminator"
categories:
 - ai
---

## 회상
이 논문은 2020년에 내가 1저자로 작성한 논문 중 처음으로 publish 된 논문이다. 현재 약 52회의 citation을 받아 내 연구 중 가장 많은 citation을 받은 논문이기도 하다. [NTIRE 2020 Challenge](https://data.vision.ee.ethz.ch/cvl/ntire20/)라는 CVPR Workshop 챌린지에 참가해서 5등을 했었고, 그 결과를 같은 학회에서 발표했다.  
당시 연구를 회상하면
- ICASSP에 제출한 음성 분야 논문 결과를 기다리면서 연구실 선배님들과 같이 시작했었다. 다른 분들은 Extreme Super resolution track을 했었고 나는 Real-world Super resolution track을 진행했다.
- Real-world Super resolution은 당시에는 새로운 task였다. task의 주요 특징은 noisy low resolution 이미지를 clean high resolution 이미지로 바꾸는 Denoising + Super-resolution task였고, paired dataset이 주어지지 않아서 cycleGAN 계열의 모델을 사용했었다.
- 상위권 입상이라는 명확한 목표가 있었고, 데이터가 주어졌기 때문에 상대적으로 연구가 편했다. 다만 quantitative measurement가 없었기 때문에 모델 성능 평가를 위해 직접 Super resolution 결과를 눈으로 보면서 주관적인 성능 평가만 진행했었다. 펭귄 사진만 수천 번은 봤던 것 같다.
- 본문을 굉장히 급하게 썼었다. 거의 일주일만에 논문 작성-검토-제출까지 진행했었다. 밤샘 및 지도교수님 두 분과의 무한 검토를 통해 겨우 제출했었다.
- 아쉽게도 COVID-19이 한창이었을 때라 virtual conference로 발표했다.

## 논문 요약
