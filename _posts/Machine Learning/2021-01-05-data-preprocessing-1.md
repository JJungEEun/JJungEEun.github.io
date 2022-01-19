---
layout: post
title: "Data Preprocessing - Numeric Data"
date: 2019-11-05 08:44:38 -0400
category: machine-learning 
author: eun
short-description: 좋은 머신 러닝 모델을 구축하기 위해 필요한 데이터 전처리 과정
toc: true
---
<br>
<hr>

### 데이터 전처리
[데이터 전처리 필요성]

![Image Alt 텍스트](/assets/images/ml01_01.png){: width="500" height="300"}

데이터 분석에 있어 데이터 전처리는 꼭 필요한 과정이다. 데이터 전처리는 분석 결과/인사이트와 모델 성능에 가장 직접적인 영향을 미치는 과정이기 때문이다. 그리고 데이터 품질과 데이터에 담긴 유용한 정보의 양은 머신 러닝 알고리즘을 얼마나 잘 학습할 수 있는 지를 결정한다. 한 설문조사에 의하면 데이터 분석가의 80% 시간을 데이터 수집 및 전처리에 사용한다고 한다. 이 만큼 중요한 과정이다. 

[전처리 전 데이터 파악하기]

<hr>

### 결측치 처리
결측치 처리는 주로 1) 결측치 값 제거 2) 결측치 대체 두 가지 방법이 사용된다.

1) 결측치 값 제거

![Image Alt 텍스트](/assets/images/ml01_02.png){: width="500" height="300"}

데이터셋에서 해당 훈련 샘플(행)이나 특성(열)을 완전히 제거하는 것이다. 결측치 처리에서 방법 중 가장 간단하지만 이는 큰 단점도 가지고 있다. 너무 많은 결측치가 있는 경우 이를 모두 제거하면 안정된 분석이 불가능해진다. 또는 너무 많은 특성 열을 제거하면 분류기가 클래스를 잘 구분하는 데 필요한 중요한 정보를 잃을 수도 있다.

```bash 
DataFrame.dropna(axis=0, how='any', thresh=None, subset=None, inplace=False)
```

2) 결측치 대체(보간 기법)

결측치 값 제거가 힘든 경우 보간 기법을 사용한다. 여러 가지 보간 기법을 사용하여 데이터셋에 있는 다룬 훈련 샘플로부터 누락된 값을 추정할 수 있다.
<ul>
    <li>mean</li>
    <li>median</li>
    <li>mode</li>
</ul>

```bash 
SimpleImputer(missing_values=nan, strategy='mean', fill_value=None, verbose=0, copy=True, add_indicator=False)
DataFrame.fillna(value=None, method=None, axis=None, inplace=False, limit=None, downcast=None)
```

결측치를 처리할  때 도메인 지식은 유용한 지표이다. 인적, 기계적 원인임이 판명되면, 협업자와 지속적으로 노력해 결측치를 사전에 발생하지 않도록 만드는 것이 좋다. 수치형인 경우 의미상 0으로 메꾸는 것이 맞는지 평균이나 중앙치가 맞는지 등 데이터에 대한 배경지식이 있을 때 더 적절한 의사결정을 할 수 있다.

<hr>

### 이상치 처리
이상치는 다른 데이터보다 아주 작은 값이나 아주 큰 값을 말한다. 데이터를 분석할 때 이상치 유무에 따라 결과가 다르게 나올 수 있다. 하지만 이상치라고 해서 항상 의미없는 값이라고 할 수 없기 때문에 그 데이터에 대한 지식을 가지고 있는 전문가와 함께 검토하는 것이 좋다.

일반적으로 01) 표준 점수 변환후 +-3 제거 02) IQR 방식 03) 도메인 지식 이용하거나 Binning 처리 하는 3가지 방식이 사용된다.

1. 표준 점수 변환 후 +-3 제거

![Image Alt 텍스트](/assets/images/ml01_03.png){: width="500" height="300"}

표준점수를 이용할 경우 평균이 0, 표준 편차가 1인 분포로 변환한 후 +- 3인 극단치를 제거한다.

2. IQR 방식

![Image Alt 텍스트](/assets/images/ml01_04.png){: width="500" height="300"}

IQR 방식은 Q1-1.5XIQR이하 거나 Q3+1.5XIQR이상인 경우 극단치로 처리하는 방식이다. 경우에 따라 많은 데이터들이 극단치로 처리될 수 있다. 

3. 도메인 지식 이용하거나 Binning 처리

<hr>

### 불균형 데이터 처리

<hr>

### 특성 스케일 맞추기
결정트리와 랜덤 포레스트는 특성 스케일 조정에 대해 걱정할 필요가 없는 알고리즘이다. 하지만 대부분의 머신러닝과 최적화 알고리즘은 특성의 스케일이 같을 때 훨씬 성능이 좋다. 

![Image Alt 텍스트](/assets/images/ml01_05.png){: width="500" height="300"}

예를 들어 두 개의 특성에서 첫 번째 특성이 1-10 사이의 스케일을 가지고 있고 두 번째 특성이 1-100000 사이의 스케일을 가진다고 하면 더 큰 스케일을 가진 특성이 결과값을 좌지우지 할 확률이 높다. 그렇기 때문에 특성의 스케일을 맞추는 과정이 필요한 것이다.
1) 정규화(Normalization)

![Image Alt 텍스트](/assets/images/ml01_06.png){: width="500" height="300"}


정규화는 모든 데이터가 동일한 정도의 스케일로 반영되도록 해주는 것이다. 

<li>Min-Max Normalization(최소-최대 정규화)</li>
최소-최대 정규화는 모든 특성의 스케일이 [0, 1] 범위에 맞추는 것이다. 하지만 최소-최대 정규화는  이상치에 많은 영향을 받는다.

![Image Alt 텍스트](/assets/images/ml01_07.png)
```bash
from sklearn.preprocessing import MinMaxScaler
mms = MinMaxScaler()
X_train_norm = mms.fit_transform(X_train)
X_test_norm = mms.transform(X_test)
```

2) 표준화(StandardScaler)

표준화는 많은 머신러닝 알고리즘, 특히 경사 하강법과 같은 최적화 알고리즘에서 널리 사용된다. 표준화를 사용하면 특성의 평균을 0에 맞추고 표준 편차를 1로 만들어 정규 분포와 같은 특징을 가지도록 만든다. 이는 가중치를 쉽게 학습 할 수 있게 만든다. 또한 표준화는 이상치 정보가 유지되기 때문에 제한된 범위로 데이터를 조정하는 최소-최대 스케일 변환에 비해 알고리즘이 이상치에 덜 민감하다.

![Image Alt 텍스트](/assets/images/ml01_08.png)
```bash
from sklearn.preprocessing import StandardScaler
stdsc = StandardScaler()
X_train_std = stdsc.fit_transform(X_train)
X_test_std = stdsc.transform(X_test) 
```


3) RobustScaler

RobustScaler는 이상치가 많이 포함된 작은 데이터셋을 다룰 때 도움이 된다. 데이터셋이 과대적합이 되기 쉬울 때 사용하는 것이 좋다. 특성 열마다 독립적으로 작용하며 중간값을 뺀 다음 데이터셋의 1사분위수와 3사분위수(25%와 75%)를 사용하여 데이터셋의 스케일을 조정한다. 그렇기 때문에 극단적인 값과 이상치의 영향을 덜 받는다.

![Image Alt 텍스트](/assets/images/ml01_09.png)
```bash
from sklearn.preprocessing import RobustScaler
rbs = RobustScaler()
X_train_robust = rbs.fit_transform(X_train)
X_test_robust = rbs.transform(X_test) 
```
