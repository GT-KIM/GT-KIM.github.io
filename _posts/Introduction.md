---
title: "Curriculum Vitae"
categories:
 - introduction
---
## Work Experience
- Staff Engineer, Samsung Electronics, Mobile eXperience(MX) Division, AP R&D Team (2024.09 ~ Current, 9 months)
    - Projects
 
- Postdoctoral Researcher, Korea University (2024.03 ~ 2024.08, 6 months)

- Dispatched Researcher, Brand Engagement Network (2023.11 ~ 2024.07, 8 months)

## Publications
- 



내가 1저자로 2020년에 NTIRE Challenge에 참여했고, CVPR Workshop에서 발표했던 논문이다.

## 링크
[Github](https://github.com/GT-KIM/unsupervised-super-resolution-domain-discriminator) [Paper](https://openaccess.thecvf.com/content_CVPRW_2020/papers/w31/Kim_Unsupervised_Real-World_Super_Resolution_With_Cycle_Generative_Adversarial_Network_and_CVPRW_2020_paper.pdf)

## 요약
### Real-world super resolution
Real-world super resolution은 "실제 저해상도 영상은 대부분 깨끗하지 않고, 노이즈가 있는 저해상도 영상에 super resolution을 적용하면 노이즈가 살아 있거나, 더 심해지는 현상이 발생한다." 라는 문제와 "실제 영상에는 Gaussian noise 뿐만 아니라 다양한 Unknown noise가 존재한다."라는 문제를 해결하기 위해 제안된 task이다. 이 문제들을 해결하기 위해 denoising과 super resolution을 동시에 적용하면서, unknown noise에 대한 unpaired dataset을 사용하여 unsupervised learning으로 학습하는 모델을 연구했다.

### Model structure
전체 모델 구조는 아래와 같다.
![model](/assets/images/AI_review/20240213/model.png)
input image, generator, discriminator, loss를 하나의 그림에 올리려고 해서 그림이 다소 복잡한데, [참고 논문:Cycle-in-cycle GAN](https://openaccess.thecvf.com/content_cvpr_2018_workshops/papers/w13/Yuan_Unsupervised_Image_Super-Resolution_CVPR_2018_paper.pdf)과 기본적인 구조는 동일하고 Real-world Super resolution 성능을 향상시키기 위해 여러 가지를 추가한 논문이 되겠다.  
x는 unknown noise가 섞인 저해상도 이미지이고, z는 clean 고해상도 이미지이다. 


## 회상
이 논문은 2020년에 내가 1저자로 작성한 논문 중 처음으로 publish 된 논문이다. 현재 약 52회의 citation을 받아 내 연구 중 가장 많은 citation을 받은 논문이기도 하다. [NTIRE 2020 Challenge](https://data.vision.ee.ethz.ch/cvl/ntire20/)라는 CVPR Workshop 챌린지에 참가해서 5등을 했었고, 그 결과를 같은 학회에서 발표했다.  
당시 연구를 회상하면
- ICASSP에 제출한 음성 분야 논문 결과를 기다리면서 연구실 선배님들과 같이 시작했었다. 다른 분들은 Extreme Super resolution track을 했었고 나는 Real-world Super resolution track을 진행했다.
- Real-world Super resolution은 당시에는 새로운 task였다. task의 주요 특징은 noisy low resolution 이미지를 clean high resolution 이미지로 바꾸는 Denoising + Super-resolution task였고, paired dataset이 주어지지 않아서 cycleGAN 계열의 모델을 사용했었다.
- 상위권 입상이라는 명확한 목표가 있었고, 데이터가 주어졌기 때문에 상대적으로 연구가 편했다. 다만 quantitative measurement가 없었기 때문에 모델 성능 평가를 위해 직접 Super resolution 결과를 눈으로 보면서 주관적인 성능 평가만 진행했었다. 펭귄 사진만 수천 번은 봤던 것 같다.
- 본문을 굉장히 급하게 썼었다. 거의 일주일만에 논문 작성-검토-제출까지 진행했었다. 밤샘 및 지도교수님 두 분과의 무한 검토를 통해 겨우 제출했었다.
- 아쉽게도 COVID-19이 한창이었을 때라 virtual conference로 발표했다.

## 논문 요약
