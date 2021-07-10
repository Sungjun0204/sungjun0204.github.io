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
 <br/>
※ 본 포스팅에서는 푸리에 변환에 대한 수학적인 설명이 아닌, 디지털 필터를 분석하기 위한 "수단"으로서만 설명합니다. 
<br/><br/><br/><br/>

# 1. Fourier Transform(푸리에 변환)
## 1-1. 푸리에 급수  
푸리에 변환을 알아보기 전에, 푸리에 급수에 대해 얘기할 필요가 있다. 푸리에 급수의 일반적인 모습은 다음과 같이 쓸 수 있다.

 
<center>
$f(x) = \frac{A_0}{2} + \sum_{n = 1}^{\infty}(A_ncos\frac{n\pi}{L}x+B_nsin\frac{n\pi}{L}x) (x\in (-L, L))$
</center>
<br/>

어떠한 주기함수를 sin과 cos의 급수합으로 표현을 할 수 있는 것인데, 이는 즉 모든 주기함수 그래프를 삼각함수 그래프의 합들로 표현이 가능하다는 것을 의미한다.  

<center>
<img src="\assets\images\2021-07-10-robot-laboratory-3\img1.png" width="70%" height="70%">
</center>

위 이미지는 각 사각파, 삼각파를 삼각함수의 급수로 표현한 것이다. 이런 식으로 많은 주기함수를 삼각함수의 급수로 표현할 수 있다.

<br/>

## 1-2. 푸리에 변환  
그럼 푸리에 변환으로 무엇을 할까? 수식적 정의를 확인해보자.


<center>
$X(\zeta)=\int_{-\infty}^{\infty}x(t)e^{-2\pi i\zeta t} dt$
</center>
<br/>

해당 수식에서의 $\zeta$는 주파수를 의미하며, 독립변수 $t$는 시간을 의미한다. 즉, 시간축에서 정의되는 함수 $x(t)$를 주파수영역에서 바라보는 것이다. 이때 주파수영역에서 바라본 $x(t)$는 $X(\zeta)$가 되는 것이다. 아래의 그림을 보자. 

<center>
<img src="\assets\images\2021-07-10-robot-laboratory-3\img2.png">
</center>
<br/>

왼쪽 빨간색 그래프가 우리가 분석하고 싶은 신호이다. 그런데 우리는 이 신호를 푸리에 급수를 이용해 삼각함수들의 합으로 표현이 가능하므로 삼각함수들로 분리를 한다. 그런 다음 시간에 대해 보이는 빨간색 신호를 주파수에 대해 보기 위해 푸리에 변환을 진행하면 파란색 그래프처럼 결과가 나오게 된다. 

즉, 원래 신호를 주파수 영역에서 분석하여 해당 신호가 가지고 있는 주파수 정보를 분석하기 위해 사용하게 된다. 우리는 이런 수학적 도구를 이용하여 원하는 주파수 범위에 있는 신호만 사용할 것이다. 이것이 바로 우리가 필터를 사용하기 위한 기본 개념이다.  

<br/><br/><br/>

# 2. Fast Fourier Transform(FFT)(고속 푸리에 변환)
그런데 푸리에 변환은 시간에 대한 연속성이 고려되지 않아 문제점이 좀 많다. 그런데 어차피 우리는 센서를 이용해 값을 받을 때 ADC를 이용해 값을 받게 된다. 즉, 연속 신호를 이산 신호로 바꾸기 때운에, 우리는 이산 푸리에 변환(DFT)을 이용해 신호 그래프를 변환하면 된다. 

여기서 "고속 푸리에 변환"이라는 개념이 등장한다. 고속 푸리에 변환(FFT)은 이산 푸리에 변환이나 그의 역변환을 빠르게 계산해주는 일종의 알고리즘이다. 우리는 이를 이용할 것이다.  

<br/><br/><br/>

# 3. FFT 구현하기
## 3-1. FFT 구현
FFT를 MATLAB으로 구현해보자.  
~~~matlab
%% Calc FFT
    % Set FFT
        Fs       = 1/delta_t;       % Sampling Frequncy : 1000Hz
        T        = delta_t;         % Sampling Period : 0.001s
        L        = length(sim_y);   % Length of Signal : 5001
        T_vector = (0:L-1)*T;       % Time Vector :1x5001 vector    
        fft_f    = Fs*(0:(L/2))/L;  % Frequency Range : 1X2501 vector 
    % Calc FFT
        fft_y_temp = abs(fft(sim_y)/L);     % Remove Imaginary Number
        fft_y = fft_y_temp(1:L/2+1);        % 켤레 복소수 대응
        fft_y(2:end-1) = 2*fft_y(2:end-1);  % 켤레 복소수 대응
~~~

샘플링 주파수는 1000Hz, 샘플링 주기는 0.001s로 설정하였다. 그리고 FFT를 하기 위한 신호 범위를 0~5000까지로 설정하기 위해 5001로 썼으며, 시간 범위는 신호 범위에 맞춰 0~5초까지로 설정하였다. 주파수 범위는 0~500Hz까지이며, 분해능은 0.2Hz로 설정했다.  
9번째 줄부터 보게 되면 허수부를 제거하는 식으로, 우리는 FFT의 값에 절대값을 씌워 크기만 도출할 것이다. 그리고 푸리에 변환을 진행하게 되면 250Hz를 기준으로 켤례복소수가 발생하는데, 우리는 양수 부분만 볼 것이므로 이를 하나로 처리하였다.  

<br/>

## 3-2. 임의 신호 설정
FFT의 계산을 확인하기 위해서는 변환할 신호가 있어야 하는데, Matlab으로 테스트를 하는 것이기에 임의의 신호를 만들어서 확인해 보았다. 다음은 FFT변환을 하기 위해 임의로 만든 신호 설정이다. 


~~~matlab
%% Set Parameters
    % Set Simulation Time
        end_time = 5;           % 그래프에 표시될 마지막 시간
        delta_t = 0.001;        % 샘플링 주기
    % Set sine Wave
        sine_mag = 2;           % sin 그래프 크기
        sine_freq = 1;          % sin 그래프 진동수
~~~  

위 FFT를 구현한 것과 동일하게 5초까지 시뮬레이션 시간을 설정하고 샘플링 주기도 0.001s로 동일하게 설정한다. 또한 sin파의 magnitude = 2, 진동수를 1로 설정해준다.  
<br/>

~~~matlab
%% Set parameter 2 Simulation 2
    % Set Simulation
        end_time = 5;           % 그래프에 표시될 마지막 시간
        delta_t = 0.001;        % 샘플링 주기
        
        sim_time = [0:0.001:5]; % 0초부터 5초까지 0.001주기로 끊어본다
    %Set sine Wave
        sine_mag1 = 2.0;    sine_freq1 = 1.0;       % Main Signal
        sine_mag2 = 0.5;    sine_freq2 = 10.0;      % Noise Signal
        
        normal_sine = sine_mag1 * sin(sine_freq1 * (2 * pi * sim_time));
        noise_sig = sine_mag2 * sin(sine_freq2 * (2 * pi * sim_time));
        rand_sig = 0.8 * randn(size(sim_time));
        
        sim_y = sine_mag1 * sin(sine_freq1 * (2 * pi * sim_time))...
                + sine_mag2 * sin(sine_freq2 * (2 * pi * sim_time))...  % 크기 0.5주파수 10Hz 노이즈 생성
                + 0.8 * randn(size(sim_time));  % 랜덤 노이즈 생성
~~~  

먼저 11번 줄은 크기가 2, 진동수가 1인 정상파, 12번은 크기가 0.5, 진동수가 10인 노이즈파, 13번은 평균이 0이고 표준편차가 0.8인 white 노이즈파이다. 이 셋을 전부 더해서 최종 노이즈 신호를 만든다.  

<center>
<img src="\assets\images\2021-07-10-robot-laboratory-3\img7.png" width="80%" height="80%">
</center>
<br/>
위 사진은 각각 임의로 생성한 신호를 그래프로 출력해 본 것으로, 첫 번째 신호가 나머지 것들을 다 더한 최종 신호 그래프이다.  
<br/>
<br/>
최종 생성된 신호에 FFT를 적용시키면 다음과 같은 그래프가 그려진다. 

<center>
<img src="\assets\images\2021-07-10-robot-laboratory-3\img6.png">
</center>

<br/>
각 주파수별로 분해가 되어서 Frequency-Domain에 표시가 되는 것을 확인할 수 있다. 
White noise는 FFT를 진행했을 때 Frequency-Domain에서는 낮게 깔리는 형태를 보이고 있는데, 이러한 노이즈를 "전자파 노이즈"라고 한다. 

<br/>
<br/>
<br/>
<br/>