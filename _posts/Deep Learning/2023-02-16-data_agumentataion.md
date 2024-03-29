---
layout: post
title: "데이터 증강(Data Augmentation)"
date: 2023-02-15 15:44:38 -0400
category: deep-learning
author: eun
short-description: CNN 모델의 성능을 높이고 오버피팅을 극복할 수 있는 가장 좋은 방법
toc: true
---

#### intro
---

[데이터 증강이 필요한 이유]

기술의 발달로 데이터의 접근이 쉬워졌지만 일부 데이터는 여전히 구하기 어렵다. 예를 들어 의료 분야의 데이터는 비용과 개인 정보 문제로 학습에 필요한 데이터를 충분히 모으기 힘들다. 

모델을 훈련시킬 때, 데이터가 적은 경우 다음과 같은 문제가 발생한다.

1. 모델의 과적합
- 모델은 복잡한데 그만큼 충분한 데이터가 제공되지 않으면 모델이 데이터를 암기해버리는 상황이 발생한다. 
- 이런 경우를 과적합이라고 부르는데, 과적합을 막는 근본적인 방법은 훈련 데이터를 늘리는 것이다.

2. 불균형 데이터
- 특정 클래스에 대한 훈련 데이터가 적을 때 발상하는 문제이다. 
- 예를 들어 고양이와 강아지 데이터를 사용해 고양이를 분류하는 모델을 만든다고 가정해보자. 이 때 고양이 데이터가 99개, 강아지 데이터가 1개라면 모든 데이터를 고양이로 분류하는 모델의 정확도가 99%가 되는 문제가 발상한다.


이러한 문제를 해결할 수 있는 기술이 **<u>'데이터 증강'</u>**이다.

<br>

#### Data argumentation
---

- CNN 모델의 성능을 높이고 오버피팅을 극복할 수 있는 가장 좋은 방법 -> 다양한 유형의 학습 이미지 데이터 양을 늘리는 것
- 하지만 이미지 데이터의 경우 학습 데이터량을 늘리는 것은 쉽지 않음
- **데이터 증강: 개별 원본 이미지를 변형해서 학습하는 것**(학습 이미지의 개수를 늘리는 것 X)
    + 데이터셋에서 크기와 편차를 프로그래밍 방식으로 늘리는 것

<p align = 'center'><img src="/assets/images/argumentation_01.PNG"  width="70%" height="70%"></p>

1. 이미지 데이터 증강
- 랜덤하게 이미지 자르기
- 회전
- 밝기 조절
- 불러 처리
- 노이즈 삽입

2. 텍스트 데이터 증강
- 특정 단어를 유의어로 교체
- 임의의 단어를 삽입 or 삭제
- 문장 내 두 단어의 위치를 임의로 바꾸기



<br>

