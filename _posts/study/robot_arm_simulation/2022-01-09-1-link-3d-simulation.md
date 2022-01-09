---
title: "[Robot Arm Simulation] 1. 1Link Simulation on 3D"
excerpt: "The Magnetic Robot Laboratory"
header: 
    teaser: \assets\images\me.png

categories: 
    - Robot Arm Simulation(with MATLAB)
tags: 
    - Robot Arm Simulation
last_modified_at: 2022-01-09t18:00-20:00
comments: true
toc: true
toc_sticky: true
use_math: true
---

<br/><br/>

# 1. Calculate the Coodinate of End Effect

MATLAB으로 로봇 팔을 시뮬레이션을 하기 위해서는 먼저 링크는 그리는 것 먼저 해야 한다고 생각해 3차원에서의 그래프를 그리는 방법을 이용하여 그림을 그려보았다.  

<br/>

다음과 같이 3차원 좌표계에서 링크가 있다고 해 보자.  

<center>
<img src="\assets\images\study\robot_arm_simulation\2022-01-09-1-link-3d-simulation\img1.PNG" width="50%" height="50%">
</center>

<center>
<span style=
"font-size:70%;
color:gray">
그림1. 3차원에서의 1 Link
</span>
</center>

<br>

이때, 직선 $\overline{OP}$의 길이를 $l$이라고 하고, $x$축 기준으로 $q$도, $xy$평면과는 $r$도 떨어져 있다고 하자. 그렇다면 직선 $\overline{OQ}$는 직선 $\overline{OP}$을 $r$도 만큼 사영을 시킨 길이이므로, $l·cos(r)$가 됨을 알 수 있다.  

<center>
<img src="\assets\images\study\robot_arm_simulation\2022-01-09-1-link-3d-simulation\img2.PNG" width="50%" height="50%">
</center>

<center>
<span style=
"font-size:70%;
color:gray">
그림2. 직선 $\overline{OQ}$의 길이
</span>
</center>

<br>

따라서 직선 $\overline{OQ}$의 길이가 정해짐에 따라 $xy$평면에서의 좌표는 cos과 sin을 이용하여 다음과 같이 계산이 가능하다.  

<center>

$\overline{OA} = l·cos(r)·cos(q)$  <br/>
$\overline{OB} = l·cos(r)·sin(q)$

</center>

<center>
<span style=
"font-size:70%;
color:gray">
식1. $\overline{OA}$와 $\overline{OB}$의 길이. 즉 $xy$평면에서의 좌표이며, 각도 $q$를 기준으로 계산함
</span>
</center>

<br/><br/>

<center>
<img src="\assets\images\study\robot_arm_simulation\2022-01-09-1-link-3d-simulation\img3.PNG" width="50%" height="50%">
</center>

<center>
<span style=
"font-size:70%;
color:gray">
그림3. 직선 $\overline{OA}$와 $\overline{OB}$의 길이
</span>
</center>

<br>

마지막 남은 $z$축 좌표도 마찬가지로 계산하면 된다.  각 $\angle POQ$가 $r$이므로 각 $\angle COP$는 자연스레 $90-r$이 됨을 알 수 있다. 따라서 $z$좌표인 직선 $\overline{OC}$을 계산하면 다음과 같다.  

<center>

$\overline{OC} = l·cos(90-r)$

</center>

<center>
<span style=
"font-size:70%;
color:gray">
식2. $\overline{OA}$와 $\overline{OC}$의 길이.
</span>
</center>

<br/><br/>

<center>
<img src="\assets\images\study\robot_arm_simulation\2022-01-09-1-link-3d-simulation\img4.PNG" width="50%" height="50%">
</center>

<center>
<span style=
"font-size:70%;
color:gray">
그림4. 직선 $\overline{OC}$의 길이. 
</span>
</center>

<br>

따라서 3차원에서의 링크의 End Effect 좌표는 다음과 같이 계산이 된다.  

<center>

$P_x = l·cos(r)·cos(q)$ <br/>
$P_y = l·cos(r)·sin(q)$ <br/>
$P_z = l·cos(90-r)$

</center>

<center>
<span style=
"font-size:70%;
color:gray">
식3. 1-Link의 End Effect 좌표 (P 점의 좌표)
</span>
</center>

<br/><br/><br/><br/>












# 2. Simulation Codes(with MATLAB)

위에서 계산한 $P$의 좌표 값을 토대로 링크를 그리는 시뮬레이션을 작성해 보자.  

<br/>

먼저 시뮬레이션에서 그릴 링크의 길이와, $q, r$값을 설정해 준다. 
~~~matlab
% Parameters 설정
L1 = 1;     % 링크의 길이
q1 = pi/4;   % xy평면에서의 각도
r1 = pi/5;   % xy평면에서 z축 방향으로의 각도
~~~

<br/>

다음으로, 링크의 양 끝 점을 입력한다. 
~~~matlab
% 링크 1의 양 끝단 좌표 계산 및 행렬로 묶음
x1 = L1*cos(r1)*cos(q1);   Px1 = [0 x1];      % x좌표
y1 = L1*cos(r1)*sin(q1);   Py1 = [0 y1];      % y좌표
z1 = L1*cos((pi/2)-r1);    Pz1 = [0 z1];      % z좌표
~~~

<br/>

시뮬레이션이 그려질 plot에 대한 설정을 진행한다. 

~~~matlab
% 시뮬레이션을 할 링크들을 띄울 plot 설정
Fig = figure('Position', [300 300 600 600], 'Color', [1 1 1])
Axis = axes('parent', Fig);
hold on;
grid on;
axis([-2 2 -2 2 -0 2]);
title('1-Link Arm', 'fontsize', 25);   % 제목 설정
xlabel('X', 'fontsize', 15)       % x축 라벨 설정
ylabel('Y', 'fontsize', 15)       % y축 라벨 설정
zlabel('Z', 'fontsize', 15)       % z축 라벨 설정
~~~

<br/>

마지막으로 링크와 각 절편에서의 점선을 그리는 plot을 설정한다. 

~~~matlab
% 로봇 링크를 그리는 plot을 변수에 초기화
p1 = plot3(Px1,Py1,Pz1, '-or','Linewidth', 3);

% 좌표가 잘 찍혔는지 각 절편에 해당하는 점선을 그림
plot3([0 x1], [0 0], [0 0], '--k', 'Linewidth', 2);         % 원점 -> x축 좌표
plot3([x1 x1], [0 y1], [0 0], '--k', 'Linewidth', 2);       % x축 좌표 -> x, y축 좌표
plot3([x1 x1], [y1 y1], [0 z1], '--k', 'Linewidth', 2);     % x, y축 좌표 -> x, y, z축 좌표

set(p1, 'XData', Px1, 'YData', Py1, 'ZData', Pz1)
drawnow
~~~

<br/><br/>

따라서 해당 코드를 시뮬레이션 돌리면 다음과 같다.  

<center>
<img src="\assets\images\study\robot_arm_simulation\2022-01-09-1-link-3d-simulation\img5.PNG" width="50%" height="50%">
</center>

<center>
<span style=
"font-size:70%;
color:gray">
그림5. 시뮬레이션 처음 실행하면 볼 수 있는 모습 
</span>
</center>

<br/>

여기서 3D로 움직일 수 있는 버튼을 누르고 마우스로 움직이면 다음과 같이 3차원 상의 링크가 그려지는 모습을 볼 수 있다.  

<center>
<img src="\assets\images\study\robot_arm_simulation\2022-01-09-1-link-3d-simulation\img6.PNG" width="10%" height="10%">
</center>

<center>
<span style=
"font-size:70%;
color:gray">
그림6. 3차원으로 돌려볼 수 있는 버튼
</span>
</center>

<br/>

<center>
<img src="\assets\images\study\robot_arm_simulation\2022-01-09-1-link-3d-simulation\img7.PNG" width="50%" height="50%">
</center>

<center>
<span style=
"font-size:70%;
color:gray">
그림7. 최종 시뮬레이션 모습
</span>
</center>

<br>

<center>
<img src="\assets\images\study\robot_arm_simulation\2022-01-09-1-link-3d-simulation\img8.gif" width="80%" height="80%">
</center>

<center>
<span style=
"font-size:70%;
color:gray">
그림8. 최종 시뮬레이션 모습(gif)
</span>
</center>

<br/><br/>