---
date: 2023-03-19T14:05:18.000Z
layout: post
title: 1-5. NMF Application
katex: True
subtitle: 'Advanced Mathematics for AI'
description: >-
  Advanced Mathematics for AI (Week 1)
image: >-
  https://velog.velcdn.com/images/dnr6054/post/346d529c-4aba-49d6-a047-c44a2244d71e/image.png
optimized_image: >-
  https://velog.velcdn.com/images/dnr6054/post/346d529c-4aba-49d6-a047-c44a2244d71e/image.png
category: math
tags:
  - NMF
  - Topic Modeling
  - Clustering
author: i4song
paginate: true
---

> 본 글은 K-MOOC의 [인공지능 수학 고급(Advanced Mathematics for AI)](http://www.kmooc.kr/courses/course-v1:SKKUk+SKKU_60+2023_T1/course/) 강의를 듣고 요약한 글입니다. 

## Problem

- $$d_1$$: `Romeo` and `Juliet`
- $$d_2$$: `Juliet` O `happy` `dagger`
- $$d_3$$: `Romeo` `die`d by `dagger`
- $$d_4$$: `Live` `free` or `die` that is the `New-Hampshire`'s motto
- $$d_5$$: Did you know `New-Hampshire` is in New-England

NMF를 통해서 문서들 간의 숨어있는 의미를 찾아보자.

## Data Representaion

이전 [1-1. Data-Representation](https://velog.io/@dnr6054/1-1-Data-Representation)과 동일하게 행렬로 표현을 할테지만, 이번에는 문서-단어가 아닌 단어-문서 행렬($$A_{V\times D}$$)로 표현해보자.

| |$$d_1$$|$$d_2$$|$$d_3$$|$$d_4$$|$$d_5$$|
|-|-|-|-|-|-|
|romeo|1|0|1|0|0|
|juliet|1|1|0|0|0|
|happy|0|1|0|0|0|
|dagger|0|1|1|0|0|
|live|0|0|0|1|0|
|die|0|0|1|1|0|
|free|0|0|0|1|0|
|new-hampshire|0|0|0|1|1|

## Nonnegative Matrix Factorization

$$K=2$$로 설정하고 결과를 보면 다음과 같다.

$$
W_{8\times 2} = \begin{bmatrix}
0.083 & 0.668 \\
0.000 & 0.767 \\
\vdots & \vdots \\
1.285 & 0.000
\end{bmatrix} \larr \begin{matrix}
\rm{romeo} \\
\rm{juliet} \\
\vdots \\
\rm{new-hampshire}
\end{matrix}
$$

$$
(H_{2\times 5})^T = \begin{bmatrix}
0.000 & 0.747 \\
0.000 & 1.039 \\
0.182 & 0.892 \\
0.887 & 0.000 \\
0.259 & 0.000
\end{bmatrix} \larr \begin{matrix}
d_1 \\
d_2 \\
d_3 \\
d_4 \\
d_5
\end{matrix}
$$

### First cluster

- $$w_1 = [0.083, 0.000, \ldots, 1.285]^T$$
- $$h_1 = [0.000, 0.000, 0.182, 0.892, 0.259]$$

$$w_1$$에서 가장 숫자가 큰 세 단어는 **new-hampshire**, **die**, **live** 이며
$$h_1$$에서 해당 문서들은 $$d_4$$, $$d_5$$, $$d_3$$ 이다.

이는 $$d_4$$, $$d_5$$, $$d_3$$가 하나의 **클러스터**로 묶일 수 있고, 이를 대표하는 단어가 **new-hampshire**, **die**, **live** 라는 것이다.

### Second cluster

위와 같은 방법을 $$w_2$$와 $$h_2$$에 적용하면

$$d_2$$, $$d_3$$, $$d_1$$이 하나의 **클러스터**로 묶이며, 이를 대표하는 단어가 **dagger**, **juliet**, **romeo**라는 것을 알 수 있다.

이러한 방법을 통해 수많은 대용량 데이터를 쉽게 계산할 수 있으며, 
이런 기법을 **Topic Modeling**이라고 부른다.