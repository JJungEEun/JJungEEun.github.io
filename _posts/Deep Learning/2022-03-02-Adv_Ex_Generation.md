---
layout: post
title: "[Paper] Adversarial Patch(NIPS'17)"
date: 2022-06-05 08:44:38 -0400
category: deep-learning
author: eun
short-description: 생성적 적대 신경망 아키텍처를 사용한 화풍모사, Pix2Pix
toc: true
use_math: true

---

#### intro
---

- 인공지능 모델에 물리적 위협을 가하는 **`Physical Adversarial Attack'**분야의  새로운 공격 방법
- 어떤 이미지든지 뭍이기만 하면 오작동을 발생시키는 patch 생성
- **to create universal, robust, targeted adversarial image patches**
    + universal: 어떤 이미지든지
    + robust: 이미지가 변형 or 조작되든지 상관없이
    + targeted: 특정한 target에 
    + 공격 가능한 패치를 생성한다.


<br>

#### 1. Introduction
---
딥러닝 모델은 `Adversarial Examples`에 취약하다. Adversarial Examples은 입력값에 사람이 인지하지 못할 정도의 조작을 가해 뉴럴네트워크의 예측를 빗나가게 하는 샘플을 의미한다.

다양한 공격 방법으로 L-BFGS, Fast Gradient Sign Method (FGSM), DeepFool, Projected Gradient Descent (PGD) 등이 있다.        
Adversarial Examples은 현실 세계에서도 존재한다. 

[기존 연구]
- Kurakin은 AE기법을 사용해 생성한 이미지를 프린트를 해도 공격이 가능하다는 것을 증명함. 심지어 조명과 방향이 달라도 가능
- Athalye은 3d 프린터로 출력한 Adversarial Examples는 방향, 스케일이 다른 경우에도 잘 작동함
- 특정한 안경을 착용하면 다른 사람으로 오분류함
- 위 연구에서의  Adversarial Examples는 일반적인 이미지에 거의 미미한 노이즈를 더해 공격함

[본 연구]
- 대부분의  Adversarial Examples 기존 연구는, 입력 이미지에 대한 변화가 아주 작거나 인지 불가능함
- 하지만 **본 논문은  Adversarial Examples의 pertubation limit을 제한하지 않을 때 발생하는 일에 대해 다룸**
- 알아채지 못할 정도의 이미지가 아닌 **입력 이미지와 무관한 효과적인 패치 생성**

<p align="center"><img src="/assets/images/AdvPatch_01.PNG"  width="60%" height="60%"></p>

- 97%의 바나나로 인식하던 것이 패치를 붙인 후 99%의 토스트로 인식하는 것을 확인할 수 있음

[장점]
- 어떤 이미지에 붙일지 고려하지 않아도 됨
    + 기존 공격 기법은 하나의 이미지를 최대한 조금 변형해 오작동을 일으키는 데 집중
    + 본 공격 기법은 하나의 패치를 만들어 어떤 이미지든지 붙여도 작동하도록 설계
- 하나의 패치를 만들어 다양하게 사용 가능! 

<br>


<!-- #### 2. Approach
---

<p align="center"><img src="/assets/images/AdvPatch_02.PNG"  width="60%" height="60%"></p>

전통적인 Adversarial Examples 공격 방법은 
<!-- `maximum perturbation` $ε$ 범위 내에서, 원본값과 조작값 차이를 $||x − x||∞ ≤ ε$ -->


<p align="center"><img src="/assets/images/AdvPatch_03.PNG"  width="60%" height="60%"></p>

- 본 논문은 이미지의 일부분의 조작을 patch로 대신하는 방법으로 공격한다.
- 이 패치는 어떤 모양이어도 가능하고, 여러 이미지에 대해서 transformations(such as scale and rotations)을 통해 학습한다
- gradient descent 방법으로 최적화 되었다.
- 너비 w, 높이 h, 채널 c(rgb인 경우 3채널)인 


본 논문에서는 변형된 패치를 얻기 위한 목적함수는 다음과 같다.

<p align="center"><img src="/assets/images/AdvPatch_04.PNG"  width="60%" height="60%"></p>

<br> -->



#### 3. Experimental Results
---

이 공격을 테스트하기 위해 1개의 control patch에 대해 2개의 화이트박스 공격, 1개의 블랙박스 공격을 비교했다.

<p align="center"><img src="/assets/images/AdvPatch_05.PNG"  width="60%" height="60%"></p>

<p align="center"><img src="/assets/images/AdvPatch_06.PNG"  width="60%" height="60%"></p>

<br>

#### 4. Conclusion
---

본 논문에서 universal, robust, targeted한 패치를 만들어냈고, 다른 아이템과 관계 없이 뉴럴 네트워크를 잘 속일 수 있음을 보여줬다. 프린트하여 현실 세계에서도 사용할 수 있다.

작은 perturbation에 대한 방어기법들은 많이 연구되어 왔지만, 본 논문과 같이 large perturbation 공격은 연구된 바가 많지 않다. 

<br>

---
<p style="font-size: 1.0em">References</p>

<a href = "https://pytorch.org/tutorials/beginner/fgsm_tutorial.html" style="font-size: 0.8em"> ADVERSARIAL EXAMPLE GENERATION </a>      
