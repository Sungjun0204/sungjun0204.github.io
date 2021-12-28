---
title: "[Robot Laboratory 4] 1. ODE Simulation"
excerpt: "ODE and Kinematics Simulation"
header: 
    teaser: 

categories: 
    - Robot Laboratory 4
tags: 
    - Robot Laboratory 4
last_modified_at: 2021-12-27t09:00-15:00
comments: true
toc: true
toc_sticky: true
use_math: true
---

<br/><br/><br/><br/>  

# 로봇학실험4 (Robot Laboratory4) Project 

해당 수업에서 배운 내용은 다음과 같다. 
-	ODE(Open dynamics Engine)를 통한 기구학 Simulation
-	MFC UI 제작
-	ATMega128과 Maxon 모터를 이용한 각종 모터 제어

<br>

해당 포스팅에서는 ODE에 대한 설명을 할 것이다. 코드는 깃 허브 Repository에 업로드를 해 놓았으니 아래 링크를 타고 들어가 참고하기 바란다.  
→
[Repository로 이동](https://github.com/Sungjun0204/Robot_Laboratory_4)

<br/>
<br/>
<br/>

# ODE (Open Dynamics Engine)

물리 엔진이며, 사실 조금 오래된 프로그램이라고 한다. MFC에 추가하여 사용할 수 있으며, 자세한 설치법을 설명하기 보다는 코드에 대해 설명하므로, 설치법을 알고 싶다면 아래의 다른 이의 블로그 포스팅을 참고해주기 바란다. 아래 블로그 주인장이 설명을 잘 해 주신다.  
→
[ODE 설치 관련 글로 이동](https://blog.naver.com/PostView.naver?blogId=tmdals727&logNo=220333154602&parentCategoryNo=&categoryNo=97&viewDate=&isShowPopularPosts=true&from=search)


<br/>
<br/>

이를 MFC에서 실행하면 다음과 같이 나온다.  

<center>
<img src="\assets\images\learn\robot-laboratory-4\2021-12-27-ODE_Simulation\img1.png" width="70%" height="70%" title="ODE_view">
</center>

<center>
<span style=
"font-size:70%;
color:gray">
MFC에서 ODE를 띄운 모습
</span>
</center>

<br/>

또한, MFC 코드를 열어보면 다음과 같은 cpp 파일들이 있는 것을 볼 수 있다.  

<center>
<img src="\assets\images\learn\robot-laboratory-4\2021-12-27-ODE_Simulation\img2.png" width="35%" height="35%" title="MFC_Code_files_list">
</center>

<center>
<span style=
"font-size:70%;
color:gray">
MFC 코드 파일 리스트
</span>
</center>

<br/>

여기에서 "ODE.cpp"파일에서 시뮬레이션을 위한 코딩을 하게 된다. 

<br/><br/><br/>





## 시뮬레이션 초기 설정

시뮬레이션을 위한 기본 Parameters 설정 값은 다음 표와 같다. 

<center>
<img src="\assets\images\learn\robot-laboratory-4\2021-12-27-ODE_Simulation\img3.jpg" width="70%" height="70%" title="MFC_Code_files_list">
</center>

<center>
<span style=
"font-size:70%;
color:gray">
로봇학 실험4 ODE 시뮬레이션 시작 모습
</span>
</center>

<br/>


|구분|링크1(빨강)|링크2(초록)|링크3(파랑)|
|--|:--:|:--:|:--:|  
|길이|0.5|1.0|0.5|  
|무게|0.5|1.0|0.5|  
|반경|0.125|0.125|0.125|  
|질량중심|0.25|0|-0.75|  
|관절 위치|0|0.5|-0.5|  

<br/>

해당 프로젝트에서 모터를 돌릴 때 아래를 기준으로 돌리기 때문에 링크 3의 관절 위치가 지면을 뚫고 들어간 위치로 지정하게 되었다.
<center>
<img src="\assets\images\learn\robot-laboratory-4\2021-12-27-ODE_Simulation\img4.png" width="30%" height="30%" title="MFC_Code_files_list">
</center>

<center>
<span style=
"font-size:70%;
color:gray">
로봇학 실험4 에서 실제 돌린 모터의 모습
</span>
</center>

<br/>

## ODE 코드 설명

먼저 가상 물리 엔진에 대한 가상 환경을 구축한다. 

~~~cpp
// 가상 물리 엔진의 가상 환경을 구축
void InitODE() {

	//TO DO
	dInitODE();										// ODE에 대한 초기 설정 함수 선언
	g_World = dWorldCreate();						// 가상 물리 엔진 월드 설정
	g_Space = dHashSpaceCreate(0);					// 월드의 공간 설정
	g_Contactgroup = dJointGroupCreate(0);
	dWorldSetGravity(g_World, 0, 0, -GRAVITY);		// 각 축에 작용하는 중력 설정
	g_Ground = dCreatePlane(g_Space, 0, 0, 1, 0);	// 지면과의 충돌이 있을 시 사용
	dWorldSetCFM(g_World, 1e-5);					// 생성한 월드의 기본적인 한계력(제약 사항) 설정
}
~~~

<br/>

가상 환경이 구축이 되었다면, 가상환경에서 물체를 그리는 코드를 작성한다.

~~~cpp
void InitDrawStuff() {

	g_Fn.version = DS_VERSION;
	g_Fn.start = &StartDrawStuff;
	g_Fn.step = &SimLoopDrawStuff;
	g_Fn.command = &CommandDrawStuff;
	g_Fn.stop = StopDrawStuff;
	g_Fn.path_to_textures = DRAWSTUFF_TEXTURE_PATH;
}
~~~

<br/>

가상환경에서의 지면과 접촉할 때 지면을 뚫고가지 않도록 하는 코드를 작성한다. 그런데 해당 프로젝트에서는 지면을 뚫고 가야 내가 원하는 자세를 취할 수 있으므로 해당 함수는 결과적으로는 사용하지 않았다.  

~~~cpp
//지면과 접촉할시 출돌이 일어나게 코드를 작성
static void SpaceCollide(void* data, dGeomID o1, dGeomID o2) {
	int i;
	static const int N = 5; //접촉면의 최대개수

	dContact contact[N];
	bool isGround = (o1 == g_Ground) || (o2 == g_Ground); //지면과 접촉햇는지?

	if (isGround) {
		int n = dCollide(o1, o2, N, &contact[0].geom, sizeof(dContact));
		for (int i = 0; i < n; i++) {
			contact[i].surface.mu = 0.1; // 마찰계수
			contact[i].surface.mode = dContactBounce;
			contact[i].surface.bounce = 1.0;// 반발계수
			contact[i].surface.bounce_vel = 0.0;// 튀어오르기 위한 최소속도
			dJointID c = dJointCreateContact(g_World, g_Contactgroup, &contact[i]);
			dJointAttach(c, dGeomGetBody(contact[i].geom.g1), dGeomGetBody(contact[i].geom.g2));
		}
	}
}
~~~

<br/>

시뮬레이션을 실행할 때 물체를 바라보는 시점을 변경하는 코드이다. 이번 프로젝트에서는 지면을 뚫고 들어가야 하기에, 시점이 지평선에 위치해야 지면을 뚫고 들어가는 물체도 볼 수 있다. 

~~~cpp
void StartDrawStuff() {

	// 시작 시 시점 설정
	float dPos[3] = { 3.0, 0.0, -0.1 };
	float dRot[3] = { 180.0, 0.0, 0.0 };
	dsSetViewpoint(dPos, dRot);
}
~~~

<br/>

그리고 시뮬레이션 상에서 오브젝트를 그리는 코드이다. 오브젝트의 스펙은 위 표로 설명한 것과 같다. 

~~~cpp
void InitRobot()
{

	// Body 생성
	dMass mass;
	dMatrix3 R;			// 4 X 3 행렬을 생성

	// 질량 중심점( 평행이동 )
	dReal x[MAX_JOINT_NUM + 1] = { 0.0, 0.0, 0.0 };
	dReal y[MAX_JOINT_NUM + 1] = { 0.0, 0.0, 0.0 };
	dReal z[MAX_JOINT_NUM + 1] = { 0.25, 0.0, -0.75 };		// Z축으로 서 있는 상태를 default로 두었기에 Z축에만 값을 넣는다.

	// 링크 자세 설정
	dReal ori_x[MAX_JOINT_NUM + 1] = { 0.0, 0.0, 0.0 };
	dReal ori_y[MAX_JOINT_NUM + 1] = { 0.0, 0.0, 0.0 };
	dReal ori_z[MAX_JOINT_NUM + 1] = { 1.0, 1.0, 1.0 };
	dReal ori_q[MAX_JOINT_NUM + 1] = { 0.0, 0.0, 0.0 };		// 해당 방향으로 틀어진 정도를 설정

	// 한 덩이의 링크 길이 ( 질량 중심점을 기준으로 양방향으로 줄어듦 )
	dReal length[MAX_JOINT_NUM + 1] = { 0.5, 1.0, 0.5 };

	// 한 덩이의 무게
	dReal weight[MAX_JOINT_NUM + 1] = { 0.5, 1.0, 0.5};

	// 캡슐의 반지름
	dReal r[MAX_JOINT_NUM + 1] = { 0.125f, 0.125f, 0.125f };


	//body 생성
	for (int i = 0; i < MAX_JOINT_NUM + 1; i++) {
		g_oObj[i].body = dBodyCreate(g_World);
		dBodySetPosition(g_oObj[i].body, x[i], y[i], z[i]);
		dMassSetZero(&mass);
		dMassSetCapsuleTotal(&mass, weight[i], 1, r[i], length[i]);
		dBodySetMass(g_oObj[i].body, &mass);   // 물체의 위치 설정

		g_oObj[i].geom = dCreateCapsule(g_Space, r[i], length[i]);
		dGeomSetBody(g_oObj[i].geom, g_oObj[i].body);
		dRFromAxisAndAngle(R, ori_x[i], ori_y[i], ori_z[i], ori_q[i]);	
				// 회전축 x, y, z를 중심으로 각 q만큼 회전하는 회전행렬 R를 생성함
		dBodySetRotation(g_oObj[i].body, R);	// 물체의 형태 방향 등등 설정
	}

	//joint 관련 설정 및 생성

	// 관절의 좌표 원점 설정
	dReal djointx[MAX_JOINT_NUM + 1] = { 0.0, 0.0, 0.0 };
	dReal djointy[MAX_JOINT_NUM + 1] = { 0.0, 0.0, 0.0 };
	dReal djointz[MAX_JOINT_NUM + 1] = { 0.0, 0.5, -0.5 };

	// 회전축의 로테이션 방향
	dReal axis_x[MAX_JOINT_NUM + 1] = { 0.0, 1.0, 1.0 };
	dReal axis_y[MAX_JOINT_NUM + 1] = { 0.0, 0.0, 0.0 };
	dReal axis_z[MAX_JOINT_NUM + 1] = { 0.0, 0.0, 0.0 };

	//joint 결합
	//먼저 fixed joint 부터 world와 연결
	g_oJoint[0] = dJointCreateFixed(g_World, 0);
	dJointAttach(g_oJoint[0], g_oObj[0].body, 0);
	dJointSetFixed(g_oJoint[0]);

	//Hinge Joint 생성 및 결합
	for (int i = 1; i < MAX_JOINT_NUM + 1; i++) {
		g_oJoint[i] = dJointCreateHinge(g_World, 0);							// Hinge Joint 생성
		dJointAttach(g_oJoint[i], g_oObj[i].body, g_oObj[i - 1].body);			// Joint 결합
		dJointSetHingeAnchor(g_oJoint[i], djointx[i], djointy[i], djointz[i]);	// Hinge의 중심점을 설정
		dJointSetHingeAxis(g_oJoint[i], axis_x[i], axis_y[i], axis_z[i]);		// Hinge의 회전축 벡터 설정
	}
}
~~~

<br/>

또한, 가상환경에서 오브젝트가 움직일텐데, 움직일 때 스위치마냥 딱딱 떨어지게만 움직이면 수렴하는 과정을 볼 수 없으므로, 움직이는 것에 대한 제어기를 설정해준다. 단순하게 P 제어기로 코드를 작성했다. 

~~~cpp
void PControl()
{

	//joint control을 위한 간단한 p control 만들기
	
	dReal Kp = 1, fmax = 100.0;
	dReal derror_q[MAX_JOINT_NUM + 1];

	
	for (int i = 1; i < MAX_JOINT_NUM + 1; i++)
	{
		
		g_cur_q[i-1] = dJointGetHingeAngle(g_oJoint[i]);
		if (g_tar_q[i - 1] - g_cur_q[i - 1] > 180.0*DEG2RAD)
		{
			g_cur_q[i - 1] += 359.9*DEG2RAD;
		}

		if (g_tar_q[i - 1] - g_cur_q[i - 1] < -180.0*DEG2RAD)
		{
			g_cur_q[i - 1] -= 359.9*DEG2RAD;
		}
		
		// g_cur_q[i] = dJointGetHingeAngle(g_oJoint[i]);
		derror_q[i - 1] = g_tar_q[i - 1] - g_cur_q[i - 1];
		dJointSetHingeParam(g_oJoint[i], dParamVel, Kp*derror_q[i - 1]);
		dJointSetHingeParam(g_oJoint[i], dParamFMax, fmax);
	}
	

}
~~~

<br/>

그리고 MCU로 따지면 제어주기인 함수이다. 해당 함수에서는 앞서 작성된 오브젝트와 P제어기를 토대로 하여 목표 값을 입력받으면, 해당 각도로 오브젝트를 회전시키게 된다. 

~~~cpp
// 여기가 MCU로 따지면 제어주기 코드. ODE의 움직임을 여기서 설정함
void SimLoopDrawStuff(int pause) {

	DataType_t jointData;
	ControlData_t graph;
	bool connected;

	GET_SYSTEM_MEMORY("JointData", jointData);

	g_tar_q[0] = jointData.Q_tar[0];
	g_tar_q[1] = jointData.Q_tar[1];

	jointData.Q_cur[0] = g_cur_q[0];
	jointData.Q_cur[1] = g_cur_q[1];
	SET_SYSTEM_MEMORY("JointData", jointData);

	GET_SYSTEM_MEMORY("connect", connected);
	GET_SYSTEM_MEMORY("graph", graph);
	if (connected)
		g_tar_q[0] = graph.position;
	
	// 첫 번째 관절에 대한 예외처리 코드
	if (g_tar_q[0] >= 360.0 * DEG2RAD) g_tar_q[0] = fmod(g_tar_q[0], 360.0 * DEG2RAD);
	if (g_tar_q[0] <= -360.0 * DEG2RAD) g_tar_q[0] = fmod(g_tar_q[0], 360.0 * DEG2RAD);

	// 두 번째 관절에 대한 예외처리 코드
	if (g_tar_q[1] >= 360.0 * DEG2RAD) g_tar_q[1] = fmod(g_tar_q[1], 360.0 * DEG2RAD);
	if (g_tar_q[1] <= -360.0 * DEG2RAD) g_tar_q[1] = fmod(g_tar_q[1], 360.0 * DEG2RAD);

		// 해당 관절 각도 값이 360도 보다 크면 360도 안에서 값이 변하도록 360을 빼 주고,
		// -360도보다 값이 작으면 이 또한 마찬가지로 음수 영억 -360도 안에서 값이 변하도록 360을 더해준다.



	PControl();		// 제어기 선언

	//루프에 바디를 그리는 함수를 집어넣는 과정: 각 물체마다 설정해 주어야 함
	dReal dR, dLength;

	// dSpaceCollide(g_Space, 0, &SpaceCollide);		// 지면과의 충돌 고려 ON
	

	dsSetColor(1, 0, 0);		// 컬러 설정 ( RGB 255를 100%(1)로 보고 설정 )
	dGeomCapsuleGetParams(g_oObj[0].geom, &dR, &dLength);	// 강체 생성: 캡슐 형태
	// Parameter로 캡슐 정보, 반경, 길이 정보를 넘김
	dsDrawCapsuleD(dBodyGetPosition(g_oObj[0].body),	// 디자인된 강체를 작업하는 월드에 생성
		dBodyGetRotation(g_oObj[0].body), (float)dLength, (float)dR);	//  ㄴ> 월드에 해당 강체를 그리기 위해 
		// 강체에 대한 정보들을 Parameter로 넘김
	dsSetColor(0, 1, 0);
	dGeomCapsuleGetParams(g_oObj[1].geom, &dR, &dLength);
	dsDrawCapsuleD(dBodyGetPosition(g_oObj[1].body),
		dBodyGetRotation(g_oObj[1].body), (float)dLength, (float)dR);

	dsSetColor(0, 0, 1);
	dGeomCapsuleGetParams(g_oObj[2].geom, &dR, &dLength);
	dsDrawCapsuleD(dBodyGetPosition(g_oObj[2].body),
		dBodyGetRotation(g_oObj[2].body), (float)dLength, (float)dR);

	double dt = 0.01;
	dWorldStep(g_World, dt);
	// dJointGroupEmpty(g_Contactgroup);
}
~~~

<br/>

최종적으로 ODE를 실행시키기 위한 함수이다. 

~~~cpp
void RunODE(size_t width, size_t height) {

	//TO DO
	InitDrawStuff();
	InitODE();

	InitRobot();

	dsSimulationLoop(0, 0, width, height, &g_Fn);
}
~~~

<br/>

그러면 다음과 같이 시뮬레이션이 실행이 됨을 알 수 있다. 

<center>
<img src="\assets\images\learn\robot-laboratory-4\2021-12-27-ODE_Simulation\img5.gif" width="70%" height="70%" title="ODE_view">
</center>

<center>
<span style=
"font-size:70%;
color:gray">
최종 ODE를 띄운 모습 
</span>
</center>

<br/>

<br/><br/><br/>

