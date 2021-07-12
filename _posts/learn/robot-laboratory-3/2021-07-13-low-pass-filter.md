---
title: "[Robot Laboratory 3] Low Pass Filter"
excerpt: "Let's Talk About LPF"
header: 
    teaser: 

categories: 
    - Robot Laboratory 3
tage: 
    - Robot Laboratory 3
    - Filter
    - Low Pass Filter
last_modified_at: 2021-07-13t01:31-15:00
comments: true
toc: true
toc_sticky: true
use_math: true
---

<br/><br/><br/><br/>

# 1. Low Pass Filter(LPF)
"저주파 통과 필터"라고도 하며, 특정 차단 주파수 이상의 주파수 신호를 감쇄시켜 차단 주파수 이하의 신호만 통과시키는 필터이다.  
LPF도 마찬가지지만, 필터를 설계할 때에는 "차단 주파수(Cutoff Frequency)"가 중요한데, 이를 기준으로 그 위나 아래의 주파수를 차단하는 것으로 필터링을 하기 때문이다. LPF의 경우, 물리적인 LPF인 1차 RC회로에서 차단 주파수와 이에 따른 필터의 시간 응답을 구할 수 있다.  

<br/><br/><br/>

# 2. RC Circuit Filter
아래와 같은 1차 RC 회로를 키르히호프 법칙으로 시정수를 구한다.

<center>
<img src="\assets\images\learn\robot-laboratory-3\2021-07-13-robot-laboratory-3\img1.png" width="70%" height="70%">
</center>

<br>
키르히호프 법칙으로 미분방정식을 세워 회로를 해석하면 다음과 같다.  
<center>$R_t(t)+v_a(t) = v_i(t)$</center>
<center>$$RC\frac{dv_0(t)}{dt}+v_0(t)=v_i(t)$$</center>

