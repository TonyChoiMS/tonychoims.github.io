---
layout: post
title:  "Unreal Engine LandScape에 대해서.."
date:   2018-04-08
desc: "Unreal Engine에서 사용하고 있는 LandScape에 대한 정리"
keywords: "LandScape,Foliage,Unreal,UnrealEngine,GameProgramming"
categories: [Unreal]
tags: [Actor,Unreal,UnrealEngine]
icon: icon-html
---

# 랜드스케이프란?
- 임의로 만들어진 모양의 그리드 3D 모델
- X,Y 값 자동 계산(내가 건들수없음)
- 높이(Z) 값만 조각 기능을 통해서 제공
- 버텍스 사이의 길이는 100 -> Scale값, 단위는 cm
- 연두색으로 나뉘어 있는 큰 단위는 Section
- Component는 Section의 모임
- Number Of Component : 한 랜드스케이프에 들어가는 컴포넌트의 갯수
* 정리
 - 한개의 랜드스케이프에 여러개의 컴포넌트가 들어가고,
 - 한개의 컴포넌트에 여러개의 섹션이 포함되어있으며,
 - 한개의 섹션은 여러개의 버텍스로 이루어진다.
 - 랜드스케이프 하나당 최대 길이는 8.161Km
 - Section Per Component -> 한 컴포넌트에 몇개의 섹션을 지정할 것인가?

## Layer Info Object
랜드스케이프 레이어에 대한 정보가 들어있는 에셋.
어느 지역에 얼마만큼의 강도로 텍스쳐를 칠할지의 강도

## LOD란?
 - Level Of Detail의 약자
 - 플레이어를 기준으로 플레이어가 대상 스태틱 매쉬에 멀어지면 해당 매쉬를 덜 복잡한 버전 또는 보이지 않게끔 하여 레벨 퍼포먼스를 높이는 기술
 - .FBX로 저장된 매쉬로 구현.

## 폴리지 시스템
 - 랜드스케이프에서 텍스쳐링 하듯 스태틱 매쉬를 렌더링 할 수 있는 시스템
 - 스태틱 매쉬들 간의 Z fighting이 일어나지 않게 조정

## 폴리지 타입
 - align to normal -> 지형에 따라 폴리지를 어떻게 배치할 것인가?(나무는 꺼주고 잔디는 켜주는게 일반적)
 - Random Yaw -> 스태틱 매쉬가 바라보는 방향
 - Cull Distance -> 개활지의 경우 로딩을 어디까지(거리) 할 것인가?
 - 컬리전 프리셋 -> 충돌 처리
 - LandScape Layers -> 특정 랜드스케이프에만 추가할 수 있게 하는 옵션

## 프로시저럴 함수
  - 단순한 절차적 생성 텍스처와 마스크를 빠프게 만들 수 있다.
  - 임포트된 텍스처에 비해 메모리가 절약된다.
* Procedural Foliage Volume

* Procedural -> Collsion Radius : 나무들 간의 사이 거리
* Procedural -> shade Radius : 일단 스킵
* Procedural Foliage Blocking Volume -> 폴리지를 다시 시뮬레이션을 눌러도 폴리지 타입이 생성되는 것을 방지한다.

## 스트리밍 레벨
 - (작은 폴리지를 관리할 때 사용하는 것)퍼시스턴트 레벨의 자식 레벨, 퍼시스턴트가 살아있는 한, 메모리에 올렸다 내리는 것이 자연스러운 레벨
 - 효율적인 메모리 관리가 가능
 - 퍼시스턴트 레벨과 시공간을 공유.

## Current Level(현재 레벨)
 - 액터를 추가할 때, 액터가 추가되는 맵의 레벨
 - 레벨 창에서 파란색으로 이름이 표시되있는 것이 현재 레벨

## Level Bounds(레벨 바운드)
 - 스트리밍 레벨이 퍼시스턴트 레벨에서 어느정도 범위를 가지고 있는지 미리 계산을 해서 박스의 형태로 가지고 있는 것
 - 폴리지는 액터 취급을 안해줌
 - 레벨 바운드의 범위(streaming distance)를 직접 지정해주고 싶을 경우 레벨 탭의 월드 컴포지션으로 들어감.
 - 하나의 레벨 바운드는 하나의 레이어만 할당할 수 있다.(1:1 관계)

## World Composition(월드 컴포지션)
 - 스트리밍 레벨이 어떻게 나뉘어있는지 한눈에 볼 수 있는 툴
 - 레이어를 새로 생성해서 커스텀할 경우 스트리밍 거리를 커스텀 할 수 있다.
 - 레이어는 수정 기능이 없음.
 - 하나도 세팅되지 못한 레이어는 나중에 자동적으로 삭제됨.

* [참조]언리얼엔진이 아닌, 맵을 구성할 때 사용하면 유용한 이미지 툴
 - 월드 머신 / 월드 크리에이터 (유료 버전만 존재)
 - Wysilab - Instant Terra : 무료 트라이얼

 - Height Map : 버텍스 하나를 그림파일로 대응시키는 방식
 - 흰색 : 최고 높은 지형의 색
 - 검은색 : 최고 낮은 지형의 색
 - Height가 0~255 일 때, Import하면 -256*(Scale Z축의 값)~256*(Scale Z축의 값)으로 임포트됨
 - Scale = Instant Terra Range값 / 512(언리얼엔진 값 범위 [상수])
// FOB
