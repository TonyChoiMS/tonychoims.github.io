---
layout: post
title:  "Unreal Engine Character에 대해서.."
date:   2018-04-05
desc: "Unreal Engine에서 사용하고 있는 Character Class에 대한 정리"
keywords: "Character,Unreal,UnrealEngine,GameProgramming"
categories: [Unreal]
tags: [Character,Unreal,UnrealEngine]
icon: icon-html
---

# Character <캐릭터>
 - Skeletal mesh - Bone이 있는 mesh
 - 스태틱매쉬 : Bone이 없는 mesh >> skeletal mesh옵션 off
 - import mesh - 버텍스와 폴리곤 정보를 임포트 할 것인가? ->off 할 경우에는 애니메이션만 가져오겠다는 표현.
 - import Material : 보통은 off 시킴
 - import texture : 보통 off 시킴
 - PhysicsAsset : 본마다 컬리젼을 만들어준 것
 - Skeletal Mesh : 캐릭터의 버텍스, 폴리곤 정보
 - Skeleton : 캐릭터의 뼈 구조를 확인 할 수 있는 정보

## CapsuleComponent : Root Component / 캐릭터의 충돌 처리나 이동은 캡슐 컴포넌트를 활용
## Arrow Component : 캐릭터의 진행방향을 나타내주는 방향
## Mesh : 스캘레탈 매쉬 컴포넌트 / 이거 외에도 원한다면 스켈레탈 매쉬를 추가할 수 있음.
// 줄 : Scene Component와 Actor Component를 구분짓는 선

## Character Movement : 캐릭터 이동에 관련된 기능들이 들어있음. 네트워킹 기능이 구현이 되어있음. 멀티플레이어 시 캐릭터 이동을 부드럽게 보간해주는 기능이 들어있음. 오직 캐릭터 클래스에만 들어가있음. / 게이머가 바라보고 있는 방향에 영향을 받음.

//마우스 입력값을 받았을 때 플레이어 컨트롤러에 입력값을 저장.

## add controller yaw input : pawn의 플레이어 컨트롤러를 찾아서, x회전값을 누적시켜서 카메라의 절대 회전값을 변환 시켜준다.
## add controller pitch input : pawn의 플레이어 컨트롤러를 찾아서, y회전값을 누적시켜서 카메라의 절대 회전값을 변환 시켜준다.
* 둘 다 카메라를 직접 회전시켜주는 것은 아니다.

## SpringArm : Use pawn control Rotation : 플레이어 컨트롤러에 로테이션을 사용하겠다.
## Inherit Roll : 카메라가 마치 롤러 코스터처럼 회전하는 방식.

## axis 가상키 : 키의 입력이 없어도 매 프레임마다 호출이 된다.

## add input vector : 캐릭터가 어느방향으로 이동하고 싶은지 방향을 알려주는 함수. 방향은 월드 축을 기준으로 알려줌.
## Get Control Rotation : 컨트롤러의 로테이션을 가져오는 함수
## Get Forward Vector : 내가 바라보고 있는 방향을 벡터로 변환
## 상수 * 벡터 : 부호를 곱해줘서 앞인지 뒤인지 확인.

* Yaw, Pitch, Roll에 대해 외우는 소소한 팁...
- Yaw : Yaw리조리 두리번두리번
- Pitch : 끄덕끄덕(피.. 알았어)
- Roll : 롤러코스터 전방 360도 회전

## 한 프레임 내에 Add Input Vector가 여러번 호출되도 Character Movement에서 한번에 취합해서 처리한 후 최종 월드 Vector에 대해 처리하기 때문에 상관없음.

## Animation Sequence : 반복되는 하나의 동작
## Animation BluePrint
- try get pawn owner : 이 블루프린트를 쓰고 있는 pawn을 가져올 수 있다.
- 다른 쓰레드에서 돌기때문에 변수를 공유해서 쓸수 없으므로, 새로 변수를 선언해야한다.

## Blend space 1D : 변수 하나의 값에 따라서 어떤 시퀀스를 실행을 해줄지 선택해주는 에셋.

## State Machine : 상태기계 안에 여러가지 State(행동)이 존재

## Animation BluePrint->Bond Transform->Rotation->Rotation Mode
 - Replace Existing : 기존 회전값 무시  
 - Add to Existing : 기존 회전값 +@

## 중첩된 상태기계
 - 많은 애니메이션을 표현할 때 bool로 포즈를 블렌딩 하는 함수보다 효율적.
 - 가장 큰 상태를 먼저 정의한 후,
 - 각각의 상태에 들어가서 또 다시 작은 상태를 정의
 - 그 안에서 분기에 따른 애니메이션을 부여한다.
 - 처음엔 어려울 수 있으나, 적응되면 나중에 많은 애니메이션을 관리할 때 더욱 수월하다.

## Notify
  - 애니메이션이나 시퀀스가 진행이 될 때 특정 타이밍에 애니메이션 블루프린트에게 이벤트를 던져 줄 수 있다.
  - 역으로 애니메이션 블루프린트가 Pawn에게도 알려줄 수 있다.
