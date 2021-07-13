---
title: "[Robot Laboratory 3] 2. Low Pass Filter"
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

## 2-1. Time Constant and Cutoff Frequency
아래와 같은 1차 RC 회로를 키르히호프 법칙으로 해석해본다.

<center>
<img src="\assets\images\learn\robot-laboratory-3\2021-07-13-robot-laboratory-3\img1.PNG" width="70%" height="70%">
</center>

<br>

키르히호프 법칙으로 미분방정식을 세워 해석하면 다음과 같다.  

* $V=IR$ 이므로 → $v_{in}(t)-v_{out}(t)=Ri(t)$  
* 축전기의 전압과 전기용량의 관계($Q=CV$)에 의해 → $Q_c(t)=Cv_{out}(t)$  
* 전류의 정의에 의해 → $i(t)=\frac{dQ_c}{dt}$  

따라서, 
<center>$$v_{out}(t)=v_{in}(t)-RC\frac{dv_{out}(t)}{dt}$$</center>  

이를 라플라스 변환을 하게 되면,  
<center>$$L[v_{out}]=L[v_{in}]-RCL[\dot{v}_{out}]$$</center>  
<center>$$→ V_{out}=V_{in}-RC(sV_{out}-v_0)$$</center>  
<center>$$→ (RCs+1)V_{out}=V_{in}+RCv_0$$</center>  
<center>$$→ V_{out}=\frac{V_{in}+RCv_0}{RCs+1}$$</center>  

그런데 여기서 $V_{in}$을 크기가 $V_{in}$인 step function으로 생각을 해 보자. 그러면 $L[v_{in}]=\frac{V_{in}}{s}$가 되므로,
<center>$$V_{out}=\frac{\frac{V_{in}}{s}+RCv_0}{RCs+1}$$</center>  
<center>$$V_{out}=\frac{(aRC+b)s+a}{(RCs+1)s}$$</center> 

부분분수로 계산을 하면,
<center>$$\frac{a}{s}+\frac{b}{RCs+1}$$</center>  
<center>$$=\frac{aRCs+a+bs}{(RCs+1)s}=\frac{(aRC+b)s+a}{(RCs+1)s}$$</center>  
<center>$$(aRC+b)s+a=V_{in}+RCv_0s$$</center>  
<center>$$a=V_{in}, b=RC(v_0-V_{in})$$</center>  
<center>$$\therefore V_{out}=\frac{V_{in}}{s}+\frac{RC(v_0-V_{in})}{s+1/RC}$$</center>  

<br/>

$v_{out}$을 구하기 위해 라플라스 역변환을 하면,
<center>$$L^{-1}[V_{out}]=L^{-1}[\frac{V_{in}}{s}]+L^{-1}[\frac{v_0-V_{in}}{s+\frac{1}{RC}}]$$</center>  
<center>$$v_{out}=V_{in}+v_0e^{-\frac{1}{RC}t}-V_{in}e^{-\frac{1}{RC}t}$$</center>

<br/>

이를 정리하면,
<center>$$v_{out}=V_{in}(1-e^{-\frac{1}{RC}t})+v_0e^{-\frac{1}{RC}t}$$</center>  

<br/>

이때, 시정수는 $RC$가 되며, 차단 주파수는 $\frac{1}{RC}$가 됨을 알 수 있다.  
엥? $\frac{1}{2\pi RC}$아닌가? 맞다. 축전기의 용량 리액턴스를 고려하기 전이므로, 이를 한 번 따져보자.  

축전기의 용량 리액턴스 $X_C$는 다음과 같이 정의가 된다.  

<center>$$X_c=\frac{1}{2\pi fC}$$</center>

<br/>

그런데 이 용량 리액턴스가 저항값과 같게 되는 때의 주파수가 바로 차단 주파수가 된다.  

<center>$$R = \frac{1}{2\pi fC}$$</center>
<center>$$f=\frac{1}{2\pi RC}$$</center>

<center>$$\therefore f_c=\frac{1}{2\pi RC}$$</center>  

<br/>

<center>$$\therefore f_c=\frac{1}{2\pi RC}, RC=\frac{1}{2\pi f_c}$$</center>


<!--
<br/>
이때 시정수는 $RC=\tau$, 차단주파수는 $f_c=\frac{1}{2\pi RC}$이므로 이를 대입하여 계산하면,
<center>$$v_0(t)=v_i(t)-\frac{\tau(v_0(t)-v_0(t-1))}{dt}$$</center>
<center>$$(dt)v_0(t)=(dt)v_i(t)=(\tau)(v_0(t)-v_0(t-1))$$</center>
<center>$$(\tau+dt)v_0(t)=(dt)v_i(t)+(\tau)v_0(t-1)$$</center>
<br/>
<center>$$\therefore v_0(t)=\frac{((dt)v_i(t)+(\tau)v_0(t-1))}{(\tau+dt)}$$</center>
-->
