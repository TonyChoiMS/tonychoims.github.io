---
layout: post
title:  "Unreal Engine System에 대해서.."
date:   2018-04-05
desc: "Unreal Engine에서 System에 관련된 행동을 하는 객체들에 대한 생각과 고민에 대한 블로깅"
keywords: "Unreal,UnrealEngine,GameProgramming"
categories: [Unreal]
comments: true
tags: [System,Unreal,UnrealEngine]
icon: icon-html
---
# Unreal Engine 4 Game System.

## Game Mode
 - 게임에 영향을 미치는 가장 중요한 규칙을 구현하는 액터
 - 게임 서버의 역할을 한다고 봄.

### HUD : 게임 UI를 렌더링하는 액터

### PlayerState : 남들이 알아야 하는 내 정보를 저장하는 액터

### GameState : 게임에 공통된 정보를 동기화 시킬 때 저장하는 장소로 사용하는 액터

// 참고 .. 데디케이트 서버 : 클라이언트가 없고 게임 로직만 돌아가는 서버

// 맵 이동을 하게 되면, 게임 모드와 플레이어 컨트롤러가 날라간다(삭제 후 재호출).
// 게임 스테이트, 플레이어 스테이트, 폰 모두 날라감

## 레벨간의 데이터를 주고 받을 수 있는 방법

### Game Instance Class : 게임이 처음 실행 될 때 생성된 후, 게임이 종료될 때 destroy
 - project setting -> map & mod -> game default map : 게임 실행 파일을 실행했을 때 제일 처음 실행될 맵(보통 인트로 or 로그인)
