---
title: "[Robot Laboratory 3]Fast Fourier Transform"
excerpt: "Let's Talk About Filter"

categories: 
    - Learn
tage: 
    - Robot Laboratory 3
    - Filter
    - Low Pass Filter
last_modified_at: 2021-07-10t01:31-15:00
comments: true
toc: true
toc_sticky: true
use_math: true
---

※ 본 포스팅에서는 푸리에 변환에 대한 수학적인 설명이 아닌, 디지털 필터를 분석하기 위한 "수단"으로서만 설명합니다. 



# 1. Fourier Transform(푸리에 변환)

푸리에 변환을 알아보기 전에, 푸리에 급수에 대해 얘기할 필요가 있다. 푸리에 급수의 일반적인 모습은 다음과 같이 쓸 수 있다.

---
<center>
$f(x) = \frac{A_0}{2} + \sum_{n = 1}^{\infty}(A_ncos\frac{n\pi}{L}x+B_nsin\frac{n\pi}{L}x) (x\in (-L, L))$
</center>
---

어떠한 함수를 sin과 cos의 급수합으로 표현을 할 수 있는 것인데, 이는 즉 모든 함수 그래프를 삼각함수 그래프의 합들로 표현이 가능하다는 것을 의미한다.  