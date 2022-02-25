---
layout: post
title: "Data Visualization"
date: 2020-12-08 08:44:38 -0400
category: python
author: eun
short-description: 데이터 분석 결과를 시각적으로 정리하는 방법
---

#### intro
<mark>시각화</mark>란 데이터 분석 결과를 시각적으로 보기 쉽도록 정리하는 것이다. 데이터 시각화를 통해 수치 안에 숨겨진 인사이트를 발견할 수 있다.

1. 범주형 데이터 
    - 명목형 데이터: 단순히 분류된 자료 ex) 성별 혈액형
    - 순서형 데이터: 이산적이면서 값 사이에 순서가 존재하는 자료
2. 수치형 데이터
    - 이산형 데이터: 이산적인 값을 찾는 자료 ex) 판애량
    - 연속형 데이터: 연속적인 값을 갖는 자료 ex) 키, 몸무게

파이썬을 이용해 데이터를 시각화할 수 있는 방법은 대표적으로 matplotlib, seaborn 등이 있다.

#### matplot
**matplotlib**은 파이썬에서 자료를 차트나 플롯으로 시각화하는 패키지이다.

- 설치
    ```
    pip3 install matplotlib
    ```
- 라이브러리 불러오기
    ```
    import matplotlib
     import matplotlib.pyplot as plt
    ```
- Figure의 구성 요소    
![Image Alt 텍스트](https://matplotlib.org/stable/_images/anatomy.png){: width="50%" height="50%"}   

<p style="font-size: 1.12em">📌막대 그래프(bar chart)</p>
x 데이터가 카테고리 값인 경우 <mark>bar</mark> 명령과 <mark>barh</mark> 명령으로 바 차트를 이용해 시각화 할 수 있다.
 <mark>barh</mark>명령을 사용하면 가로 방향으로 바 차트를 그릴 수 있다

[matplotlib 공식 홈페이지] <a href="http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.bar"> pyplot.bar / </a> <a href="http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.barh">pyplot.barh</a>

<p style="font-size: 1.12em">📌파이차트(pie chart)</p>
<p style="font-size: 1.12em">📌선 그래프(line plot)</p>
<p style="font-size: 1.12em">📌히스토그램(histogram)</p>
<p style="font-size: 1.12em">📌박스 플롯(box plot)</p>
<p style="font-size: 1.12em">📌산점도(scatter)</p>

#### seqborn
<p style="font-size: 1.12em">📌막대 그래프(bar chart)</p>
<p style="font-size: 1.12em">📌박스 플롯(box plot)</p>
<p style="font-size: 1.12em">📌바이올린 플롯(vionlin plot)</p>
<p style="font-size: 1.12em">📌페어 플롯(pair plot)</p>
<p style="font-size: 1.12em">📌히트맵(heatmap)</p>
