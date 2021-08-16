---
title: "[Magnetic Robot Lab] 2. Paper Review (1)"
excerpt: "Title: Expanded Equations for Torque and Force on a Cylindrical Permanent Magnet Core in a Large-Gap Magnetic Suspension System"
header: 
    teaser: \assets\images\me.png

categories: 
    - Magnetic Robot Laboratory
tage: 
    - magnetic robot lab
last_modified_at: 2021-07-08t12:58-15:00
comments: true
toc: true
toc_sticky: true
use_math: true
---

<br/><br/>

>앞으로 내가 해당 랩실에서 구현할 시스템의 이론적 근본이 되는 논문에 대한 리뷰이다. 코일로 구성된 자기장 생성 시스템에서의 자석 로봇의 움직임 제어(x, y, z, roll, pitch, yaw)에 대해 수식적으로 가능하다는 것을 논하고 있다. 자석 로봇을 제어하기 위한 시스템의 매우매우 기초적인 내용이라 결과만 알고 있어도 문제될 것은 없지만, 잘 알아두면 좋을 것이다.  

<br/><br/>

# 1. Paper Information

이번에 리뷰할 논문의 정보는 다음과 같다. 

* 제목: Expanded Equations for Torque and Force on a Cylindrical Permanent Magnet Core in a Large-Gap Magnetic Suspension System  
* 저자: Nelson J. Groom (NASA)
* 날짜: 1997.02  

* 주제: 기존 자기장 발생 시스템에서는 로봇을 5자유도(x, y, z, pitch, yaw)으로만 움직일 수 있었으나, 자기장 식을 테일러 급수를 통해 2차까지 확장하여 사용하게 되면 6자유도(x, y, z, roll, pitch, yaw), 즉 모든 방향으로 제어가 가능하다고 말하고 있다. 

<br/><br/><br/>

# 2. Introduction
해당 논문에서는 제어할 자석 로봇을 "Cylindrical Permanent Magnet Core(원통형 영구자석 코어)"라고 부르고, 해당 자석을 움직이게 할 장소(field)를 "Large-Gap Magnetic Suspension System"(결국 커다란 코일을 의미한다)이라고 부르고 있다. 결국 커다란 코일 안에 자석 로봇을 넣어 로봇을 움직이게 하는 것인데, 이를 일반화하기 위해 이런 식으로 말하는 것 같다. 자석 로봇도 단순히 "자석 코어"라고 말하고 있는데, 아마 일정하게 자화가 된다고 가정을 하므로 단순한 원통형 자석을 기준으로 설명을 하는 것 같다.  

<center>
<img src="\assets\images\study\magnetic-robot-lab\2021-08-14-first-paper-review\img2.jpg" width="50%" height="50%">
</center>  

<center>
<span style=
"font-size:70%;
color:gray">
Source: https://kr.misumi-ec.com/vona2/detail/110300263570/
</span>
</center>

<br/>

<center>
<img src="\assets\images\study\magnetic-robot-lab\2021-08-14-first-paper-review\img1.JPG" width="70%" height="70%">
</center>  

<center>
<span style=
"font-size:70%;
color:gray">
논문에 언급하는 Cylindrical Permanent Magnet Core의 좌표계이다. 본문에서는 x축이 대칭축(Symmetry Axis)이며, z축이 수직축(Perpendicular Axis)이라고 설명한다. 
</span>
</center>

<br/>

해당 논문처럼 Magnetic Suspension System에서 Magnetic Core의 움직임을 제어하기 위한 논문이 여러 편 있으나, 살펴보면 전부 X축에 대한 회전(X축에 대한 토크( $T_x$ ), Roll)은 불가능한 상태의 5자유도에 대한 내용이다. 해당 논문에서는 이러한 내용을 reference 1~6으로 적어두었다.  물론 다른 방법으로 6자유도 제어가 가능하도록 연구를 한 논문도 있다. Reference 4, 7이 그러한 내용이긴 하나, 대신 코어의 모양을 바꾸거아 균일하지 않은 3차원 자화를 이용하는 방법이라 일반적이지 않다는 단점이 있다. 그러나 해당 논문에서는 테일러 급수를 이용하여 Cylindrical Permanent Magnet Core의 확장방정식을 확인하고 대칭축에 수직으로 일정한 자화 벡터를 발생시킬 경우 6자유도로 움직일 수 있다는 것을 밝히고 있다.  

그런데 논문을 읽기 전에 본 Introdiction에서 언급하는 자기장의 "확장 방정식" 형태와 해당 Magnetic Core에 걸리는 힘과 토크에 대한 수식을 이해할 필요가 있다. 이를 위해 논문 뒤쪽에 Appendix A, B를 각각 남겨 두었다. 우리는 해당 논문을 이해하기 위해 Appendix먼저 읽어 볼 것이다.  

<br/><br/><br/>

# 3. Appendix A
: Expansion of Fields and Gradients About The Nomial Operating Point of a Cylindrical Permanent Magnet Core
(Cylindrical Permanent Magnet Core의 통칭 작용점에 대한 자기장과 구배의 확장 방정식)  

해당 부록에서는 테일러 급수를 이용해 자기장과 구배의 확장을 전개를 설명하게 된다. 테일러 급수를 전개해야 하므로 해당 논문에서는 자기장이 적절히 2차 이상 전개된다 가정하고 시작한다.  

<br/>

## 3-1. Transformation of Frame

<br/>

먼저 좌표계에 대한 얘기 먼저 나오는데, 다음의 식을 먼저 보자.  

<center>$$\begin{bmatrix}\overline{x}\\ \overline{y}\\ \overline{z}\\ \end{bmatrix}=[\mathbf{T}_m]\begin{bmatrix}x\\ y\\ z\\ \end{bmatrix}$$</center>  

<center>
<span style=
"font-size:80%;
color:gray">
A1: 좌표계 이동에 관한 수식
</span>
</center>  

<br/>

여기서 $[x, y, z]$는 자기장 시스템에 고정되어 있는 "관성좌표계(Inertial Frame)"이고, $[\overline{x}, \overline{y}, \overline{z}]$는 영구 자석 코어에 고정되어 있는 "고정좌표계(Body Frame)"로 설명하고 있다. 보통 고정좌표계는 해당 물체의 움직임을 직접적으로 알기 쉽고, 관성좌표계는 해당 물체가 속해 있는 공간을 기준으로 바라보는 것으로 생각할 수 있으므로 이렇게 정한 것 같다.  
그럼 왜 좌표계를 다르게 쓸까? 우리가 결국 알고 싶은 것은 "코일이 발생시키는 자기장"이 아닌, "자석 로봇의 자기장", 자석 로봇 그 자체가 어떻게 움직이는지를 알고 싶은 것이다. 따라서 해당 Magnetic Core에 고정되어 있는 고정좌표계로 이동을 하여 생각을 해야 한다. 따라서 고정좌표계로 이동하기 위해서 $\mathbf{T}_m$이라는 행렬을 곱하게 되며, 이는 Euler Angle Convention 을 이용해 X축 -> Y축 -> Z축 순서로 회전을 한 회전행렬이다.  

<center>$$R_x R_y R_z (\theta_z, \theta_y, \theta_x) = I_3 R_x(\theta_z) R_y(\theta_y) R_z(\theta_x)$$</center>
<center>$$=\begin{bmatrix}1 & 0 & 0\\ 0 & 1 & 0\\ 0 & 0 & 1\end{bmatrix} \begin{bmatrix}1 & 0 & 0\\ 0 & cos \theta_x & -sin \theta_x \\ 0 & sin \theta_x & cos \theta_x\end{bmatrix} \begin{bmatrix}cos \theta_y & 0 & sin \theta_y\\ 0 & 1 & 0\\ -sin \theta_y & 0 & cod \theta_y\end{bmatrix} \begin{bmatrix}cos \theta_z & -sin \theta_z & 0\\ sin \theta_z & cos \theta_z & 0\\ 0 & 0 & 1\end{bmatrix}$$</center>
<center>$$\therefore \begin{bmatrix}c\theta_z c\theta_y & \ -s\theta_z c\theta_y & s\theta_y\\ c\theta_z s\theta_y s\theta_x + s\theta_z c\theta_x & c\theta_x c\theta_z - s\theta_x s\theta_y s\theta_z & - c\theta_y s\theta_x \\ s\theta_x c\theta_z - c\theta_x c\theta_z s\theta_y & s\theta_z s\theta_y c\theta_x + c\theta_z s\theta_x & c\theta_y c\theta_x \end{bmatrix}$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
A2: 관성에서 고정 좌표계로 이동하기 위한 회전행렬  
</span>
</center>  

<br/>

참고로 논문에 적힌 A2에 오타가 있다. 위 식은 내가 직접 계산한 행렬식인데, 어려울 것도 없고 그냥 단순 행렬 곱 계산이다. 그리고 논문에서는 sin, cos을 간편하게 s, c로 줄여 쓰는데, 여기 포스팅에서도 동일하게 표기하겠다. 어쨌든 이게 중요한 건 아니니까 바로 다음 단계로 넘어가자. 

<br/>

## 3-2. Expansion of The Field B by Talor Series

그럼 다음으로 확장 방정식을 계산해 보자.  
자기장 $\mathbf{B}$ 와 $\mathbf{B}$ 에서의 구배(Gradient)는 Suspension System(커다란 코일)에 의해 생성이 되며, 따라서 $ \mathbf{r} = [x, y, z] $ 에 대해 정의가 된다. 테일러 급수를 이용하여 전개한 식을 $ \tilde{\mathbf{B}} $ 라고 하면, 결과는 다음과 같다. 

<center>$$\tilde{\mathbf{B}} = \mathbf{B} + \mathbf{B}' + (1/2)\mathbf{B}''$$</center>

<br/>

그런데 미분하는 대상이 자기장 $ \mathbf{B} $  이다. 자기장은 벡터인데, 즉 벡터를 미분하고 있다. 이는 즉 단위 부피당 자기장의 흐름을 의미하므로, 이는 Divergence를 의미하기에 $ \mathbf{B}' = \frac{\partial \mathbf{B}}{\partial \mathbf{r}} = (\mathbf{r} \cdot \triangledown) \mathbf{B} $ 이므로, 다음과 같이 쓸 수 있다.  

<center>$$\tilde{\mathbf{B}} = \mathbf{B} + (\mathbf{r} \cdot \bigtriangledown)\mathbf{B} + (1/2)(\mathbf{r} \cdot \bigtriangledown)^2 \mathbf{B}$$</center>  

<center>
<span style=
"font-size:80%;
color:gray">
A3: 자기장 B를 테일러 급수로 2차까지 전개한 모습 
</span>
</center>  

<br/>

그리고 A3식을 벡터 항등식에 의해 다음과 같이 쓸 수 있다. 

<center>$$\tilde{\mathbf{B}}=\mathbf{B}_i+\frac{\partial \mathbf{B}_i}{\partial \mathbf{r}} \mathbf{r} + (1/2) \mathbf{r}^T \frac{\partial^2 \mathbf{B}_i}{\partial \mathbf{r}^2}\mathbf{r}$$</center>  

<center>
<span style=
"font-size:80%;
color:gray">
A4: A3 식을 다른 표현으로 바꾼 모습. 벡터 항등식이라고 해서 특별한 게 아니라 벡터 공식에 의해 다른 표현으로 정리한 것이다.
</span>
</center>  

<br/>

이때, 자기장 $ \mathbf{B} $ 는 $ [x, y, z] $ 성분으로 나눌 수 있으므로, $ \frac{\partial \mathbf{B}_i}{\partial \mathbf{r}} $ 도 마찬가지로 세 성분으로 나뉜다.  

<center>$$\frac{\partial \mathbf{B}_i}{\partial \mathbf{r}} = \left [ \frac{\partial \mathbf{B}_i}{\partial x} \; \frac{\partial \mathbf{B}_i}{\partial y} \; \frac{\partial \mathbf{B}_i}{\partial z} \right ]$$</center>  

<center>
<span style=
"font-size:80%;
color:gray">
A5: 자기장 B를 위치벡터 r에 대해 편미분 한 것을 다시 각 축에 대해서 분해한 수식
</span>
</center>  

<br/>

마찬가지로 두 번 편미분한 $ \frac{\partial^2 \mathbf{B}_i}{\partial \mathbf{r}^2} $ 도 각 성분별로 나눌 수 있다. 그런데 $ \frac{\partial^2 \mathbf{B}_i}{\partial \mathbf{r}^2} $ 는 $ \frac{\partial \mathbf{B}_i}{\partial \mathbf{r}} $ 를 한 번 더 편미분을 한 것이므로, 3 by 3 행렬로 표현될 것이다.  

<center>$$\frac{\partial^2 \mathbf{B}_i}{\partial \mathbf{r}^2} = \begin{bmatrix}
\frac{\partial(\partial \mathbf{B}_i / \partial x)}{\partial x} & \frac{\partial(\partial \mathbf{B}_i / \partial x)}{\partial y} & \frac{\partial(\partial \mathbf{B}_i / \partial x)}{\partial z} \\ 
\frac{\partial(\partial \mathbf{B}_i / \partial y)}{\partial x} & \frac{\partial(\partial \mathbf{B}_i / \partial y)}{\partial y} & \frac{\partial(\partial \mathbf{B}_i / \partial y)}{\partial z} \\ 
\frac{\partial(\partial \mathbf{B}_i / \partial z)}{\partial x} & \frac{\partial(\partial \mathbf{B}_i / \partial z)}{\partial y} & \frac{\partial(\partial \mathbf{B}_i / \partial z)}{\partial z}
\end{bmatrix}$$</center>  

<center>
<span style=
"font-size:80%;
color:gray">
A6: A5를 미분한 것을 다시 각 축에 대해서 분해한 수식
</span>
</center>  

<br/>

그런데 매번 이렇게 적기에는 힘드므로, 논문에서는 $ f_{ij} = \partial f_i / \partial j $, $ f_{(ij)k} = \partial(\partial f_i / \partial j) / \partial k $ 로 일반적인 형태로 바꿔 쓰는데, 다음과 같다.  

<center>$$\frac{\partial \mathbf{B}_i}{\partial \mathbf{r}} = \begin{bmatrix}
\mathbf{B}_{ix} & \mathbf{B}_{iy} & \mathbf{B}_{iz}
\end{bmatrix}$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
A7: A5를 일반화한 식
</span>
</center>  

<br/>

<center>$$\frac{\partial^2 \mathbf{B}_i}{\partial \mathbf{r}^2} = \begin{bmatrix}
\mathbf{B}_{(ix)x} & \mathbf{B}_{(ix)y} & \mathbf{B}_{(ix)z} \\ 
\mathbf{B}_{(iy)x} & \mathbf{B}_{(iy)y} & \mathbf{B}_{(iy)z} \\ 
\mathbf{B}_{(iz)x} & \mathbf{B}_{(iz)y} & \mathbf{B}_{(iz)z}
\end{bmatrix}$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
A8: A6를 일반화한 식
</span>
</center>  

<br/>

최종적으로 A8식은 다음과 같이 더 간단히 표현이 가능하다. 

<center>$$\frac{\partial^2 \mathbf{B}_i}{\partial \mathbf{r}^2} = \frac{\partial (\partial \mathbf{B}_i / \partial j)}{\partial \mathbf{r}} = \begin{bmatrix}
\mathbf{B}_{(ij)x} & \mathbf{B}_{(ij)y} & \mathbf{B}_{(ij)z}
\end{bmatrix}$$  
</center>

<center>
<span style=
"font-size:80%;
color:gray">
A10: A8 식을 더 간략화한 수식
</span>
</center>  

<br/>

따라서 $ \tilde{\mathbf{B}} $ 의 일차 구배 방정식은 다음과 같이 표현된다.  

<center>$$\tilde{\mathbf{B}}_{ij} = \mathbf{B}_{ij} + \frac{\partial (\partial \mathbf{B}_i / \partial j)}{\partial \mathbf{r}} \mathbf{r}$$  
</center>

<center>
<span style=
"font-size:80%;
color:gray">
A9: 자기장의 일차 구배(Gradient)방정식
</span>
</center>  

<br/>

## 3-3. Expansion Equation on The Body Frame
이제 확장 방정식을 Magnet Core의 고정 좌표계로 옮겨보면 다음과 같다.  

<center>$$\overline{\tilde{\mathbf{B}}} = \overline{\mathbf{B}} + (\overline{\mathbf{r}} \cdot \overline{\triangledown}) \overline{\mathbf{B}} + (1/2) (\overline{\mathbf{r}} \cdot \overline{\triangledown})^2 \overline{\mathbf{B}}$$  
</center>

<center>
<span style=
"font-size:80%;
color:gray">
A11: 고정좌표계에서의 확장방정식
</span>
</center>  

<br/>

그런데 A1에서와 같이 $ \mathbf{r} $ 에 $ \mathbf{T}_m $ 을 곱해주면 $ \overline{\mathbf{r}} $ 이 되는 것을 먼저 정의하였다. 따라서 A11식도 마찬가지로 다음과 같이 생각할 수 있다.  

<center>$$\overline{\mathbf{B}} = [\mathbf{T}_m] \mathbf{B}$$</center>
<center>$$\overline{\mathbf{\triangledown}} = [\mathbf{T}_m] \mathbf{\triangledown}$$</center>

<br/>

그리고 $ \overline{\mathbf{r}} = [\mathbf{T}_m] \mathbf{r} $ 에서 반대로 $ \mathbf{r} $ 를 구하려면 다음과 같이 쓸 수 있다.  

<center>$$\mathbf{r} = [\mathbf{T}_m]^T \overline{\mathbf{r}}$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
A12: A1에서 r을 유도하는 수식
</span>
</center>  

<br/>

따라서 A12식에 의해 A4식을 다시 쓰면,  

<center>$$\tilde{\mathbf{B}}_i = \mathbf{B}_i + \frac{\partial \mathbf{B}_i}{\partial \mathbf{r}} [\mathbf{T}_m]^T \overline{\mathbf{r}} + (1/2) \overline{\mathbf{r}}^T [\mathbf{T}_m] \frac{\partial^2 \mathbf{B}_i}{\partial \mathbf{r}^2} [\mathbf{T}_m]^T \overline{\mathbf{r}}$$</center>  

<center>
<span style=
"font-size:80%;
color:gray">
A13: A4식에 A12를 대입한 모습
</span>
</center>  

<br/>

이는 고정좌표계(Magnetic Core)에서의 자기장 성분을 관성좌표계(Suspension System)로 확장할 수 있음을 보여준다. 즉 해당 확장방정식이 수식적으로 시스템에 온전히 적용이 된다는 것을 의미한다. 따라서 A13식에 $ \mathbf{T}_m $ 을 곱해주면 고정좌표계(Magnetic Core)에서의 확장방정식이 완성된다.  

<center>$$\overline{\tilde{\mathbf{B}}} = [\mathbf{T}_m] \begin{bmatrix}
[\mathbf{B}_x + \frac{\partial \mathbf{B}_x}{\partial \mathbf{r}} [\mathbf{T}_m]^T \overline{\mathbf{r}} + (1/2) \overline{\mathbf{r}}^T [\mathbf{T}_m] \frac{\partial^2 \mathbf{B}_x}{\partial \mathbf{r}^2} [\mathbf{T}_m]^T \overline{\mathbf{r}}] \\ 
[\mathbf{B}_y + \frac{\partial \mathbf{B}_y}{\partial \mathbf{r}} [\mathbf{T}_m]^T \overline{\mathbf{r}} + (1/2) \overline{\mathbf{r}}^T [\mathbf{T}_m] \frac{\partial^2 \mathbf{B}_y}{\partial \mathbf{r}^2} [\mathbf{T}_m]^T \overline{\mathbf{r}}] \\ 
[\mathbf{B}_z + \frac{\partial \mathbf{B}_z}{\partial \mathbf{r}} [\mathbf{T}_m]^T \overline{\mathbf{r}} + (1/2) \overline{\mathbf{r}}^T [\mathbf{T}_m] \frac{\partial^2 \mathbf{B}_z}{\partial \mathbf{r}^2} [\mathbf{T}_m]^T \overline{\mathbf{r}}] 
\end{bmatrix}$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
A14: A13식을 다시 고정좌표계로 이동한 모습
</span>
</center>  

<br/>

여기에 추가로 Small-Angle Assumption을 적용하여 각을 0으로 근사시키면 $ sin \theta = 0, cos \theta = 1 $ 이 되어 $ \mathbf{T}_m $ 을 다음과 같이 쓸 수 있다.  

<center>$$[\mathbf{T}_m] = \begin{bmatrix}
1 & \theta_z & - \theta_y \\ 
- \theta_z & 1 & \theta_x \\ 
\theta_y & - \theta_x & 1
\end{bmatrix}$$</center>

<center>
<span style=
"font-size:80%;
color:gray">
A15: A2를 간단히 바꾼 모습
</span>
</center>  

<br/>