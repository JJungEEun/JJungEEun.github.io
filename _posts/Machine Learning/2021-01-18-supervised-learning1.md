---
layout: post
title: "Supervised Learning: Linear Regression, Logistic Regression"
date: 2019-11-05 08:44:38 -0400
category: machine-learning
author: eun
short-description: 이진분류 알고리즘(퍼셉트론, 아달린, 로지스틱 회귀)
toc: true
---

### 이진분류
**이진분류**는 임의의 샘플 데이터를 True인지 False인지 구분하는 문제를 말한다. 예를 들면 특정 종양 샘플이 주어졌을 때 양성(True)인지 음성(False)인지를 판단하는 것이다. 

이진분류 알고리즘은 `퍼셉트론 -> 아달린 -> 로지스틱 회귀` 순으로 발전한다.
위 순서로 이준분류 알고리즘을 알아보도록 하자.

### 퍼셉트론(Perceptron)
**퍼셉트론**은 MCP 뉴런 모델을 기반으로 한 알고리즘이다. 특정 샘플의 최종 입력이 사전에 정의된 임계값 보다 크면 클래스 1로 예측하고, 그렇지 않으면 클래스 -1로 예측한다. 퍼셉트론 알고리즘에서 결정함수는 **단위 계단 함수**를 변형한 것이다. 

 $\phi(z)=\begin{cases}1&z\ge\theta\mbox{ 일 때} \\ -1&\mbox{그 외}\end{cases}$
$\;\;\;\;\;$