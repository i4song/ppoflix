---
date: 2021-03-14T20:48:05.000Z
layout: post
title: 1-3. SVD-Application
katex: True
subtitle: 'Advanced Mathematics for AI'
description: >-
  Advanced Mathematics for AI (Week 1)
image: >-
  https://velog.velcdn.com/images/dnr6054/post/18dec618-679e-401f-ae84-0363b8d6c558/image.png
optimized_image: >-
  https://velog.velcdn.com/images/dnr6054/post/18dec618-679e-401f-ae84-0363b8d6c558/image.png
category: math
tags:
  - SVD
  - 행렬분해
  - LatentSemanticIndexing
author: i4song
paginate: true
---
> 본 글은 K-MOOC의 [인공지능 수학 고급(Advanced Mathematics for AI)](http://www.kmooc.kr/courses/course-v1:SKKUk+SKKU_60+2023_T1/course/) 강의를 듣고 요약한 글입니다. 

## Question

[1-1. Data representation](https://velog.io/@dnr6054/1-1-Data-Representation) 에서 봤던 데이터를 다시 가져오자.

$d_1$: `Romeo` and `Juliet`
$d_2$: `Juliet` O `happy` `dagger`
$d_3$: `Romeo` `die`d by `dagger`
$d_4$: `Live` `free` or `die` that is the `New-Hampshire`'s motto
$d_5$: Did you know `New-Hampshire` is in New-England

자, 여기에서 `die`와 `dagger`에 관련된 문서를 찾으라는 문제가 나왔다면 어떻게 접근할 수 있을까?

$d_2$, $d_3$, $d_4$은 제목에 단어들이 있다. 아마 연관성이 있을 것이다.
$d_5$는 아무 단어도 없다. 그리고 연관성도 없다.
$d_1$은 아무 단어도 없다. 하지만..? 사실 로미오와 줄리엣은 `die`와 `dagger`와 연관이 있는 소설의 제목이다.

이러한 숨은 의미를 발견할 수 있을까?

## Solution: Latent Semantic Indexing

우리는 문서들에 숨은 의미를 찾아내야 한다. 

[1-1. Data representation](https://velog.io/@dnr6054/1-1-Data-Representation) 에서 만들었던 행렬을 다시 가져오자.

| |romeo|juliet|happy|dagger|live|die|free|New-Hampshire|
|-|-|-|-|-|-|-|-|-|
|$d_1$|1|1|0|0|0|0|0|0|
|$d_2$|0|1|1|1|0|0|0|0|
|$d_3$|1|0|0|1|0|1|0|0|
|$d_4$|0|0|0|0|1|1|1|1|
|$d_5$|0|0|0|0|0|0|0|1|

이 행렬을 분해하여 숨은 의미를 찾을 수 있지 않을까?

우리는 [1-2. Matrix Decomposition](https://velog.io/@dnr6054/1-2-Matrix-Decomposition) 에서 여러 분해 기법을 살펴보았고, 해당 행렬은 정사각행렬이 아니기 때문에 마지막으로 다룬 **SVD**가 가능해보인다.

> 잠깐 **SVD**에 대해서 짚고 넘어가자.
> 주어진 행렬 $A_{M\times N}$를 $A_{M\times N} = U_{M\times M}\Sigma_{M\times N}{V_{N\times N}}^T$ 로 분해하는 것을 `full SVD`라고 부른다. 
실제로 이와같이 `full SVD`를 하는 경우는 드물며 아래 그림들과 같이 `reduced SVD`를 하는게 일반적이다.
> - `thin SVD`
> ![](https://velog.velcdn.com/images/dnr6054/post/20fa02c2-6daf-4c9e-8817-e35b821ed649/image.png)
> - `compact SVD`
> ![](https://velog.velcdn.com/images/dnr6054/post/adeaa9ec-e59e-4c5f-bff2-8f59e883d0b4/image.png)
> - `truncated SVD`
> ![](https://velog.velcdn.com/images/dnr6054/post/84d9d3c9-76f2-4139-bd28-853fe984eed7/image.png)

여기서 우리는 데이터들간의 유사성을 판병해야 하고 2차원 평면 위에서 쉽게 표현하기 위해 다음과 같은 `reduced SVD`를 적용할 것이다.

$$
A_{5\times 8} = U_{5\times 2}\Sigma_{2\times 2}(V_{2\times 8})^T
$$

그 결과 아래와 같은 데이터들을 얻을 수 있다.

$$
\Sigma = \begin{bmatrix}
2.285 & 0 \\
0 & 2.010
\end{bmatrix}\\\,\\
U = \begin{bmatrix}
-0.311 & 0.363 \\
-0.407 & 0.547 \\
\vdots & \vdots \\
-0.143 & -0.229
\end{bmatrix} \larr \begin{matrix}
d_1 \\
d_2 \\
\vdots \\
d_5
\end{matrix} \\\,\\
V = \begin{bmatrix}
-0.396 & 0.280 \\
-0.314 & 0.450 \\
\vdots & \vdots \\
-0.326 & -0.460
\end{bmatrix} \larr \begin{matrix}
\rm{romeo} \\
\rm{juliet}\\
\vdots \\
\rm{new-hampshire}
\end{matrix}
$$

여기에서 본래의 가중치(특이값, Singular value)를 각각 $U$와 $V$에 곱해주면 각각의 문서, 단어들의 벡터를 구해줄 수 있다.
(Document vector: $U\Sigma$, Word vector: $\Sigma V^T$)

$$
d_1 = \begin{bmatrix}
-0.711\\
0.730
\end{bmatrix}, d_2 = \begin{bmatrix}
-0.930\\
1.087
\end{bmatrix}, d_3 = \begin{bmatrix}
-1.357\\
0.402
\end{bmatrix}, d_5 = \begin{bmatrix}
-0.327\\
0.460
\end{bmatrix}, \\\,\\
\rm{romeo} = \begin{bmatrix}
-0.905\\
0.563
\end{bmatrix},juliet = \begin{bmatrix}
-0.717\\
0.905
\end{bmatrix}, dagger = \begin{bmatrix}
-1.001\\
0.742
\end{bmatrix}, die = \begin{bmatrix}
-1.197\\
-0.494
\end{bmatrix}
$$

자 이제 쿼리의 벡터를 구해주기 위해 `die` 벡터와 `dagger` 벡터의 평균을 내주자.
$$
q=\begin{bmatrix}
-1.099\\
0.124
\end{bmatrix}
$$

마지막으로 문서들과 쿼리 벡터를 2차원 평면위에 나타내어 보자.

![](https://velog.velcdn.com/images/dnr6054/post/91cb3988-2fc3-4c89-9b28-aa8f6aeac74e/image.png)

그 결과 겉으로는 둘 다 아무 단어도 포함되어 있지 않은 $d_1$과 $d_5$였지만, 현재는 $d_1$이 더 좁은 각도를 나타내는 것을 볼 수 있다.

이런 식의 분석법을 **Latent Semantic Indexing**이라고 한다.