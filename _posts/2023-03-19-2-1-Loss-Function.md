---
date: 2023-03-19T14:27:14.000Z
layout: post
title: 2-1. Loss Function
katex: True
subtitle: 'Advanced Mathematics for AI'
description: >-
  Advanced Mathematics for AI (Week 2)
image: >-
  https://velog.velcdn.com/images/dnr6054/post/4fd2cc2c-e1f6-43f2-b33b-d3479718c2a7/image.png
optimized_image: >-
  https://velog.velcdn.com/images/dnr6054/post/4fd2cc2c-e1f6-43f2-b33b-d3479718c2a7/image.png
category: math
tags:
  - Loss Function
  - Linear Regression
author: i4song
paginate: true
---

> 본 글은 K-MOOC의 [인공지능 수학 고급(Advanced Mathematics for AI)](http://www.kmooc.kr/courses/course-v1:SKKUk+SKKU_60+2023_T1/course/) 강의를 듣고 요약한 글입니다. 

## Problem

광고 예산에 따른 TV의 판매량을 다음과 같은 그래프로 나타내었다. 

![](https://velog.velcdn.com/images/dnr6054/post/33a29cdd-05ef-4a79-bf02-78fa2de93328/image.png)

이 때, 새로운 광고 예산에 대한 TV의 판매량을 예측하는 문제이다.

## Data

다음과 같이 변수를 정의하자.

- $$X$$: TV 광고 예산 (input variable, features)
- $$Y$$: 판매량 (output variable, response variable)
- $$(x^{(i)}, y^{(i)})$$: $$i$$번째 학습 데이터

이를 통해 우리는 이 그래프를 행렬로 표현할 수 있다.

|$$X$$|$$Y$$|
|-|-|
|230.1|22.1|
|44.5|10.4|
|17.2|9.3|
|151.5|18.5|
|$$\vdots$$|$$\vdots$$|

## Linear Regression

우리는 이를 위해 선형회귀분석을 사용할 것이다.

모델을 다음과 같이 정의하자. $$Y \approx \beta_0 + \beta_1X$$

![](https://velog.velcdn.com/images/dnr6054/post/ed777064-0ef4-48ee-b29e-11f55069f9ee/image.png)

이 때 우리는 최적의 $$\beta_0, \beta_1$$을 찾는 문제로 문제를 변형할 수 있다.

즉, 같은 $$x^{(i)}$$에 대해서, $$\hat{y}^{(i)}$$ 와 $$y^{(i)}$$ 의 차이가 최소가 되는 $$\beta_0, \beta_1$$를 찾으면 된다.

![](https://velog.velcdn.com/images/dnr6054/post/9088a527-a3df-4363-a269-64fc5a0145ec/image.png)

Euclidean distance를 이용하여 차이를 계산한다고 가정할 때, 모든 차이를 다음과 같이 계산할 수 있을 것이다.

$$
\sum^N_i(y^{(i)}-\hat{y}^{(i)})^2 = \sum^N_i(y^{(i)}-(\beta_0 + \beta_1x^{(i)}))^2
$$

이 함수를 바로 Loss function이라고 정의한다. 

$$
L(\beta_0, \beta_1)= \sum^N_i(y^{(i)}-(\beta_0 + \beta_1x^{(i)}))^2
$$

그럼 문제가 다음과 같이 바뀐다. 

$$
\argmin_{\beta_0, \beta_1}\sum^N_i(y^{(i)}-(\beta_0 + \beta_1x^{(i)}))^2
$$

이를 최적화하는 알고리즘에 대해서는 다음 강의에서 다룬다.