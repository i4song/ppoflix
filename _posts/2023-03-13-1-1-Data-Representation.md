---
date: 2023-03-13T23:48:05.000Z
layout: post
title: 1-1. Data Representation
katex: True
subtitle: 'Advanced Mathematics for AI'
description: >-
  Advanced Mathematics for AI (Week 1)
image: >-
  https://velog.velcdn.com/images/dnr6054/post/9325aa03-264f-4961-89b7-1b07ab79c9a5/image.png
optimized_image: >-
  https://velog.velcdn.com/images/dnr6054/post/9325aa03-264f-4961-89b7-1b07ab79c9a5/image.png
category: math
tags:
  - 데이터표현법
  - 행렬표현
author: i4song
paginate: true
---
> 본 글은 K-MOOC의 [인공지능 수학 고급(Advanced Mathematics for AI)](http://www.kmooc.kr/courses/course-v1:SKKUk+SKKU_60+2023_T1/course/) 강의를 듣고 요약한 글입니다. 

## Question
> 다음과 같은 **문서**가 있다. 이를 어떻게 우리가 쓰기 쉽게 **표현**할 수 있을까?

$d_1$: `Romeo` and `Juliet`
$d_2$: `Juliet` O `happy` `dagger`
$d_3$: `Romeo` `die`d by `dagger`
$d_4$: `Live` `free` or `die` that is the `New-Hampshire`'s motto
$d_5$: Did you know `New-Hampshire` is in New-England

## Answer

답은 다음과 같은 **행렬**을 만드는 것이다.
`행`: 문서
`열`: 단어
$A_{ij}$: $j$번째 단어가 $i$번째 문서에 등장한 **횟수**

| |romeo|juliet|happy|dagger|live|die|free|New-Hampshire|
|-|-|-|-|-|-|-|-|-|
|$d_1$|1|1|0|0|0|0|0|0|
|$d_2$|0|1|1|1|0|0|0|0|
|$d_3$|1|0|0|1|0|1|0|0|
|$d_4$|0|0|0|0|1|1|1|1|
|$d_5$|0|0|0|0|0|0|0|1|

앞으로 우리는 이러한 **데이터**들을 다룰 것이다.

데이터는 행렬(**matrix**) 또는 다차원 배열(**multidimensional array**)로 표현될 것이며 그 말인즉슨 **tensor**의 형태로 나타나게 될 것이라는 것이다.