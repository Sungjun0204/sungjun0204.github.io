---
title: "[Magnetic Robot Lab] 2. Paper Review 1(2)"
excerpt: "Expanded Equations for Torque and Force on a Cylindrical Permanent Magnet Core in a Large-Gap Magnetic Suspension System"
header: 
    teaser: \assets\images\me.png

categories: 
    - Magnetic Robot Laboratory
tags: 
    - magnetic robot lab
last_modified_at: 2021-08-17t17:23-23:00
comments: true
toc: true
toc_sticky: true
use_math: true
---

<br/>

이전 포스팅에서는 해당 논문의 도입부와 본 내용을 이해하기 위한 Appendix A를 알아보았다. 한 포스팅에 다 적으면 너무 길어지므로 호흡 한 번 할 겸 적절히 나눠서 포스팅한다. 저번 포스팅에 이어 오늘은 Appendix B부터 공부해 보자.  

<br/><br/>

# 1. Appendix B
Torques and Forces on a Magnetic Dipole With Incremental Volume  
(증분 부피를 갖는 자기 쌍극자에서 가해지는 토크와 힘)  

크기가 일정한 자기장에서 자기 쌍극자에 가해지는 토크와 힘은 자기 모멘트가 동일한 미세 전류 루프에 가해지는 토크, 힘과 동일하다는 것을 먼저 언급하면서 시작한다. 이 내용이 무엇을 의미하길래 먼저 언급을 할까? 쉽게 풀어 말하면,  

**"Suspension System(자기장을 발생시키는 커다란 코일)에 극소량의 전류를 흘려 발생하는 힘과 토크는, 크기가 일정한 자기장에서 Magnetic Core에 가해지는 힘과 토크와 동일하다."**  

는 의미이다.  
그러면 왜 갑자기 자기 쌍극자 얘기가 나오는 것인가? 이전 포스팅에서 좌표계 변환의 이유를 설명하면서 다음과 같이 언급했다.  

>그럼 왜 좌표계를 다르게 쓸까? 우리가 결국 알고 싶은 것은 “코일이 발생시키는 자기장”이 아닌, “자석 로봇의 자기장”, 자석 로봇 그 자체가 어떻게 움직이는지를 알고 싶은 것이다.  

<center>
<span style=
"font-size:70%;
color:gray">

[해당 글이 있는 포스팅으로 이동](https://sungjun0204.github.io/magnetic%20robot%20laboratory/first-paper-review/#3-1-transformation-of-frame)

</span>
</center>

<br/>

 우리가 알고 싶은 것은 Suspension System의 자기장이 아닌 Magnetic Core의 자기장이다. 이를 잊어서는 안 된다. 따라서 Magnetic Core에 가해지는 토크와 힘을 구해야 하는데, 해당 Suspension System이 발생시키는 자기장 안에 있는 Magnetic Core를 하나의 자기 쌍극자로 보는 것이다.  

그럼 자기 쌍극자는 무엇이냐? 일단 자기장에서 어떠한 물체가 반응하여 토크가 발생하는 정도를 나타내는 벡터 물리량인 "자기 모멘트"라는 것이 있다. 그런데 이러한 모멘트를 가지고 있는 "계"를 "자기 쌍극자"라고 하는 것이다. 이 정도 설명하면 다들 이해 하리라 생각한다. 살짝 꼬리에 꼬리를 물면서 설명을 하게 되지만, Appendix B를 이해하기 위해서는 이 정도는 인지하고 있어야 하므로 깊게 설명했다. 자기 쌍극자에 대한 얘기는 [여기](https://ko.wikipedia.org/wiki/%EC%9E%90%EA%B8%B0_%EB%AA%A8%EB%A9%98%ED%8A%B8)에서 자세히 설명해주고 있으므로 참고 바란다. 

~~사실 이에 대해 자세히 알고 싶어 Reference 9를 읽으려고 봤는데 Cambridge대학에서 쓴 몇백 페이지 교제라 다 읽을 엄두가 안 난다 ㅎㅎ...~~  

<br/>

## 1-1. Infinitesimal Current Loop

우선 자기 쌍극자에 대한 그림을 논문에서 제시해주고 있다.  

<center>
<img src="\assets\images\study\magnetic-robot-lab\2021-08-14-first-paper-review\img4.JPG" width="60%" height="60%">
</center>  

<center>
<span style=
"font-size:70%;
color:gray">
논문에서 제시한 자기 쌍극자에 대한 그림. 크기가 일정한 자기장 B에서 일정한 전류 I가 흐르는 전도체(Magnetic core)의 평면 루프의 모습.
</span>
</center>

<br/>

먼저 자기 쌍극자에 가해지는 힘 $ \mathbf{F} $ 를 알아보자. 이는 로렌츠 법칙에 의해 다음과 같이 정의된다.  

<center>$$d \mathbf{F} = I d \mathbf{I} \times \mathbf{B}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B1: 로렌츠 힘 법칙. dF는 전도체의 힘 벡터, I는 전도체에 흐르는 전류, dI는 전도체의 길이만큼의 크기를 가지는 (+)방향인 벡터, B는 전도체 외부의 자속밀도(자기장)
</span>
</center>

<br/>

또한 토크 $ \mathbf{T} $ 는 다음과 같이 정의될 것이다.  

<center>$$\mathbf{T} = I \oint [\mathbf{r} \times (d \mathbf{I} \times \mathbf{B})]$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B2: B1에 따른 토크에 대한 식. B1이 현재 미소 부피에 대한 식이므로 폐루프에 대해 적분을 해야 한다.
</span>
</center>

<br/>

수식 해석은 간단하다. 위 자기 쌍극자 그림에서 Right Hand Rule을 이용하면 $ \mathbf{F} $ 의 방향은 루프 기준으로 밖으로 향하는 쪽으로 결정이 된다. 거기에 $ \mathbf{r} $ 과 외적을 취하게 되면 전류 $ I $ 가 흐르는 방향, 즉 토크의 방향이 결정된다. B1, B2식의 앞에 곱해져 있는 $ I $ 는 전류의 크기(상수)이므로 앞으로 뺀 것이다.  

그런데 B2식은 벡터 항등식에 의해 다음과 같이 일부를 바꿔 쓸 수 있다.  

<center>$$\mathbf{r} \times (d \mathbf{l} \times \mathbf{B}) = d \mathbf{I} (\mathbf{r} \cdot \mathbf{B}) - \mathbf{B} (\mathbf{r} \cdot d \mathbf{I})$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B3: "미분이 없는 벡터 항등식"에 의하여 B2식 일부를 변경한 식
</span>
</center>

<br/>

이를 다시 B2식에 대입하면,  

<center>$$\mathbf{T} = I [\oint (\mathbf{r} \cdot \mathbf{B}) d \mathbf{I} - \mathbf{B} \oint \mathbf{r} \cdot d \mathbf{I}]$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B4: B3식을 B2식에 대입한 모습
</span>
</center>

<br/>

그리고 B4식에 Stock's Thorem을 적용하면 다음과 같이 된다.  

<center>$$\oint_{s} (\triangledown \times \overrightarrow{A}) \cdot d \overrightarrow{s} \equiv \oint_{l} \overrightarrow{A} \cdot d \overrightarrow{l}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
참고: Stock's Theorem(선적분을 면적분으로 바꾸는 식)
</span>
</center>

<br/>

<center>$$\mathbf{T} = I \left \{ \int_{s} [d \mathbf{A} \times \triangledown(\mathbf{r} \cdot \mathbf{B})] - \mathbf{B} \int_{s} (\triangledown \times \mathbf{r}) \cdot d \mathbf{A} \right \} $$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B5: B4식에 Stock's Theorem을 적용한 모습
</span>
</center>

<br/>

B5식을 잘 보면 $ (\triangledown \times \mathbf{r}) $ 은 $ Curl \; \mathbf{r} $ 로 볼 수 있다. 그런데 $ \mathbf{r} $ 은 Position Vector이므로 이의 값은 0이 된다.  
$ \triangledown (\mathbf{r} \cdot \mathbf{B}) $ 의 경우, 벡터 항등식에 의해 다음과 같이 쓸 수 있다.  

<center>$$\triangledown (\mathbf{r} \cdot \mathbf{B}) = \mathbf{r} \times (\triangledown \times \mathbf{B}) + \mathbf{B} \times (\triangledown \times \mathbf{r}) + (\mathbf{r} \cdot \triangledown) \mathbf{B} + (\mathbf{B} \cdot \triangledown) \mathbf{r}$$</center>

<br/>

그런데 우리는 Maxwell의 4대 방정식에서, $ \triangledown \times \mathbf{B} = \triangledown \cdot \mathbf{B} = 0 $ 임을 알고 있다. 또한 Position Vector $ \mathbf{r} $ 의 divergence는 상수이고, Curl은 0이기에, $ \mathbf{T} $ 는 다음과 같이 쓸 수 있다.  

<center>$$\mathbf{T} = I \int_{s} (d \mathbf{A} \times \mathbf{B})$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B6: B5식을 정리한 모습
</span>
</center>

<br/>

<center>$$\mathbf{T} = I \mathbf{A} \times \mathbf{B}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B7: B6식에서 적분을 적용한 모습
</span>
</center>

<br/>

그런데 $ I \mathbf{A} $ 는 자기 모멘트 $ \mathbf{m} $ 이므로, 다음과 같이 토크에 대한 식이 성립힌다.  

<center>$$\mathbf{T} = \mathbf{m} \times \mathbf{B}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B8: 자기 모멘트로 B7식을 다시 쓴 모습
</span>
</center>

<br/>

또한, 외적의 형태로 정의가 되어 있으므로, $ \mathbf{m} $ 과 $ \mathbf{B} $ 가 $ \theta $ 만큼 틀어져 있으면 다음과 같이도 쓸 수 있다.  

<center>$$\mathbf{T} = \mathbf{m} \mathbf{B} sin \theta $$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B9: 자기 모멘트 m과 자기장 B가 90도가 아닌 다른 각도로 틀어져 있을 경우의 토크 식
</span>
</center>

<br/>

이제 토크에서 힘에 대한 수식을 유도해 보자. 해당 loop에서 $ d \theta $ 만큼 움직였다고 했을 때, 일 $ W = Fs $ 은 다음과 같이 표현할 수 있다.

<center>$$dW = \mathbf{T} d \theta = \mathbf{m} \mathbf{B} sin \theta d \theta$$</center>

<br/>

그리고 위치에너지에 대해서도 다음과 같은 관계가 성립하게 된다.

<center>$$dU = dW = \mathbf{T} d \theta = \mathbf{m} \mathbf{B} sin \theta d \theta$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B10:  dθ만큼 증가시킬 때 Potential Energy와 Work, 그리고 토크의 관계
</span>
</center>

<br/>

그런데 $ dU $ 를 적분하여 $ U $ 를 얻기 위해 적분을 하면, 

<center>$$U = - \mathbf{m} \mathbf{B} cos \theta = - \mathbf{m} \cdot \mathbf{B}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B11: B10식을 적분한 형태. cosθ가 있으므로 내적 형태로 쓸 수 있다. 
</span>
</center>

<br/>

그리고 우리는 <abbr title="힘이 가해진 방향으로 움직인 물체의 거리">일</abbr> $ W $ 가 $ Fs $ ( $ F $ : 가해지는 힘 , $ s $ : 거리) 라는 것을 알고 있다. 그러면 다음과 같이 정리가 가능하다. 

<center>$$dW = \mathbf{F} \cdot d \mathbf{r} = -dU = - \triangledown U \cdot d \mathbf{r}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B12: 일과 Potential Energy 사이의 관계식 
</span>
</center>

<br/>

그러나 B12식을 처음 봤을 때 $ dW = \mathbf{F} \cdot d \mathbf{r} $ 는 알겠는데 나머지 관계가 이해가 가지 않았다. 열심히 이곳저곳을 뒤져보니 다음에서 설명을 자세히 해 주고 있다. 혹여나 이해가 가지 않는 분은 해당 링크를 참고 바란다.    

* $ dW = -dU $ :  <http://hyperphysics.phy-astr.gsu.edu/hbase/pegrav.html#pec>
* $ dU = \triangledown U \cdot d \mathbf{r} $ : <https://ocw.mit.edu/courses/aeronautics-and-astronautics/16-07-dynamics-fall-2009/lecture-notes/MIT16_07F09_Lec13.pdf>

<br/>

따라서 다음과 같은 식이 도출된다.  

<center>$$\mathbf{F} = - \triangledown U = \triangledown (\mathbf{m} \cdot \mathbf{B})$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B13: 힘 F에 대한 수식 도출 
</span>
</center>

<br/>

그런데 B13식을 잘 보면, B5식에서 B6식으로 바꿔 표현하기 위해 사용한 벡터 항등식 꼴이 보인다. 이를 다시 B13식에 적용해 보면, 

<center>$$\triangledown (\mathbf{m} \cdot \mathbf{B}) = \mathbf{m} \times (\triangledown \times \mathbf{B}) + \mathbf{B} \times (\triangledown \times \mathbf{m}) + (\mathbf{m} \cdot \triangledown) \mathbf{B} + (\mathbf{B} \cdot \triangledown) \mathbf{m}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B14: B13식을 벡터 항등식에 의해 다시 쓴 모습 
</span>
</center>

<br/>

위에서 설명한 대로 Maxwell 4대 방정식에 외적의 물리적 의미에 의해 다음과 같이 $ F $ 가 최종적으로 구해진다. 

<center>$$\mathbf{F} = (\mathbf{m} \cdot \triangledown) \mathbf{B}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B15: F에 대한 최종 수식 
</span>
</center>

<br/>





## 1-2. Magnetic Dipole With Incremental Volume 

여기서는 자기 모멘트 $ \mathbf{m} $ 에 대한 수식을 다르게 설명하고 있다. N극과 S극이 길이 $ l $ 만큼 떨어져 있는 영구자석의 자기 쌍극자(Magnetic Dipole)의 자기 모멘트는 <abbr title="두 자석이 서로 같거나 반대 극성을 가질 때 자석의 한 면에 의해 다른 자석의 표면에 가해지는 힘">Pole Strength</abbr>를 이용하여 다음과 같이 정의가 된다.  

<center>$$\mathbf{m} = Q_m l$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B16: Pole Strength에 대한 자기 모멘트 m의 수식 
</span>
</center>

<br/>

그러나 실질적인 자석에서는 $ Q_m $ 이나 $ l $ 이 불명확하다. 단, 큰 거리 상에 있는 자석의 자기장을 특정하기에는 충분한데, 즉 자기 모멘트가 $ Q_m l $ 인 자기 쌍극자는 극소 전류 루프와 동급으로 볼 수 있으며, $ Q_m = I \mathbf{A} $ 가 성립된다. 따라서 정상상태의 자기장 $ \mathbf{B} $ 에서는 B8식과 B15가 동일하게 적용이 된다.  

해당 Appendix B에서는 부피가 $ v $ 인 영구자석이 같은 방향으로 향하고 있는 증분 부피(Incremental Volume) $ \delta v $ 를 가지는 큰 수치로 일정하게 분포된 영구자석 쌍극자로 구성되어 있다고 가정을 한다. 그래서 미소 부피 $ \delta v $ 를 가지는 쌍극자에서의 미소 자기 모멘트 $ \delta \mathbf{m} $ 는 <abbr title="자화(Magnetization)란, 자성체에 있는 영구(혹은 유도) 자기 쌍극자들의 밀도를 표현한 벡터장의 일종이다. ~화 라고 적혀있어 무슨 현상을 의미하는 것 같지만 아니므로 주의">자화벡터</abbr> $ \mathbf{M} $ 을 다음과 같이 정의할 수 있다.  

<center>$$\mathbf{M} = \delta \mathbf{m} / \delta v$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B17: 자화벡터의 정의 
</span>
</center>

<br/>

자화에 대한 내용은 [여기](https://en.wikipedia.org/wiki/Magnetization)로 가면 잘 설명해 주고 있으므로 자화 개념에 대해 생소한 분은 참고 바란다.  

B17에서, $ \mathbf{M} $ 을 부피에 대해 적분을 하면 다음과 같이 자기 모멘트를 정의할 수 있다.  

<center>$$\mathbf{m} = \int_v \mathbf{M} \; dv$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B18: B17식에서 자기 모멘트 m에 대해 정의한 모습
</span>
</center>

<br/>

그런데 우리는 자기장이 전체적으로 일정하다고 가정을 하였다. 그렇다는 것은, Magnetic Core가 일정하게 자화된다는 의미인데, 이는 결국 Magnetic Core의 부피에 대해 자화가 일정하게 걸린다는 의미이다. 따라서 다음이 성립한다.  

<center>$$\mathbf{m} = \mathbf{M} v$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B19: 일정하게 자화가 될 때의 자기 모멘트
</span>
</center>

<br/>

따라서 증분 부피에 대해서도 자기 모멘트가 일정하므로, 최종적으로 다음이 성립한다.  

<center>$$\delta \mathbf{T} = (\mathbf{M} \times \mathbf{B}) \delta v$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B20: Magnet Core의 증분 부피에 대한 토크
</span>
</center>

<br/>

<center>$$\delta \mathbf{F} = (\mathbf{M} \cdot \triangledown) \mathbf{B} \delta v$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
B21: Magnet Core의 증분 부피에 대한 힘
</span>
</center>




<br/><br/><br/>










# 2. The Main Content

자, 드디어 해당 논문의 핵심 내용을 이해하기 위한 준비가 끝났다. 그럼 우리는 앞서 살펴 본 Appendix에서 무슨 내용을 얻은 것인가?  

* Appendix A: 자기장을 2차까지 확장이 가능  
* Appendix B: Magnetic Core에 작용되는 토크와 힘  

이 점을 인지하고 메인 내용으로 바로 들어가 보자.  

<br/>




## 2-1. Magnetic Torques and Forces

이제 본격적으로 해당 부분부터 Magnetic Core에 적용을 하면서 설명한다. Suspension System 한 가운데에 Magnetic Core가 있다고 하면, 해당 Core의 미소 부피를 다음과 같이 그림으로 제시하였다.  

<center>
<img src="\assets\images\study\magnetic-robot-lab\2021-08-14-first-paper-review\img5.JPG" width="60%" height="60%">
</center>  

<center>
<span style=
"font-size:70%;
color:gray">
Suspension System에 있는 Magnetic Core의 미소 부피를 표현한 그림
</span>
</center>

<br/>

먼저 해당 내용을 시작하기 전에 Magnetic Core의 좌표계와 Suspension System의 좌표계 사이의 상대 운동은 0이라고 가정을 하고 있다. 왜냐하면 우리는 Magnetic Core로 좌표계를 옮겨야 하는 작업을 해야 하는데, A14식을 보다 시피, 변환하기에는 너무 복잡하다. 즉 연산의 간편함 때문에 이러한 가정을 한다고 명시를 하고 있다.  

먼저 토크를 계산해 보자. Magnetic Core의 미소 부피에 대한 토크의 경우, Core의 체적의 자기 모멘트와 증분 부피에 토크와 힘에 대한 방정식을 합하여 제시가 되고 있다.  

<center>$$\delta \overline{\tilde{\mathbf{T}}} = \delta \overline{\mathbf{T}} + (\overline{\mathbf{r}} \times \delta \overline{\mathbf{F}})$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
(1): 확장 방정식에 따른 증분 부피에서의 토크
</span>
</center>

<br/>

이 때 $ \delta \overline{\mathbf{T}} $ 와  $ \delta \overline{\mathbf{F}} $ 는 해당 위치에서의 자기장에 의한 증분 부피의 토크와 힘이다.  
(1) 식을 $ \overline{\mathbf{T}} $ 에 대해 정리하면 다음과 같이 쓸 수 있고,  

<center>$$\overline{\mathbf{T}} = \int_v \delta \overline{\tilde{\mathbf{T}}} = \int_v [\delta \overline{\mathbf{T}} + (\overline{\mathbf{r}} \times \delta \overline{\mathbf{F}})]$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
(2): (1)식을 bar T에 대해 정리한 식
</span>
</center>

<br/>

그런데 (2)식에서 B20, B21식을 대입하면,

<center>$$\overline{\mathbf{T}} = \int_v (\overline{\mathbf{M}} \times \tilde{\mathbf{B}}) + [\overline{\mathbf{r}} \times (\overline{\mathbf{M}} \cdot \triangledown) \tilde{\mathbf{B}}] \; dv$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
(3): (2)식에 B20, B21 대입한 모습. Core 좌표계에서의 최종 토크 식
</span>
</center>

<br/>

그 다음으로 힘을 구해보면, B21식에서 부피에 대해 적분을 하면 다음과 같이 쓸 수 있다.  

<center>$$\overline{\mathbf{F}} = \int_v (\overline{\mathbf{M}} \cdot \triangledown) \tilde{\mathbf{B}} \; dv$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
(4): B21식을 적분하여 얻은 bar F의 모습
</span>
</center>

<br/>

그런데 다음과 같은 벡터 항등식에 의해 식을 변형할 수 있다.  

<center>$$(A \cdot \triangledown)f(r) = \frac{\partial f(r)}{\partial r}(A \cdot \hat{r})$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
벡터 항등식
</span>
</center>

<br/>

<center>$$(\overline{\mathbf{M}} \cdot \triangledown) \tilde{\mathbf{B}} = [\partial \tilde{\mathbf{B}}] \overline{\mathbf{M}}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
(5): 벡터 항등식을 적용한 모습
</span>
</center>

<br/>

그런데 $ \tilde{\mathbf{B}} $ 에 대해 편미분을 적용했다. 즉, 이차 확장방정식에 대해 편미분을 적용한 것이므로, 그에 대한 성분이 당연히 3 by 3 행렬로 나올 것이다. 또한 $ \overline{\mathbf{M}} $ 은 Magnetic Core의 좌표계에서의 자화벡터를 의미하므로, 각 축마다의 성분들로 나눌 수 있다.  

<center>$$[\partial \tilde{\mathbf{B}}] = \begin{bmatrix}
\tilde{B}_{xx} & \tilde{B}_{xy} & \tilde{B}_{xz} \\ 
\tilde{B}_{yx} & \tilde{B}_{yy} & \tilde{B}_{yz} \\ 
\tilde{B}_{zx} & \tilde{B}_{zy} & \tilde{B}_{zz}
\end{bmatrix}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
(6)
</span>
</center>

<br/>

<center>$$\overline{\mathbf{M}} = \begin{bmatrix}
M_{\overline{x}}\\ 
M_{\overline{y}}\\ 
M_{\overline{z}}
\end{bmatrix}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
(7)
</span>
</center>

<br/>




## 2-2. Magnetization Along Axis of Symmetry

지금까지 6자유도에 대해 설명하기 위한 빌드업은 끝났다. 이제부터 두 방향의 자화벡터를 각각 수식을 풀어서 증명해 볼 것이다. [이전 포스팅](https://sungjun0204.github.io/magnetic%20robot%20laboratory/first-paper-review/#1-paper-information)에서 논문의 주제를 말한 것처럼, Magnetic Core의 대칭축과 수직한 축에 자화벡터를 거는 것이 어떻게 차이가 나길래 자유도가 1개 더 늘어나는지 증명을 할 것이다. 지금부터 수식이 많이 나오므로 집중해서 따라오기 바란다.  

먼저 대칭축을 따라 자화벡터를 적용한 경우이다. 대칭축에 대해서만 가한 경우이므로, $ M_{\overline{x}} $ 에 대해서만 식이 유효해진다. 따라서 식 (5)는 다음과 같이 계산이 된다.  

<center>$$[\partial \tilde{\mathbf{B}}] \overline{\mathbf{M}} = \begin{bmatrix}
\tilde{B}_{xx} & \tilde{B}_{xy} & \tilde{B}_{xz} \\ 
\tilde{B}_{yx} & \tilde{B}_{yy} & \tilde{B}_{yz} \\ 
\tilde{B}_{zx} & \tilde{B}_{zy} & \tilde{B}_{zz}
\end{bmatrix} 
\begin{bmatrix}
M_{\overline{x}}\\ 
M_{\overline{y}}\\ 
M_{\overline{z}}
\end{bmatrix}$$</center>

<center>$$= \begin{bmatrix}
\tilde{B}_{xx} M_{\overline{x}} + \tilde{B}_{xy} M_{\overline{y}} + \tilde{B}_{xz} M_{\overline{z}}\\ 
\tilde{B}_{yx} M_{\overline{x}} + \tilde{B}_{yy} M_{\overline{y}} + \tilde{B}_{yz} M_{\overline{z}}\\ 
\tilde{B}_{zx} M_{\overline{x}} + \tilde{B}_{zy} M_{\overline{y}} + \tilde{B}_{zz} M_{\overline{z}}
\end{bmatrix}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
식 (5)를 식 (6), (7)을 토대로 계산한 모습
</span>
</center>

<br/>

그런데 앞서 설명했듯이 대칭축을 따라 자화를 걸었으므로 $ M_{\overline{x}} $ 를 제외하고 나머지는 다 0이다. 따라서 다음과 같이 계산된다.  

<center>$$[\partial \tilde{\mathbf{B}}] \overline{\mathbf{M}} = M_{\overline{x}}\begin{bmatrix}
\tilde{B}_{xx}\\ 
\tilde{B}_{xy}\\ 
\tilde{B}_{xz}
\end{bmatrix}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
(8): 식 (5)에서 대칭축에 대해서만 자화를 한 모습. B의 원소들의 첨자의 경우, x에 대해 정리한다. 이는 편미분 표시인데, 우리는 불규칙하지 않은, 연속적인 자기장을 다루고 있으므로 바꿔도 상관없다. 
</span>
</center>

<br/>

이렇게 계산한 식 (8)을 토크와 힘 수식에 대입해서 풀어보자.  
먼저 토크 수식 (3)을 풀어보자. 식 (8)은 식 (5)와 같고, 식 (3)을 보면 두번째 항에서 식 (8)이 계산되므로 식 (3)을 다음과 같이 풀 수 있다.  

<center>$$\overline{\mathbf{r}} \times (\overline{\mathbf{M}} \cdot \triangledown) \tilde{\mathbf{B}} = \overline{\mathbf{r}} \times [\partial \tilde{\mathbf{B}}] \overline{\mathbf{M}}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
식 (3)에 식 (8)이 있으므로 대입해 계산해본다.
</span>
</center>

<br/>

<center>$$= M_{\overline{x}} \begin{bmatrix}
\overline{x} \\ 
\overline{y} \\ 
\overline{z} 
\end{bmatrix} \times \begin{bmatrix}
\tilde{B}_{xx} \\ 
\tilde{B}_{xy} \\ 
\tilde{B}_{xz} 
\end{bmatrix}
= M_{\overline{x}} \begin{bmatrix}
i & j & k \\ 
\overline{x} & \overline{y} & \overline{z} \\ 
\tilde{B}_{xx} & \tilde{B}_{xy} & \tilde{B}_{xz}
\end{bmatrix}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
외적 계산이므로 그 꼴로 바꿔 계산한다. 
</span>
</center>

<br/>

<center>$$= M_{\overline{x}}\begin{bmatrix}
(-\tilde{B}_{xy} \overline{z} + \tilde{B}_{xz} \overline{y})\\ 
(\tilde{B}_{xx} \overline{z} - \tilde{B}_{xz} \overline{x})\\ 
(-\tilde{B}_{xx} \overline{y} + \tilde{B}_{xy} \overline{x})
\end{bmatrix}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
(9): 토크의 두번째 항 최종 계산 모습
</span>
</center>

<br/>

그리고 식 (3)의 첫번째 항도 똑같은 방법으로 계산이 가능하다. 

<center>$$\overline{\mathbf{M}} \times \tilde{\mathbf{B}} = \begin{bmatrix}
M_{\overline{x}}\\ 
M_{\overline{y}}\\ 
M_{\overline{z}}
\end{bmatrix} \times 
\begin{bmatrix}
\tilde{B}_{x}\\ 
\tilde{B}_{y}\\ 
\tilde{B}_{z}
\end{bmatrix}$$</center>

<center>$$= \begin{bmatrix}
i & j & k \\ 
M_{\overline{x}} & M_{\overline{y}} & M_{\overline{z}} \\ 
\tilde{B}_{x} & \tilde{B}_{y} & \tilde{B}_{z}
\end{bmatrix} = 
\begin{bmatrix}
(M_{\overline{y}} \tilde{B}_{z} - M_{\overline{z}} \tilde{B}_{y})\\ 
-(M_{\overline{x}} \tilde{B}_{z} - M_{\overline{z}} \tilde{B}_{x})\\ 
(M_{\overline{x}} \tilde{B}_{y} - M_{\overline{y}} \tilde{B}_{x})
\end{bmatrix}$$</center>

<center>$$\therefore \; M_{\overline{x}}\begin{bmatrix}
0 \\ 
- \tilde{B}_z\\ 
\tilde{B}_y
\end{bmatrix}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
(10): 토크의 첫번째 항 최종 계산 모습 
</span>
</center>

<br/>

따라서 식 (3)의 최종 모습은 다음과 같다. 

<center>$$\overline{\mathbf{T}} = \int_v (\overline{\mathbf{M}} \times \tilde{\mathbf{B}}) + [\overline{\mathbf{r}} \times (\overline{\mathbf{M}} \cdot \triangledown) \tilde{\mathbf{B}}] \; dv$$</center>

<center>$$ = \overline{\mathbf{T}} = \int_v M_{\overline{x}}\begin{bmatrix}
0 \\ 
- \tilde{B}_z\\ 
\tilde{B}_y
\end{bmatrix} + M_{\overline{x}}\begin{bmatrix}
(-\tilde{B}_{xy} \overline{z} + \tilde{B}_{xz} \overline{y})\\ 
(\tilde{B}_{xx} \overline{z} - \tilde{B}_{xz} \overline{x})\\ 
(-\tilde{B}_{xx} \overline{y} + \tilde{B}_{xy} \overline{x})
\end{bmatrix} \; dv$$</center>

<br/>

<center>$$T_{\overline{x}} = 0 + M_{\overline{x}} \int (-\tilde{B}_{xy} \overline{z} + \tilde{B}_{xz} \overline{y}) \; dv$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
(11): x축에 대한 토크 
</span>
</center>

<br/>

<center>$$T_{\overline{y}} = -M_{\overline{x}} \int \tilde{B}_z \; dv + M_{\overline{x}} \int (\tilde{B}_{xx} \overline{z} - \tilde{B}_{xz} \overline{x}) \; dv$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
(12): y축에 대한 토크 
</span>
</center>

<br/>

<center>$$T_{\overline{z}} = M_{\overline{x}} \int \tilde{B}_y \; dv + M_{\overline{x}} \int (-\tilde{B}_{xx} \overline{y} + \tilde{B}_{xy} \overline{x}) \; dv$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
(13): z축에 대한 토크 
</span>
</center>

<br/><br/>

이제 식 (11)~(13)을 하나하나 풀어보자.  
먼저 식 (11)에서 $ \int \tilde{B}_{xz} \overline{y} \; dv $ 를 풀어보자. 이는 [이전 포스팅](https://sungjun0204.github.io/magnetic%20robot%20laboratory/first-paper-review/#3-2-expansion-of-the-field-b-by-talor-series)의 A9식에서 설명한 일차 구배 방정식에 의해 다음과 같이 풀 수 있다.  

<center>$$\tilde{\mathbf{B}}_{ij} = \mathbf{B}_{ij} + \frac{\partial (\partial \mathbf{B}_i / \partial j)}{\partial \mathbf{r}} \mathbf{r}$$  
</center>

<center>
<span style=
"font-size:80%;
color:gray">
식 A9
</span>
</center>  

<br/>

<center>$$\tilde{\mathbf{B}}_{xz} = B_{xz} + \frac{\partial}{\partial \mathbf{r}} \frac{\partial B_x}{\partial z} \mathbf{r}$$</center>

<center>$$= \tilde{\mathbf{B}}_{xz} = B_{xz} + \frac{\partial}{\partial x} \frac{\partial B_x}{\partial z} x + \frac{\partial}{\partial y} \frac{\partial B_x}{\partial z} y + \frac{\partial}{\partial z} \frac{\partial B_x}{\partial z} z$$</center>

<center>$$= B_{xz} + B_{(xx)z}x + B_{(xy)z}y + B_{(xz)z}z$$</center>

<br/>

<center>$$\therefore \int \tilde{B}_{xz} \overline{y} \; dv = \\ B_{xz} \int_v \overline{y} \; dv + B_{(xx)z} \int_v \overline{xy} \; dv + B_{(xy)z} \int_v \overline{y}^2 \; dv + B_{(xz)z} \int_v \overline{zy} \; dv$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
(14): (11)의 일부 항을 A9식을 이용해 정리한 모습
</span>
</center>  

<br/>

그리고 계속 나오는 적분 계산은 Magnetic Core에 대한 부피에 대해 적분을 하고 있으므로 체적 계산을 진행해본다. 그런데 네 개의 항 중에서 $ \overline{y}^2 $ 가 있는 항을 제외하고는 전부 1차 항이기에 계산하면 0이 나온다. 따라서, 

<center>$$\int _v \overline{y}^2 \; dv = \int_{-l/2}^{l/2} \int_{-a}^{a} \int_{-\sqrt{a^2 - \overline{z}^2}}^{\sqrt{a^2 - \overline{z}^2}} \overline{y}^2 \; d\overline{y} \; d\overline{z} \; d\overline{x}$$</center>

<center>$$= (a^4 / 4) \pi l$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
(15): 식 (14)에서 적분 계산을 한 모습. 원기둥 체적 계산을 했다. 
</span>
</center>  

<br/>

그런데 여기서 $ \pi l $ 은 부피가 되므로, 부피를 $ v $ 라고 하면, 

<center>$$= (a^4 / 4) v$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
(16): 식 (15)에서 πl을 v로 치환한 모습
</span>
</center>  

<br/>

따라서 $ \int \tilde{B}_{xz} \overline{y} \; dv $ 는 다음과 같이 계산된다. 

<center>$$= (a^4 / 4) v B_{(xy)z}$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
(17): 식 (11)의 일부 항 계산 결과
</span>
</center>  

<br/>

이런 식으로 똑같이 전부 계산해 주면 다음과 같이 결과가 나온다. (전부 A9 식에 의해 전개한 다음 체적분 계산하면 된다. 사실상 적분 노가다라 여기에 모든 계산 과정을 적지는 않겠다. )  

<center>$$T_{\overline{x}} = 0$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
(25): 식 (11) 전개 결과
</span>
</center>  

<br/>

<center>$$T_{\overline{y}} = -vM_{\overline{x}}B_{z} - vM_{\overline{x}}[(a^2 / 4) - (l^2 / 8)] B_{(xx)z}$$</center>

<center>$$- vM_{\overline{x}}(a^2 / 8) (B_{(yy)z} + B_{(zz)z})$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
(26): 식 (12) 전개 결과
</span>
</center>  

<br/>

<center>$$T_{\overline{z}} = -vM_{\overline{x}}B_{y} - vM_{\overline{x}}[(l^2 / 8) - (a^2 / 4)] B_{(xx)y}$$</center>

<center>$$- vM_{\overline{x}}(a^2 / 8) (B_{(yy)y} + B_{(yz)z})$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
(27): 식 (13) 전개 결과
</span>
</center>  

<br/>

드디어 나왔다. 왜 대칭축을 따라 자화벡터를 걸게 되면 5자유도밖에 되지 않는지 말이다. 식 (25)를 보면 결국 x축에 대한 토크가 0이 되는 것을 수식적으로 알 수 있다. 그럼 각 축의 토크 말고 힘은 어떻게 되는 걸까? 식 (4)는 결국 식 (8) 형태로 바꿀 수 있으므로 식 (8)을 다음과 같이 각 축에 대해서 쪼갤 수 있다.  

<center>$$F_{\overline{x}} = M_{\overline{x}} \int_v \tilde{B}_{xx} \; dv$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
(28): 식 (8)의 x축 성분 계산 결과
</span>
</center>  

<br/>

<center>$$F_{\overline{y}} = M_{\overline{x}} \int_v \tilde{B}_{xy} \; dv$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
(29): 식 (8)의 y축 성분 계산 결과
</span>
</center>  

<br/>

<center>$$F_{\overline{z}} = M_{\overline{x}} \int_v \tilde{B}_{xz} \; dv$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
(30): 식 (8)의 z축 성분 계산 결과
</span>
</center>  

<br/>

(28)~(30)의 계산은 앞서 토크를 계산한 것 처럼 체적분 계산을 하면 된다. 따라서 다음과 같이 계산이 된다. 

<center>$$F_{\overline{x}} = vM_{\overline{x}} B_{xx}$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
(32): 식 (28)의 최종 결과
</span>
</center>  

<br/>

<center>$$F_{\overline{y}} = vM_{\overline{x}} B_{xy}$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
(33): 식 (29)의 최종 결과
</span>
</center>  

<br/>

<center>$$F_{\overline{z}} = vM_{\overline{x}} B_{xz}$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
(34): 식 (30)의 최종 결과
</span>
</center>  

<br/>

## 2-3. Magnetization Perpendicular to Axis of Symmetry

자, 이번에는 Magnetic Core에 수직한 방향, z축 방향으로 자화를 걸어보자.  
계산은 2-2절에서 한 계산과 동일하다. 식 (5)에서 이번에는 z축을 제외한 나머지 축에 대한 성분은 모두 0이기에 다음과 같이 남게 된다.   

<center>$$[\partial \tilde{\mathbf{B}}] \overline{\mathbf{M}} = M_{\overline{x}}\begin{bmatrix}
\tilde{B}_{xz}\\ 
\tilde{B}_{xz}\\ 
\tilde{B}_{zz}
\end{bmatrix}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
(35): 식 (5)에서 수직축에 대해서만 자화를 한 모습. 
</span>
</center>

<br/>

따라서 다시 토크에 대해서 계산을 하게 되면, 다음과 같다.  

<center>$$\overline{\mathbf{r}} \times (\overline{\mathbf{M}} \cdot \triangledown) \tilde{\mathbf{B}} = M_{\overline{z}}\begin{bmatrix}
(-\tilde{B}_{yz} \overline{z} + \tilde{B}_{zz} \overline{y})\\ 
(\tilde{B}_{xz} \overline{z} - \tilde{B}_{zz} \overline{x})\\ 
(-\tilde{B}_{xz} \overline{y} + \tilde{B}_{yz} \overline{x})
\end{bmatrix}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
(36): 토크의 두번째 항 최종 계산 모습
</span>
</center>

<br/>
<center>$$\overline{\mathbf{M}} \times \tilde{\mathbf{B}} = M_{\overline{x}}\begin{bmatrix}
- \tilde{B}_y \\ 
\tilde{B}_x\\ 
0
\end{bmatrix}$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
(36): 토크의 첫번째 항 최종 계산 모습
</span>
</center>

<br/>

따라서 이렇게 전개된 토크 식을 각 축에 대해 분리하면,  

<center>$$T_{\overline{x}} = -M_{\overline{z}} \int \tilde{B}_y \; dv + M_{\overline{z}} \int (\tilde{B}_{zz} \overline{y} - \tilde{B}_{yz} \overline{z}) \; dv$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
(38): x축에 대한 토크 
</span>
</center>

<br/>

<center>$$T_{\overline{y}} = M_{\overline{z}} \int \tilde{B}_x \; dv + M_{\overline{z}} \int (\tilde{B}_{xz} \overline{z} - \tilde{B}_{zz} \overline{x}) \; dv$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
(39): y축에 대한 토크 
</span>
</center>

<br/>

<center>$$T_{\overline{z}} = 0 + M_{\overline{z}} \int (\tilde{B}_{yz} \overline{x} - \tilde{B}_{xz} \overline{y}) \; dv$$</center>

<center>
<span style=
"font-size:70%;
color:gray">
(40): z축에 대한 토크 
</span>
</center>

<br/>

이후로 2-2절에서 했던 것처럼 A9식 이용하여 전개 후 체적분 계산하면 토크와 힘에 대한 식은 다음과 같이 된다. 

<center>$$T_{\overline{x}} = -vM_{\overline{z}}B_{y} - vM_{\overline{z}}(l^2 / 24)B_{(xx)y}$$</center>

<center>$$- vM_{\overline{z}}(a^2 / 8) (B_{(yy)y} + B_{(yz)z})$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
(41): 식 (38) 전개 결과
</span>
</center>  

<br/>

<center>$$T_{\overline{y}} = -vM_{\overline{z}}B_{x} - vM_{\overline{z}}[(3a^2 / 8) - (l^2 / 12)] B_{(xz)z}$$</center>

<center>$$+ vM_{\overline{z}}(l^2 / 24)B_{(xx)x} + vM_{\overline{z}}(a^2 / 8)B_{(xy)y}$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
(42): 식 (39) 전개 결과
</span>
</center>  

<br/>

<center>$$T_{\overline{z}} = vM_{\overline{z}}[(l^2 / 12) - (a^2 / 4)] B_{(xy)z}$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
(43): 식 (40) 전개 결과
</span>
</center>  

<br/>

드디어 나왔다...! 자화 방향을 대칭축이 아닌 수직한 방향으로 하니까 모든 축에 대한 회전력이 0이 아니라는 것이 수식적으로 증명했다.  
아, 물론 같은 방식으로 힘에 대한 수식도 다음과 같이 계산 가능하다.  

<center>$$F_{\overline{x}} = M_{\overline{z}} \int_v \tilde{B}_{xz} \; dv = vM_{\overline{z}} B_{xz}$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
(44): x축에 대한 식 (35) 계산 결과
</span>
</center>  

<br/>

<center>$$F_{\overline{y}} = M_{\overline{z}} \int_v \tilde{B}_{yz} \; dv = vM_{\overline{z}} B_{yz}$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
(45): y축에 대한 식 (35) 계산 결과
</span>
</center>  

<br/>

<center>$$F_{\overline{z}} = M_{\overline{z}} \int_v \tilde{B}_{zz} \; dv = vM_{\overline{z}} B_{zz}$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
(46): z축에 대한 식 (35) 계산 결과
</span>
</center>  

<br/><br/><br/>


















# 3. Conclusion

크게 두 가지로 정리를 할 수 있다. 

1. 최종 계산한 토크와 힘 간의 연관성이 없다.  
실제로 토크에 관한 식 (41)~(43)과 힘에 대한 식 (44)~(46)을 보면 서로의 수식이 다 독립적인 것을 알 수 있다.


2. 자화를 대칭축에 평행하게 걸었을 때 고차항들이 소거되어 x축 성분이 0이 되는 것을 볼 수 있었으나, 자화를 대칭죽에 수직하게 걸었을 때는 고차항이 남아있어 모든 축에 대한 토크가 존재한다는 것을 확인할 수 있다.  



<br/><br/>

