---
title: "[Robot Laboratory 3] 2. Low Pass Filter"
excerpt: "Let's Talk About LPF"
header: 
    teaser: 

categories: 
    - Robot Laboratory 3
tags: 
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
디지털 LPF를 알아보기 전에 먼저 회로적인 LPF를 먼저 알아보자. 결국 회로적인 LPF와 디지털 LPF를 구현하는 게 같기 때문에 회로 LPF를 이해하면 디지털 LPF를 쉽게 이해할 수 있다. 회로 LPF는 아래와 같은 1차 RC 회로로 설계할 수 있으며, 이를 키르히호프 법칙으로 해석해 볼 것이다. 

<center>
<img src="\assets\images\learn\robot-laboratory-3\2021-07-13-robot-laboratory-3\img1.PNG" width="70%" height="70%">
</center>

<br>

먼저 키르히호프 법칙으로 미분방정식을 세워 시정수와 차단주파수를 계산해 보자.  

* $V=IR$ 이므로 → $v_{in}(t)-v_{out}(t)=Ri(t)$  
* 축전기의 전압과 전기용량의 관계($Q=CV$)에 의해 → $Q_c(t)=Cv_{out}(t)$  
* 전류의 정의에 의해 → $i(t)=\frac{dQ_c}{dt}$  

따라서, 
<center>$$v_{out}(t)=v_{in}(t)-RC\frac{dv_{out}(t)}{dt} ⋅⋅⋅ (1)$$</center>  

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

<center>$$\therefore f_c=\frac{1}{2\pi RC}, RC=\frac{1}{2\pi f_c} ⋅⋅⋅ (2)$$</center>

<br/>

## 2-2. RC Filter Realization

그럼 한 번 LPF를 설계를 해 보자. 위 (1)번 식을 다시 가져와 보자.  

<center>$$v_{out}(t)=v_{in}(t)-RC\frac{dv_{out}(t)}{dt} ⋅⋅⋅ (1)$$ </center>  

<br/>

이때 시정수는 $RC=\frac{1}{2\pi f_c}=\tau$, 차단주파수는 $f_c=\frac{1}{2\pi RC}$이므로 이를 대입하여 계산하면,
<center>$$v_0(t)=v_i(t)-\frac{\tau(v_0(t)-v_0(t-1))}{dt}$$</center>
<center>$$(dt)v_0(t)=(dt)v_i(t)=(\tau)(v_0(t)-v_0(t-1))$$</center>
<center>$$(\tau+dt)v_0(t)=(dt)v_i(t)+(\tau)v_0(t-1)$$</center>
<center>$$\therefore v_0(t)=\frac{((dt)v_i(t)+(\tau)v_0(t-1))}{(\tau+dt)} ⋅⋅⋅ (3)$$</center>

<br/>

그런데 우리는 ADC 작업을 거친 신호에 대해 필터링을 적용하는 것이기 때문에 엄밀히 따지면 (3)번 식의 표현은 연속신호에 대한 필터링 구현 식이므로 틀렸다. 이산 신호에 대한 표현으로 옳게 바꾸면 다음과 같다.  

<center>$$y_i=\frac{(\Delta t)x_i+(\tau)y_{i-1}}{\tau+\Delta t} ⋅⋅⋅ (4)$$</center>  

<br/>

즉, 현재 필터링된 값은 현재 필터링을 진행할 센서값과 바로 이전 샘플링 때 계산된 필터링 값을 사용하여 계산이 된다는 것을 알 수 있다.  

<br/><br/><br/>

# 3. 코드로 LPF 구현하기
기본 FFT와 노이즈 등의 파라미터 설정은 [이전 포스팅](https://sungjun0204.github.io/robot%20laboratory%203/fft/#3-2-%EC%9E%84%EC%9D%98-%EC%8B%A0%ED%98%B8-%EC%84%A4%EC%A0%95)에서 설명했으므로 설명이 필요하다면 링크를 타고 들어가 확인해 보기 바란다.  
<br/>
다음은 LPF를 MATLAB으로 구현한 코드이다.  

~~~matlab
%% LPF: cutoff is 2
    cutoff = 2;                     % 차단주파수 설정
    tau = 1 / (2 * pi * cutoff);    % 시정수 
    lpf_1(1) = 0;                     % 필터에 적용되는 첫번째 값을 설정
    n = 2;                          % index를 2번째부터 시작                           
    
    for(t = delta_t:delta_t:end_time) 
            output_l = ((delta_t * sim_y(n)) + (tau * lpf_1(n-1))) / (tau + delta_t);
                                    % LPF 계산식
            %get delta
            lpf_1(n) = output_l;      % LPF 계산 결과를 필터에 적용
            time(n) = t;            % 
            n = n + 1;              % 다음 index로 이동 
    end
~~~  

차단주파수 $f_c$를 2로 설정해 보았다. 즉, 2Hz 이하인 신호만 통과하고, 이보다 높은 주파수를 가진 신호는 차단하는 것이다. 현재 반복문은 0~5초까지 진행이 되며, 샘플링을 0.001s로 잡았기에 총 5001번 필터링을 진행할 것이다.  
코드를 자세히 보게 되면, 4번 줄에 `lpf_1(1) = 0` 이라고 있는데, 일단 `lpf_1` 는 필터가 적용된 값을 저장하는 일종의 배열 변수이다.(정확히는 행렬) 그런데 그 변수에 1번째에 0을 넣는 것인데, 앞서 언급했듯이 LPF는 <u>현재 필터링을 할 값</u>과 <u>바로 직전에 필터링된 값</u> 두 개를 사용하여 현재 센서값을 필터링을 한다고 했다. 그런데 맨 처음 필터링을 시작할 때, 직전 필터링된 값이 없으므로 계산이 안 된다. 이를 방지하기 위해 인위적으로 0을 집어넣어준 것이다.  

<br/>

이렇게 하여 필터링을 각각 차단 주파수 2, 10, 30Hz로 설정하고 코드를 돌려보았다. 결과는 다음과 같다.  

<center>
<img src="\assets\images\learn\robot-laboratory-3\2021-07-13-robot-laboratory-3\img2.PNG">
</center>  

<br/>

확실히 차단주파수를 낮출수록 그에 맞게 필터링이 잘 되는 것을 볼 수 있다. 그런데 잘 보면 차단주파수가 낮으면 낮을수록 그 만큼 지연이 생기는데, 이는 RC Filter의 특징으로, 어느 정도의 위상 지연(Phase Delay)이 발생하기에 R, C값을 적절히 선정하는 것이 중요하다. 디지털 필터도 마찬가지로 이 RC Filter를 기반으로 설계가 되었기에 적절한 샘플링 주기와 차단 주파수를 고려해야 한다.  

<br/>

<center>
<img src="\assets\images\learn\robot-laboratory-3\2021-07-13-robot-laboratory-3\img3.PNG">
</center>  

<br/>

그리고 위 사진은 차단주파수가 2Hz로 설정했을 때 필터링을 하기 전과 후를 Frequency Domain에서 확인한 것이다. 확실히 10Hz 구간이 필터링 후 많이 줄어드는 것을 확인할 수 있다.  

<br/>
<br/>
<br/>
<br/>