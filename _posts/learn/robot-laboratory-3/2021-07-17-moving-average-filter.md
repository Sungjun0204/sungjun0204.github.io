---
title: "[Robot Laboratory 3] 3. Moivng Average Filter"
excerpt: "Let's Talk About MAF"
header: 
    teaser: 

categories: 
    - Robot Laboratory 3
tage: 
    - Robot Laboratory 3
    - Filter
    - Moving Average Filter
last_modified_at: 2021-07-17t01:31-15:00
comments: true
toc: true
toc_sticky: true
use_math: true
---

<br/><br/><br/><br/>

# 1. Moving Average Filter(MAF)
이동 평균 필터(Moving Average Filter)란, 각 샘플링 시간이 지날 때마다 일정한 갯수의 표본들의 평균을 내어 필터링을 하게 된다. 즉, 표본 5개를 기준으로 필터링을 한다 하면 다음과 같이 표본 갯수를 유지하면서 데이터를 갱신하는 방식으로 필터링을 진행하게 된다. 

<br/>

<center>
<img src="\assets\images\learn\robot-laboratory-3\2021-07-17-moving-average-filter\img2.jpg">
</center>  

<br/>

위 그림을 보면 표본으로 5개를 유지하고 있다. 그런데 표본으로 정한 데이터가 고정이 아니라, 단위시간이 지날 때마다 표본 중 가장 오래된 데이터를 버리고, 새로운 데이터를 표본으로 선택하여 평균을 낸다. 이것이 이동 평균필터의 기본 알고리즘이다. 

<br/>

## 1-1. Normal Average Filter
"이동 평균필터"라는 이름을 봤을 때는 평균을 내어 필터링을 한다는 것을 알 수 있다. 그런데 어떻게 평균만으로 필터링이 가능한 것일까?  

원래 단순히 데이터들을 평균을 내는 것 만으로 필터링이 가능하다. 노이즈가 단순하거나 드문 경우에는 효과를 보이나, 많은 경우에는 노이즈가 그렇게 만만치 않기에 필터링에 한계가 있다. 다음 그래프를 보자.  

<br/>

<center>
<img src="\assets\images\learn\robot-laboratory-3\2021-07-17-moving-average-filter\img1.jpg">
</center>  

<br/>

파란색 그래프가 일반 데이터이고, 주황색이 단순히 평균을 내어 그 값을 표시한 것이다. 평균을 계산한 방식은, 시간이 지남에 따라 데이터를 계속 누산하고, 누산한 데이터의 개수만큼 나누어 주었다. 코드는 다음과 같이  C언어로 간단하게나마 작성하여 단순 평균 필터링 데이터를 계산했다.  

~~~c
// arr의 데이터를 단순 평균필터링하는 코드
#include <stdio.h>

int main()
{
	double arr[14] = { 11, 26, 38, 15, 41, 16, 43, 25, 35, 20, 45, 30, 36, 31 };
	double sum = 0;
	double result[14] = { 0, };
	double n = 1;

	for (int i = 0; i < 14; i++)
	{
		for (int j = i; j >= 0; j--)
			sum = sum + arr[j];

		result[i] = sum / n++;
		printf("%lf ", result[i]);

		sum = 0;
	}

	return 0;
}
~~~


그래프를 보면 얼핏 필터링이 잘 되는 듯 하다. 그런데 이러한 필터링 방식은 측정하려는 값이 시간에 따라 변하는 경우 사용하게 되면 필터링이 잘 안 된다. 전체적으로 평균을 계산하게 되므로 데이터의 동적인 변화는 모두 없애버리고 측정 데이터를 어느 정도 무시하여 달랑 하나의 값으로 제시해 버리기 때문이다. 다음 그래프를 보자. 

<br/>

<center>
<img src="\assets\images\learn\robot-laboratory-3\2021-07-17-moving-average-filter\img3.jpg">
</center>  

<br/>

코드는 MATLAB으로 다음과 같이 작성하였다.  

~~~matlab
%% 단순 평균필터   
    n = 1;  % 표본의 갯수
    
    for(t = delta_t : delta_t : end_time)   % 0.001초부터 5초까지 0.001씩 증가
        for(i = 0 : 1 : (t*1000))     % 표본 누적
            buffer(i + 1) = sim_y(i + 1);   % 버퍼에 저장
        end
        
        average_c = sum(buffer) /  (t*1000);
                    % 평균 값 계산
        
        n = n + 1; % 표본 갯수 1개 증가
        maf(n) = average_c;   % 계산한 평균값 저장
    end
~~~

이전 포스팅부터 계속 사용한 노이즈 신호에 단순 평균 필터를 적용한 모습이다. 초반 약 0.4초 정도까지는 잘 따라오나 싶었으나, 뒤로 갈수록 본래의 신호보다 더 약해지더니 거의 파형 자체가 약해지는 것을 알 수 있다. 이렇듯 데이터 측정 시간이 길어질수록 동적 변화량이 모두 사라져 버리기에 단순 평균값으로 필터링을 하는 것은 무리가 있다. 이를 보완하기 위해 등장한 것이 "이동 평균필터"라고 보면 된다.

<br/>

## 1-2. Formula of MAF

위에서 설명했듯이, 이동 평균필터는 모든 데이터의 평균이 아닌, 지정된 개수의 최근 측정값만의 평균을 이용하게 되며, 오래된 데이터는 버리고 최근 값을 가지고 평군을 구해주는 원리이다. 이를 고려하여 이동 평균필터를 수식으로 표현하면 다음과 같다. 

<center>$$\overline{X_k}=\frac{X_{k-n+1}+X_{k-n+2}+ ... + K_k}{n} ⋅⋅⋅ (1)$$</center>  

이 (1)번 식을 다시 재귀식으로 바꾸면 다음과 같이 쓸 수 있다.  

<center>$$x_k - x_{k-1} = \frac{(x_{k-n+1} + x_{k-n+2} + ... + x_k) - (x_{k-n} + x_{k-n+1} + ... + x_{k-1})}{N} = \frac{x_k - x_{k-n}}{N} ⋅⋅⋅ (2)$$</center>  

<center>$$\therefore \overline{X_k} = \overline{X}_{k-1} + \frac{x_k - x_{k-n}}{N} ⋅⋅⋅ (3)$$</center>  

<br/>

평균을 사용하기에 노이즈에 강하긴 하나, 어느 정도의 표본 데이터를 추출한 후에 필터링을 거치기 때문에 지연이 생기게 된다.  

<br/><br/><br/>

# 2. MAF 구현하기
## 2-1. MATLAB 함수로 구현하기
MATLAB에서 지원하는 `filter()`라는 필터링 함수가 있다. 이 함수가 필터링을 하는 원리가 MAF 방식이라고 하므로, MAF를 사용하고 싶다면 사실 이 함수를 사용하면 된다.  

~~~matlab
%% MAF
    windowsize = 100;   % 100개의 표본으로 평균을 구한다
    num = (1/windowsize) * ones(1, windowsize);
    den = [1];
    maf = filter(num, den, sim_y);
~~~

`filter(a, b, c)`함수에 대한 설명은 [MATLAB 홈페이지](https://kr.mathworks.com/help/matlab/ref/filter.html)에서 잘 설명해 주고 있다. 결과는 다음과 같이 나온다.  

<center>
<img src="\assets\images\learn\robot-laboratory-3\2021-07-17-moving-average-filter\img4.jpg">
</center>  

앞서 설명했듯이 표본 데이터를 추출하는 과정이 있어 어느 정도 지연이 있는 것을 확인할 수 있다.  

<br/>

## 2-2. 수식으로 구현하기
이번에는 위에서 설명한 재귀식을 토대로 코드를 구현해 보겠다. 코드는 MATLAB 상에서 구현했으며, 다음과 같다.  

~~~matlab
%% MAF by formula
    windowsize_c = 100;     % 100개의 표본으로 평균을 구한다
    n = windowsize_c;       
    
    % 표본들을 가지고 평균을 계산한다
    for(t = windowsize_c * delta_t : delta_t : end_time)
        for(i = 0 : 1 : windowsize_c - 1)
            buffer(i + 1) = sim_y(n - i);   % 버퍼에 저장
        end
        
        average_c = sum(buffer) /  windowsize_c;
                    % 실제 평균 값 계산
        
        n = n + 1; 
        sim_y_maf(n) = average_c;   % 계산한 평균값 저장
    end
~~~

6번 줄에서는 표본의 개수에 따른 샘플링이며, 표본 데이터는 100개로 설정했다. 즉 t는 0.1부터 5까지 0.001씩 증가하게 된다. 코드를 보면 0.001씩 샘플링을 진행하는데 0.1부터 시작을 한다. 막상 보면 이해가 안 될 텐데, 앞서 설명했듯이 MAF는 표본 추출 작업이 있기에 지연이 발생한다고 했다. 그런데 신호를 막 받기 시작할 때에는 표본이 충분히 받아지지 않기에 표본이 다 모일때 까지 필터링을 진행하지 않는 것이다. 해당 코드에서는 표본을 100개로 설정했으므로, 0.001s부터 0.1s까지 100개의 초기 데이터를 받을 때까지는 필터링을 생략한 것이다.  

7~8번 줄에서는 표본 100개를 받는 코드이다.  
11번 줄에서 표본 100개에 대한 평균을 계산하고 14번 줄에서 다음 샘플링 시간에 따라 표본 추출 구간을 1칸 움직이게 한다. 이렇게 계산된 필터링 값을 15번 줄에서 차례대로 저장한다.  
따라서 그래프를 그리게 되면 다음과 같이 나온다.  

<center>
<img src="\assets\images\learn\robot-laboratory-3\2021-07-17-moving-average-filter\img5.jpg">
</center>  

코드를 작성한 대로 필터링 초반에 어느 정도 지연이 된 것을 확인할 수 있다.  

다음은 MATLAB 함수 필터링과 수식 필터링을 비교한 그림이다.  

<center>
<img src="\assets\images\learn\robot-laboratory-3\2021-07-17-moving-average-filter\img6.jpg">
</center>  

<center>
<img src="\assets\images\learn\robot-laboratory-3\2021-07-17-moving-average-filter\img7.jpg">
</center>  

필터링 성능이 거의 일치함을 볼 수 있으며, 초반 99개의 표본을 추출하기 전 까지 수식 구현 필터가 지연이 됨을 알 수 있다.  
그럼 왜 MATLAB 함수로 구현한 것은 왜 이런 구간이 없는 것일까? 일단 해당 코드는 MATLAB에서 작성을 한 것이다. 필터링 테스트를 위해 노이즈 신호도 임의로 만들어 낸 것이기에 MATLAB 입장에서는 해당 신호에 대해 다 알고 있는 상태이다. 따라서 최초 100개의 표본 추출 전에도 필터링을 진행할 수 있는 것이다.  
그런데 이는 의미가 없다. 실제 임베디드에서 필터링을 사용하게 되면 당연히 신호를 모르는 상태이기 때문에 수식으로 구현한 필터처럼 코드를 구현해야 한다.  

마지막으로 Frequency Domain에서 필터링이 잘 되는지 확인해 보자.  

<center>
<img src="\assets\images\learn\robot-laboratory-3\2021-07-17-moving-average-filter\img8.jpg">
</center>  
<center>
<img src="\assets\images\learn\robot-laboratory-3\2021-07-17-moving-average-filter\img9.jpg">
</center>  
<center>
<img src="\assets\images\learn\robot-laboratory-3\2021-07-17-moving-average-filter\img10.jpg">
</center>  

<br/>

필터링이 잘 되는 것을 확인할 수 있다. 

<br/><br/><br/>

