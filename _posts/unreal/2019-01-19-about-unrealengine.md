---
layout: post
title:  "Unreal Engine LandScape에 대해서.."
date:   2019-01-19
desc: "Unreal Engine 기초"
keywords: "UnrealEngine"
categories: [Unreal]
tags: [Unreal,UnrealEngine]
icon: icon-html
---

입문과 팁

UObject : 기본이 되는 클래스 => 유니티의 Component
 -> 가비지 컬렉터, 레퍼런스 업데이트
 -> 레퍼런스 카운터 존재
 -> 스마트포인터 사용 권장.

AActor : 게임 내에 배치되는 오브젝트. (= GameObject), UObject 상속
 -> 하지만 가비지 컬렉션에 의해 관리되지 않고, 해제자를 통해서만 해제를 할 수 있다.
 -> 레퍼런스 카운터가 없음.

object와 actor의 차이점.
 -> UObject를 상속하는 클래스 받는 클래스 접두사는 U
 -> AActor를 상속하는 클래스 받는 클래스 접두사는 A

 클래스를 생성할 때 이름에 A 또는 U는 자동으로 붙여지기 떄문에 따로 입력하지 않는다.

APawn, ACharacter : 게임 상에서 움직이는 모든 액터들을 표현할 떄 사용하는 클래스.

APawn과 ACharacter의 차이 : ACharacter는 2족보행(인간형)에 특화된 APawn

UActorComponent : 기능만 구현. Actor에 귀속되는 컴포넌트

USceneComponent : Transform을 가지고 있는 컴포넌트. ex 카메라.

CDO Class Default Object

클래스 생성자로 인해 생성된 이후로 변경되지 않음.

C++ 구조.

include generated.h : 리플렉션이라는 실행 시간에 자신을조사할 수 있는 기능이 동작.
PROJECTDRU_API
리플렉션이란? 런타임에 객체의 정보를 알 수 있는기능.
 -> 실행 중에 (런타임중) 클래스가 무엇을 가지고 있는지, 어떤 기능을 수행하는지 알 수 있는 기능.
 -> 실행 중에 프로퍼티를 제공할 수 있는 기능.
 -> generated.h가 존재하는 이유.
 -> C++에는 리플렉션이 없다. 유일하게 언리얼만이 리플렉션 기능을 갖추고 있다.

GENREATED_BODY() 매크로.
 -> 이 매크로 아래 작성되는 변수 및 함수는 public이 default로 선언된다.
 -> 가독성을 위해 public, private는 명시적으로 선언해주는 것이 좋다.

언리얼 엔진 클래스는 DLL로 관리.

언리얼 모듈에 대한 이해 필요.

핫리로드 : 생성자 수정 또는 헤더에서 수정할 경우 적용이 잘 안되는 경우 존재.

언리얼변수 UPROPERTY 매크로 사용. 블루프린트에서 변수를 사용할 경우는 UPROPERTY가 public 변수여야함.

언리얼의 코딩 표준에서는 변수는 대문자로 시작한다.

AController는 AActor를 상속받는 클래스.

FConstPlayerControllerIterator

TActorIterator

Check 기능.

UE_LOG

EngineUtils.h -> GEngine->AddOnScreenDebugMessage
 - Print함수와 동일.

 언리얼이 유니티보다 먼저 나옴

 #include "Engine/World.h"


 unit의 기본단위 unity : m // unreal : cm.

 GetPlayerPawn -> GetPlayerCharacter를 더 많이씀.
 -> 차이점.

 Kismet -> 언리얼3에서 쓰이는 비주얼스크립팅.
 언리얼4에서의 블루프린트 스크립팅.

 블루프린트에서 제공하는 함수들을 사용하고 싶을때는 Kismet을 include로 가져와야 한다.
