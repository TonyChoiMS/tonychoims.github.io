---
layout: post
title:  "Unreal Engine Socket과 Weapon에 대해서.."
date:   2018-04-08
desc: "Unreal Engine에서 사용하고 있는 Socket에 대한 정리"
keywords: "Socket,Unreal,UnrealEngine,GameProgramming,Weapon"
categories: [Unreal]
tags: [Socket,Weapon,Unreal,UnrealEngine]
icon: icon-html
---

* 최종 업데이트 : 2018-04-10

# 소켓과 총 붙이기
 - 본에는 등이나 팔과 같이 특정 부위에 소켓을 붙일 수 있는데, 이 소켓에 총을 붙일 수 있다.

## 작업 프로세스
 - 캐릭터 skeleton 클래스로 들어가서 원하는 부위의 스켈레톤에 소켓을 추가한다.
 - 소켓에 프리뷰를 통해 총 에셋을 미리 구현시킨다.
 - 몸과 총이 어색하지 않도록 각도를 조정한다.
 - 캐릭터 블루프린트 클래스로 들어가서 Mesh가 Root가 되도록 static mesh를 새로 생성한다.
 - 생성된 static mesh에 이름을 부여한 후, 소켓->부모 소켓에 skeleton 클래스에서 선언했던 소켓을 추가한다.
 - static mesh에 원하는 총의 이미지를 집어넣는다.


# 총 장착 및 조준 애니메이션

## 작업 프로세스
 - 프로젝트 세팅 -> 입력 칸으로 가서 Action Mapping을 통해 입력받을 키와 행동 이름을 추가한다.
 - 캐릭터 블루프린트로 들어가서 추가한 행동 이름에 대한 함수를 호출한다.
 - equip rifle -> 토글키
 - aiming -> 누르고 있을 때만 true, 떼면 false
 - 언리얼 엔진 블루프린트에서 bool 값의 네모칸이 빈칸이면 false, 체크되있으면 true
 - bool형 변수를 선언하여 포즈를 블렌딩합니다.
## Set static mesh 함수 -> 컴포넌트의 static mesh를 노드의 공간에서 추가할 수 있는 함수.


## 위젯 블루프린트 <CrossHair 추가>
* size to content : 원본 사이즈에 맞춰서 위젯의 크기를 조정해준다.

* 앵커 : 위젯의 위치를 잡아주는 툴

* Alignment(정렬)
 - 위젯의 피봇 위치.
 - 왼쪽 위가 (0,0)이며, 오른쪽 아래가 (1,1)이다. 정렬 위치 조절을 통해 위젯 원점의 위치를 조절할 수 있다.

* Create Widget : 위젯을 생성하는 함수.

* get player controller : 0번째 인덱스는 무조건 내꺼(사용자).

* Widget->Add to Viewport : 뷰포트에 해당 위젯을 추가한다.(보이게 설정)
* Widget->Remove from Parent : 해당 위젯을 화면(Viewport)에서 삭제한다.

### FOV(Field Of View) 조정
* Camera -> Set Field Of View : 카메라의 뷰 각도를 업데이트할 수 있는 함수.
* Timeline 함수 : 특정 시간동안 FOV 값을 애니메이션화 하여 업데이트 할 수 있게 도와주는 함수.

## 피탄 이펙트
* Ray Casting : 총알의 시작점과 끝점 사이에 존재하는 물체들을 검사한 후, 그 중 시작점에서 가장 가까운 물체를 리턴해준다.
 -> 언리얼 엔진에서는 Line Trace라고함.
* 기본적으로 FPS 게임에서는 LineTrace의 시작점은 총구의 끝이 아닌, CrossHair를 기준으로 간다.
 - 언리얼의 기준에서 CrossHair를 기준으로 잡을 경우, 그 기준은 SpringArm이라고 보면 된다.

* Get Control Location : 사용자의 위치를 리턴받는 함수.
* Get Forward Vector : 입력값을 벡터로 변환해주는 함수.

* Complex Collision : 복합 컬리전. 폴리곤을 사용하여 표면을 정확하게 감싸는 컬리전.
* Break Hit Result : LineTrace의 리턴값 중 하나로, 구조체의 변수값 하나하나 직접 접근하고 싶을 때 사용.
* Impact Point : 맞은 장소 리턴.

* Apply Damage : 액터에게 데미지를 넘겨줄 수 있다.
* AnyDamage : Apply Damage 함수에서 피격된 액터(Damaged Actor)의 AnyDamage 이벤트가 호출됨.
이곳의 파라미터들은 앞쪽에서 줬던 Apply Damage 함수에서 선언한 파라미터들을 그대로 받아오는 것.

* 화면의 카메라 정보는 Controller에 저장되어있다.

* Apply POintDamage만 호출해도 AnyDamage도 같이 호출된다.


## 랙돌(Ragdoll) 세팅.

## 부분 랙돌(Ragdoll) 세팅.
* Set All bodies below Simulate Physics
 - In Bone Name : 해당 액터의 Skeleton에 저장된 뼈 이름을 기준으로 컨트롤 하고 싶은 부분의 이름을 입력한다.
* Set All bodies below Physics Blend Weight
 - Physics Blend Weight : 0~1사이의 값을 입력
 - 값이 0인 경우, 애니메이션 포즈만 쓰겠다.
 - 값이 1인 경우, 랙돌 계산 후 랙돌 포즈만 쓰겠다.
 - 값이 0.5인 경우, 애니메이션 포즈 반, 랙돌 포즈 반씩 섞어 사용.
