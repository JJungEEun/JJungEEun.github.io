---
layout: post
title: "Data Visualization"
date: 2020-12-08 08:44:38 -0400
category: python
author: eun
short-description: 데이터 분석 결과를 시각적으로 정리하는 방법
---

#### intro
---
<mark>데이터 시각화</mark>는 데이터를 여러 유형의 차트, 그래프 등으로 표현하는 것을 의미한다. 즉, 데이터 분석 결과를 시각적으로 보기 쉽도록 정리하는 것이다. 열과 행, 글자와 숫자로만 이뤄진 데이터로만 알기 힘든 변화 추세나 관계성 등 또한 한 눈에 파악할 수 있다. 그리고 수치 안에 숨겨진 인사이트를 발견할 수 있다.

1. 범주형 데이터 
    - 명목형 데이터: 단순히 분류된 자료 ex) 성별 혈액형
    - 순서형 데이터: 이산적이면서 값 사이에 순서가 존재하는 자료
2. 수치형 데이터
    - 이산형 데이터: 이산적인 값을 찾는 자료 ex) 판애량
    - 연속형 데이터: 연속적인 값을 갖는 자료 ex) 키, 몸무게

파이썬을 이용해 데이터를 시각화할 수 있는 방법은 대표적으로 matplotlib, seaborn 등이 있다.

#### matplot
---
**matplotlib**은 파이썬에서 자료를 차트나 플롯으로 시각화하는 패키지이다.

- 설치
    ``` python
    pip3 install matplotlib
    ```
- 라이브러리 불러오기
    ``` python
    import matplotlib
    import matplotlib.pyplot as plt
    ```
- Figure의 구성 요소    
![Image Alt 텍스트](https://matplotlib.org/stable/_images/anatomy.png){: width="50%" height="50%"}   

---

<p style="font-size: 1.12em">📌막대 그래프(bar chart)</p>
- 각 범주의 데이터 값의 크기에 비례해 직사각형 막대로 표현한 그래프
- x 데이터가 카테고리 값인 경우 <mark>bar</mark> 명령과 <mark>barh</mark> 명령 사용
-  <mark>barh</mark>명령을 사용하면 가로 방향으로 바 차트를 그릴 수 있다

``` python
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(3)
x = 0.5 + np.arange(8)
y = np.random.uniform(2, 7, len(x))

fig, ax = plt.subplots()
ax.bar(x, y, width=1, edgecolor="white", linewidth=0.7)
plt.show()
```

![Image Alt 텍스트](https://matplotlib.org/stable/_images/sphx_glr_bar_001.png){: width="35%" height="35%"}   


[공식 홈페이지] <a href="https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.bar.html"> pyplot.bar / </a> <a href="https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.barh.html">pyplot.barh</a>

---

<p style="font-size: 1.12em">📌파이차트(pie chart)</p>
-범주형 구성 비율을 원형으로 표현한 그래프
- 카테고리 별 값의 상대적인 비교를 해야할 때 <mark>pie</mark> 명령 사용
- 파이 차트를 그릴 때 원의 형태를 유지할 수 있도록 <mark>plt.axis('equal')
</mark> 명령을 실행해야한다

```python
import matplotlib.pyplot as plt

labels = 'Frogs', 'Hogs', 'Dogs', 'Logs'
sizes = [15, 30, 45, 10]
explode = (0, 0.1, 0, 0) # 2nd slide만 추출

fig1, ax1 = plt.subplots()
ax1.pie(sizes, explode=explode, labels=labels, autopct='%1.1f%%', shadow=True, startangle=90)

plt.axis('equal')

```

![Image Alt 텍스트](https://matplotlib.org/stable/_images/sphx_glr_pie_features_001.png){: width="50%" height="50%"}   

[공식 홈페이지] <a href="https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.pie.html">pyplot.pie</a>

---

<p style="font-size: 1.12em">📌선 그래프(line plot)</p>
- 시간, 순서에 따른 추이 변화를 보기 좋은 그래프
- 연속형 데이터 유리
- <mark>plot</mark> 명령을 사용

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0, 10, 100)
y = 4 + 2 * np.sin(2 * x)

fig, ax = plt.subplots()
ax.plot(x, y, linewidth=2.0)

ax.set(xlim=(0, 8), xticks=np.arange(1, 8), ylim=(0, 8), yticks=np.arange(1, 8))

plt.show()
```

![Image Alt 텍스트](https://matplotlib.org/stable/_images/sphx_glr_plot_001.png){: width="35%" height="35%"}   

[공식 홈페이지] <a href="https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.html"> pyplot.plot</a>

---

<p style="font-size: 1.12em">📌히스토그램(histogram)</p>
- 도수분표표를 나타낸 그래프
- 연속형 데이터에 많이 사용
- <mark>hist</mark> 명령어 사용
- <mark>bins </mark> 인수로 데이터를 집계할 구간 정보를 받음

```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(1)
x = 4 + np.random.normal(0, 1.5, 200)

fig, ax = plt.subplots()
ax.hist(x, bins=8, linewidth=0.5, edgecolor="white")

ax.set(xlim=(0, 8), xticks=np.arange(1, 8), ylim=(0, 56), yticks=np.linspace(0, 56, 9))

plt.show()
```

![Image Alt 텍스트](https://matplotlib.org/stable/_images/sphx_glr_hist_plot_001.png){: width="35%" height="35%"}   

[공식 홈페이지] <a href="https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.hist.html">pyplot.hist</a>

---

<p style="font-size: 1.12em">📌박스 플롯(box plot)</p>
- 5개의 요약 통계랑(min, max, q1, q3, median) 제공
- 이상치 파악할 때 유리
- <mark>boxplot</mark> 명렁어 사용

![Image Alt 텍스트](https://miro.medium.com/max/1400/1*2c21SkzJMf3frPXPAR_gZA.png){: width="35%" height="35%"}   


```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(10)
data = np.random.normal(100, 20, 200)

fig, ax = plt.subplots()
VP = ax.boxplot(D, positions=[2, 4, 6], widths=1.5, patch_artist=True,
                showmeans=False, showfliers=False,
                medianprops={"color": "white", "linewidth": 0.5},
                boxprops={"facecolor": "C0", "edgecolor": "white",
                          "linewidth": 0.5},
                whiskerprops={"color": "C0", "linewidth": 1.5},
                capprops={"color": "C0", "linewidth": 1.5})

ax.set(xlim=(0, 8), xticks=np.arange(1, 8), ylim=(0, 8), yticks=np.arange(1, 8))

plt.show()
```

![Image Alt 텍스트](https://matplotlib.org/stable/_images/sphx_glr_boxplot_plot_001.png){: width="35%" height="35%"} 

[공식 홈페이지] <a href="https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.boxplot.html">pyplot.boxplot</a>

---

<p style="font-size: 1.12em">📌산점도(scatter)</p>
- 2차원 데이터(두 개의 실수 데이터 집합)의 상관관계를 살펴볼 때 사용
- 주로 서로 다른 연속형 변수의 관계
- 패턴 유무 파악에 사용
- <mark>scatter</mark> 명령 사용

```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(3)
x = 4 + np.random.normal(0, 2, 24)
y = 4 + np.random.normal(0, 2, len(x))

sizes = np.random.uniform(15, 80, len(x))
colors = np.random.uniform(15, 80, len(x))

fig, ax = plt.subplots()
ax.scatter(x, y, s=sizes, c=colors, vmin=0, vmax=100)

ax.set(xlim=(0, 8), xticks=np.arange(1, 8), ylim=(0, 8), yticks=np.arange(1, 8))

plt.show()
```

![Image Alt 텍스트](https://matplotlib.org/stable/_images/sphx_glr_scatter_plot_001.png){: width="35%" height="35%"} 

[공식 홈페이지] <a href="https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.scatter.html">pyplot.scatter</a>







#### seaborn
---

**Seaborn**은 Matplotlib을 기반으로 다양한 색상 테마와 통계용 차트 등의 기능을 추가한 시각화 패키지이다. 기본적인 시각화 기능은 Matplotlib 패키지에 의존하며 통계 기능은 Statsmodels 패키지에 의존한다. 

<p style="font-size: 1.12em">📌막대 그래프(bar chart)</p>
- 카테고리 값에 따른 실수 값에 평균과 편차를 표시하는 기본적인 바 차트
- 평균: 막대의 높이
- 편차: 에러바(error bar)
- 범주형 데이터에서 사용

```python
import seaborn as sns

tips = sns.load_dataset("tips")
sns.barplot(x="day", y="total_bill", data=tips)
plt.show()
```

![Image Alt 텍스트](http://seaborn.pydata.org/_images/seaborn-barplot-1.png
){: width="40%" height="40%"} 

[공식 홈페이지] <a href="http://seaborn.pydata.org/generated/seaborn.barplot.html">seaborn.barplot</a>


---

<p style="font-size: 1.12em">📌박스 플롯(box plot)</p>
- 박스와 박스 바깥의 선(whisker)로 이루어져있음
- 박스: 실수 값 분포에서 Q1(1사분위수)과 Q3(3사분위수)
- IQR: Q3-Q1
- 박스 바깥의 선: Q1보다 1.5XIQR 만큼 낮은 값, Q3보다 1.5XIQR 만큼 높은 값을 기준으로 그 구간의 내부에 있는 가장 큰 데이터와 작은 데이터를 잇는 선분
- 바깥의 점: 아웃라이어(outlier)

```python
import seaborn as sns

tips = sns.load_dataset("tips")
ax = sns.boxplot(x="day", y="total_bill", data=tips)
```

![Image Alt 텍스트](http://seaborn.pydata.org/_images/seaborn-boxplot-2.png){: width="40%" height="40%"} 

[공식 홈페이지] <a href="http://seaborn.pydata.org/generated/seaborn.boxplot.html">seaborn.boxplot</a>


---

<p style="font-size: 1.12em">📌바이올린 플롯(vionlin plot)</p>
- 각 범주에 따른 분포의 전체 형상을 직관적으로 보여줌
- 이상치 표기 X
- <mark>boxplot</mark>은 중앙값, 표준 편차 등, 분포의 간략한 특성만 보여줌
- <mark>violinplot</mark>은 카테고리값에 따른 각 분포의 실제 데이터나 전체 형상을 보여주는 장점이 있다

```python
import seaborn as sns

sns.set_theme(style="whitegrid")
ax = sns.violinplot(x="day", y="total_bill", data=tips)
```

![Image Alt 텍스트](http://seaborn.pydata.org/_images/seaborn-violinplot-2.png){: width="40%" height="40%"} 

[공식 홈페이지] <a href="http://seaborn.pydata.org/generated/seaborn.violinplot.html">seaborn.violinplot</a>


---

<p style="font-size: 1.12em">📌페어 플롯(pair plot)</p>
- 다차원 실수형 데이터(3차원 이상 데이터)
- 데이터프레임을 인수로 받아 Grid 형태로 각 데이터 열의 조합에 대해 산점도 생성
- 같은 데이터가 만나는 대각선 영역에는 해당 데이터의 히스토그램을 그린다

``` python
sns.pairplot(iris)
plt.show()
```

![Image Alt 텍스트](https://datascienceschool.net/_images/05.04%20%EC%8B%9C%EB%B3%B8%EC%9D%84%20%EC%82%AC%EC%9A%A9%ED%95%9C%20%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EB%B6%84%ED%8F%AC%20%EC%8B%9C%EA%B0%81%ED%99%94_27_0.png){: width="35%" height="35%"} 

만약 카테고리형 데이터가 섞여있는 경우 <mark>hue</mark> 인수에 카테고리 변수 이름을 지정하여 카테고리 값에 따라 색상을 다르게 할 수 있다.

``` python
sns.pairplot(iris, hue="species", markers=["o", "s", "D"])
plt.show()
```

![Image Alt 텍스트](https://datascienceschool.net/_images/05.04%20%EC%8B%9C%EB%B3%B8%EC%9D%84%20%EC%82%AC%EC%9A%A9%ED%95%9C%20%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EB%B6%84%ED%8F%AC%20%EC%8B%9C%EA%B0%81%ED%99%94_29_0.png){: width="35%" height="35%"} 

[공식 홈페이지] <a href="http://seaborn.pydata.org/generated/seaborn.pairplot.html">seaborn.pairplot</a>

---

<p style="font-size: 1.12em">📌히트맵(heatmap)</p>
- 2차원 데이터
- 색상에 따른 차이 직관적으로 표현

```python
import numpy as np
import seaborn as sns

uniform_data = np.random.rand(10, 12)
ax = sns.heatmap(uniform_data)
```

![Image Alt 텍스트](http://seaborn.pydata.org/_images/seaborn-heatmap-1.png){: width="35%" height="35%"} 

[공식 홈페이지] <a href="http://seaborn.pydata.org/generated/seaborn.heatmap.html">seaborn.heatmap</a>

---

#### 한글폰트 사용
1. 나눔고딕 폰트 설치
    - 윈도우/맥: http://hangeul.naver.com/2017/nanum 에서 폰트 인스톨러를 내려받아 실행한다.
    - 설치 확인

    ```python
    import matplotlib.font_manager

    matplotlib.font_manager._rebuild()
    sorted([f.name for f in matplotlib.font_manager.fontManager.ttflist if f.name.startswith("Nanum")])
    ```
2. rc parameter 설정
    ```python
    # 폰트 설정
    mpl.rc('font', family='NanumGothic')
    # 유니코드에서  음수 부호설정
    mpl.rc('axes', unicode_minus=False)

    ```
