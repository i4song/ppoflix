---
date: 2021-03-14T14:48:05.000Z
layout: post
title: 1-2. Matrix Decomposition
katex: True
subtitle: 'Advanced Mathematics for AI'
description: >-
  Advanced Mathematics for AI (Week 1)
image: >-
  https://velog.velcdn.com/images/dnr6054/post/49ce63dd-d720-47fe-a69b-5ae49528c5cc/image.png
optimized_image: >-
  https://velog.velcdn.com/images/dnr6054/post/49ce63dd-d720-47fe-a69b-5ae49528c5cc/image.png
category: math
tags:
  - 행렬분해
  - Eigenvalue
  - Eigenvector
  - SVD
author: i4song
paginate: true
---
> 본 글은 K-MOOC의 [인공지능 수학 고급(Advanced Mathematics for AI)](http://www.kmooc.kr/courses/course-v1:SKKUk+SKKU_60+2023_T1/course/) 강의를 듣고 요약한 글입니다. 

## Eigenvalues, Eigenvectors

정사각행렬 $$A_{N\times N}$$ 의 `Eigenvalue`는 다음 방정식의 해들이다. ($$I$$는 항등 행렬이다.)

$$
|A-\lambda I|  = 0
$$

$$\lambda$$를 $$A$$의 `eigenvalue`일때, 다음을 만족하는 벡터 $$x$$가 존재한다면 

$$
Ax = \lambda x
$$

$$x$$는 $$\lambda$$에 대한 $$A$$의 `Eigenvector`이다. 

### Eigenvalue, Eigenvector의 특성

이때 다음 명제들은 동치이다.
- $$\lambda$$ 는 $$A$$의 eigenvalue이다.
- $$\lambda$$ 는 특성방정식 $$\det(A-\lambda I) = 0$$ 의 해이다.
- 선형방정식 $$(A-\lambda I)x = 0$$ 은 nontrivial한 해가 존재한다.

## Eigen Decomposition  

$$A$$가 대각화가능 행렬일 때, $$A$$는 다음 식처럼 분해할 수 있다.

$$
A = PDP^{-1}
$$

여기서 $$D$$는 각 주대각선 위의 성분이 $$A$$의 eigenvalue인 대각행렬이다.
이때, $$P$$는 각 $$\lambda_1, \cdots \lambda_N$$에 대한 eigenvector들의 행렬이다.

## QR Decomposition

정사각행렬 $$A_{N\times N}$$은 다음과 같이 분해가능하다. ($$Q$$는 직교행렬이며 $$R$$은 상삼각행렬이다.)

$$
A = QR
$$

우리는 이를 통해서 $$\min\|Ax - b\|$$ 를 쉽게 구할 수 있다.

$$
\min||Ax-b||\Leftrightarrow A^TAx = A^Tb\; \\
\phantom{(R^TQ^T)QRx=(R^TQ^T)b}\Leftrightarrow (R^TQ^T)QRx=(R^TQ^T)b \\
\phantom{R^TRx=R^TQ^Tb}\Leftrightarrow R^TRx=R^TQ^Tb \\
\phantom{Rx=Q^Tb}\Leftrightarrow Rx=Q^Tb \\
\phantom{x=R^{-1}Q^Tb}\Leftrightarrow x=R^{-1}Q^Tb \\
$$

### QR분해 예시

다음 행렬을 QR분해 해보자.

$$
A = \begin{bmatrix}
   1 & 1 & 0 \\
   1 & 0 & 1 \\
   0 & 1 & 1
\end{bmatrix} \rightarrow a_1 = \begin{bmatrix}
   1 \\
   1 \\
   0
\end{bmatrix} , a_2 = \begin{bmatrix}
   1 \\
   0 \\
   1
\end{bmatrix} , a_3 = \begin{bmatrix}
   0 \\
   1 \\
   1
\end{bmatrix}
$$

Gram-Schmidt 과정을 통해 직교기저들을 만들자.

$$
u_1 = a_1 = \begin{bmatrix}
   1 \\
   1 \\
   0
\end{bmatrix} \\\,\\
u_2 = a_2 - proj_{u_1}a_2 = \begin{bmatrix}
   1 \\
   0 \\
   1
\end{bmatrix} - \left( \frac{u_1\cdot a_2}{u_1 \cdot u_1}\right)u_1 \\\,\\
\phantom{.,,.,.,.,.,.,...,.,.,.,.,.,.,}= \begin{bmatrix}
   1 \\
   0 \\
   1
\end{bmatrix} - \frac{1}{2}\begin{bmatrix}
   1 \\
   1 \\
   0
\end{bmatrix} = \begin{bmatrix}
   1/2 \\
   -1/2 \\
   1
\end{bmatrix}
\\\,\\
u_3 = a_3 - proj_{u_1}a_3 - proj_{u_2}a_3 = \begin{bmatrix}
   0 \\
   1 \\
   1
\end{bmatrix} - \left( \frac{u_1\cdot a_3}{u_1 \cdot u_1}\right)u_1 - \left( \frac{u_2\cdot a_3}{u_2 \cdot u_2}\right)u_2
\\\,\\
\phantom{.,.,.,.,..,....................................}= \begin{bmatrix}
   0 \\
   1 \\
   1
\end{bmatrix} - \frac{1}{2}\begin{bmatrix}
   1 \\
   1 \\
   0
\end{bmatrix} - \frac{1}{3}\begin{bmatrix}
   1/2 \\
   -1/2 \\
   1
\end{bmatrix} = \begin{bmatrix}
   -2/3 \\
   2/3 \\
   2/3
\end{bmatrix}
$$

각 벡터들을 정규화하면 $$Q$$는 다음과 같다. 

$$
Q = \begin{bmatrix}
1/\sqrt{2} & 1/\sqrt{6} & -1/\sqrt{3} \\
1/\sqrt{2} & -1/\sqrt{6} & 1/\sqrt{3} \\
0 & 2/\sqrt{6} & 1/\sqrt{3}
\end{bmatrix}
$$

그리고 $$R$$도 직교행렬의 성질을 통해 바로 구해줄 수 있다.

$$
R = Q^TA = \begin{bmatrix}
2/\sqrt{2} & 1/\sqrt{2} & 1/\sqrt{2} \\
0 & 3/\sqrt{6} & 1/\sqrt{6} \\
0 & 0 & 2/\sqrt{3}
\end{bmatrix}
$$

따라서 결과는 다음과 갔다.

$$
A = QR =  \begin{bmatrix}
1/\sqrt{2} & 1/\sqrt{6} & -1/\sqrt{3} \\
1/\sqrt{2} & -1/\sqrt{6} & 1/\sqrt{3} \\
0 & 2/\sqrt{6} & 1/\sqrt{3}
\end{bmatrix} \begin{bmatrix}
2/\sqrt{2} & 1/\sqrt{2} & 1/\sqrt{2} \\
0 & 3/\sqrt{6} & 1/\sqrt{6} \\
0 & 0 & 2/\sqrt{3}
\end{bmatrix}
$$

## Singular Value Decomposition

> 일반적으로는 복소수 공간에서 **SVD**를 정의하지만, 여기서는 실수 공간에 대해서만 언급합니다.

$$A_{M\times N}$$이 $$M\times N$$ 실수 행렬일 때, 다음을 만족하는 직교행렬 $$U_{M\times M}$$, $$V_{N\times N}$$,$$\Sigma_{M\times N}$$ 이 존재한다.

$$
A = U\Sigma V^T
$$

여기서 $$\Sigma$$의 대각성분은 양수이며 단조감소한다. ($$\Sigma_{00}$$부터 시작한다.)

> 다음 강의에서 **SVD**의 활용에 대해 좀 더 자세히 다루고, 간단한 **SVD** 예시 하나만 남긴다.

### SVD 예시

다음 행렬을 SVD 해보자.

$$
A = \begin{bmatrix}
   1 & -1 \\
   -2 & 2 \\
   2 & -2
\end{bmatrix}
$$

이때 $$\Sigma$$의 대각성분은 $$A^TA$$의 eigenvalue들의 양의 제곱근들이다. 

$$
A^TA = \begin{bmatrix}
   9 & -9 \\
   -9 & 1
\end{bmatrix} \\\,\\
\lambda_1 = 18 \Rarr v_1= \begin{bmatrix}
   1/\sqrt{2} \\
   -1/\sqrt{2}
\end{bmatrix}, \sigma_1 = \sqrt{18} \\\,\\
\lambda_2 = 0 \Rarr v_2= \begin{bmatrix}
   1/\sqrt{2} \\
   1/\sqrt{2}
\end{bmatrix}, \sigma_2 = 0 \\\,\\
\Rarr V = \begin{bmatrix}
   v_1 & v_2
\end{bmatrix} = \begin{bmatrix}
   1/\sqrt{2} & 1/\sqrt{2} \\
   -1/\sqrt{2} & 1/\sqrt{2}
\end{bmatrix}, \Sigma = \begin{bmatrix}
   \sqrt{18} & 0 \\
   0 & 0 \\
   0 & 0
\end{bmatrix} \\\,\\
$$

이제 주어진 데이터들로 $$U$$의 처음 몇 열을 알 수 있다.

$$
Av_1 = \begin{bmatrix}
   2/\sqrt{2} \\
   -4/\sqrt{2}\\
   4/\sqrt{2}
\end{bmatrix} \Rarr u_1 = Av_1 / \sigma _1 =  \begin{bmatrix}
   1/3 \\
   -2/3 \\
   2/3
\end{bmatrix}
$$

나머지는 아무 두 직교하는 벡터만 넣으면 되므로 $$u_1^Tx=0$$을 만족하는 두 벡터를 잡자.

$$
w_1=\begin{bmatrix}
   2 \\
   1 \\
   0
\end{bmatrix}, w_2=\begin{bmatrix}
   -2 \\
   0 \\
   1
\end{bmatrix}
$$

이후 Gram-Schmidt 과정을 통해 서로 직교하도록 만들면 $$U$$의 나머지 열을 만들 수 있다.

$$
u_2 = \begin{bmatrix}
   2/\sqrt{5} \\
   1/\sqrt{5} \\
   0
\end{bmatrix}, u_3 = \begin{bmatrix}
   -2/\sqrt{45} \\
   4/\sqrt{45} \\
   5/\sqrt{45}
\end{bmatrix} \\\,\\
$$

최종적으로 다음 분해가 완성된다.

$$
A = U\Sigma V^T = \begin{bmatrix}
   1/3 & 2/\sqrt{5} & -2/\sqrt{45} \\
   -2/3 & 1/\sqrt{5} & 4/\sqrt{45} \\
   2/3 & 0 & 5/\sqrt{45}
\end{bmatrix} \begin{bmatrix}
   \sqrt{18} & 0 \\
   0 & 0 \\
   0 & 0
\end{bmatrix} \begin{bmatrix}
   1/\sqrt{2} & -1/\sqrt{2} \\
   1/\sqrt{2} & 1/\sqrt{2}
\end{bmatrix}
$$