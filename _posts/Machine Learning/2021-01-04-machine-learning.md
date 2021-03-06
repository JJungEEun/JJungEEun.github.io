---
layout: post
title: "Machine Learning"
date: 2019-11-05 08:44:38 -0400
category: machine-learning
author: eun
short-description: 머신러닝의 일반적인 개념과 지도학습, 비지도 학습, 강화학습 알아보기
toc: true
---
### 머신러닝
<b>[머신러닝이란]</b>

머신러닝은 수집된 데이터로부터 모델을 만드는 것이다. 

사람이 수동으로 대량의 데이터를 분석하여 규칙을 유도하고 모델은 만드는 대신, <br>
<u>머신러닝이 데이터에서 더 효율적으로 지식을 추출하여 예측 모델과 데이터 기반의 의사 결정</u>
하는 것이다.

<b>[머신러닝의 기본 용어]</b> Dataset 관련
<br>
![Image Alt 텍스트](/assets/images/ml00_01.png){: width="500" height="300"}
<ul>
  <li>훈련 샘플: 데이터셋을 나타내는 테이블 행</li>
  <li>특성(x): 데이터 테이블의 열(속성, 측정값, 차원)</li>
  <li>타깃(y): 모델이 맞춰야 할 정답</li>
</ul>

<hr>

### 머신러닝의 3가지 종류
![Image Alt 텍스트](/assets/images/ml00_02.png){: width="500" height="300"}
<ul>
  <li>지도 학습</li>
  <li>비지도 학습</li>
  <li>강화 학습</li>
</ul>

<hr>

#### 1) 지도 학습 

![Image Alt 텍스트](/assets/images/ml00_03.png){: width="500" height="400"}

<mark>지도학습</mark>은 레이블된 훈련 데이터에서 모델을 학습하여 본 적 없는 미래 데이터에 대해 예측을 만드는 것이다. 즉, 정답이 주어진 상태에서 학습하는 알고리즘이다. 위 그림처럼 레이블된 훈련 데이터가
머신러닝 알고리즘에 전달되어 예측 모델을 훈련하고 새로운 레이블 되지 않은 데이터 입력에 대해
예측을 한다.

![Image Alt 텍스트](/assets/images/ml00_04.png){: width="500" height="300"}

예를 들어 수많은 하얀 강아지와 검정 강아지의 사진과 정답을 알려준 다음,
어떤 사진을 주었을 때 머신러닝 알고리즘이 검정 강아지인지 하얀 강아지인지
알아 맞힐 수 있도록 하는 것이다.

1) 분류: 클래스 레이블 예측
![Image Alt 텍스트](/assets/images/ml00_05.png){: width="500" height="300"}

<mark>분류</mark>는 과거의 관측을 기반으로 새로운 샘플의 범주형 클래스 레이블을 예측하는 것이다.
위 그림은 30개의 훈련 샘플이 있는 이진 분류 작업의 개념을 보여준다. 15개의 샘플은 음성 클래스(뺄셈 부호),
다른 15개의 샘플은 양성 클래스(덧셈 부호)이다. 지도 학습 알고리즘을 사용하여 이런 두 클래스를 구분할 수 있도록 학습한다.
이 규칙은 그림 속 점선을 의미하며, 이를 결정 경계라고 부른다.

분류는 이진 분류와 다중분류로 나눌 수 있다.
<ul>
  <li>이진 분류: 클래스 레이블이 두 개 일 때 ex) 스팸 메일: 2개의 범주 클래스</li>
  <li>다중 분류: 클래스 레이블이 두 개 이상일 때 ex) 손글씨: 순서가 없는 범주나 클래스 레이블</li>
</ul>

2) 회귀: 연속적인 출력 값 예측
![Image Alt 텍스트](/assets/images/ml00_06.png){: width="500" height="300"}

`회귀`는 연속적인 출력 값을 예측하는 것이다. 예측 변수(특성)와 연속적인 반응 변수(타깃)가 주어졌을 때
출력 값을 예측하기 위해 두 변수 사이의 관계를 찾는다. 

예를 들어 학생들의 기말고사 시험 점수를 예측한다고 하자. 시험 공부에 투자한 시간과 성적 사이의 관계가 있다면 두 값을 훈련 데이터로 만들고
모델을 학습할 수 있다. 이 모델은 시험에 응시하려는 학생들의 공부한 시간을 이용해 시험 점수를 예측한다. 이 때 공부한 시간은 특성 x, 성적은 타깃 y가 된다.
위 그림은 선형 회귀의 개념을 보여준다. 특성 x와 타깃 y가 주어지면 데이터 포인트와 직선 사이 거리가 최소가 되는 직선을 긋는다. 이렇게 데이터에서 학습한
직선의 기울기와 절편을 사용하여 새로운 데이터의 출력값을 예측하는 것이다.

<hr>

#### 2) 강화 학습 
![Image Alt 텍스트](/assets/images/ml00_07.png){: width="500" height="300"}

<mark>강화 학습</mark>은 환경과 상호 작용하여 시스템(에이전트) 성능을 향상하는 것이다. 환경의 현재 상태 정보는 
보상 신호를 포함하기 때문에 강화 학습을 지도 학습과 관련된 분야로 생각할 수 있다. 강화 학습의 피드백은
보상 함수로 얼마나 행동이 좋은지를 측정한 값이다. 에이전트는 환경과 상호 작용하여 보상이 최대화되는 
행동을 강화학습으로 학습한다.


<hr>

#### 3) 비지도 학습 
`비지도 학습`은 레이블 되지 않거나 구조를 알 수 없는 데이터를 다룬다. 

1) 군집: 서브그룹 찾기

![Image Alt 텍스트](/assets/images/ml00_08.png){: width="500" height="300"}

<mark>군집</mark>은 사전 정보 없이 쌓여 있는 그룹의 정보를 의미있는 서브 그룹 또는 클러스터로 조직하는
탐색적 데이터 분석 기법이다. 분석 과정에서 만든 각 클러스터는 어느 정도의 유사성을 공유하고 다른 클러스터와 
비슷하지 않은 샘플을 그룹을 형성한다. 위 그림처럼 레이블 되지 않은 데이터를 특성들의 유사도를 기반으로 3개의 
개별적인 그룹으로 조직화한다. 

2) 차원 축소: 데이터 압축
![Image Alt 텍스트](/assets/images/ml00_09.png){: width="500" height="300"}

<mark>차원 축소</mark>는 고차원의 데이터를 다룰 떄관련 있는 정보를 대부분 유지하며 더 작은 차원을 가진 부분 공간으로 데이터를 압축한다. 
머신 러닝 알고리즘의 계산 성능과 저장 공간의 한계를 해결해주는 역할을 한다. 

<hr>

### 머신러닝 분석 절차
![Image Alt 텍스트](/assets/images/ml00_10.png){: width="600" height="350"}

머신러닝은 전처리, 학습, 평가, 예측 순으로 이루어진다. 