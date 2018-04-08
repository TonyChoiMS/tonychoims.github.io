---
layout: post
title:  "Unreal Engine Socket과 Weapon에 대해서.."
date:   2018-04-20
desc: "Unreal Engine에서 사용하고 있는 Socket에 대한 정리"
keywords: "Socket,Unreal,UnrealEngine,GameProgramming,Weapon"
categories: [Unreal]
tags: [Socket,Weapon,Unreal,UnrealEngine]
icon: icon-html
---

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
