---
layout: post
title:  "Singleton Pattern"
date: 2017-12-07
desc: "Design Pattern 중, SingleTon에 대해서 알아보자."
keywords: "OOP DesignePattern, Singleton"
categories: [Programming]
comments: true
tags: [OOP DesignePattern, Singleton]
icon: icon-html
---

# Singleton Pattern
<br />
## Instance란?
 - 객체(Object)를 생성하여 Heap 메모리 영역에 할당된 실체(Stack된 것)를 의미하는 개념.
<br />
## Singleton이란?
 - OOP에서의 객체는 Class와 Instance를 포함한 개념
 - 하나의 프로그램 내에서 인스턴스가 사용될 때, 이전에 생성된 인스턴스가 있을 경우 동일한 인스턴스를 생성하는 것이 아닌, 기존에 생성되어 있던 인스턴스를 가져와 사용하는 것을 기본 전략으로 내세운 디자인 패턴이다.
 - 프로그램 상에서 동일한 커넥션 객체를 만든다든지, 하나만 사용되어야 하는 객체를 만들때 유용하다. 
<br />
## Singleton 패턴을 사용하는 이유는?
 - 지정한 클래스 인스턴스가 프로그램이 작동할 때 단 한개만을 생성하여 유지하고 싶을 경우
 - new 키워드를 통해 객체를 생성하게 되면, 생성되는 클래스의 인스턴스가 Heap 메모리 영역으로 올라가게 되고, 그 인스턴스를 가리키고 있는 변수는 Stack 메모리 영역에 생기게 된다. 
이렇게 될 경우, 메모리의 낭비가 심해져 누적될 경우 프로세스 처리 시간이 길어질 수 있다.
 - 프로그램에서 지속적으로 유지가 되어야하는 정보(ex. 유저 정보 또는 프로그램의 커스텀 정보 등)를 저장/불러오기에 용이하다.
<br />
## Singleton 패턴의 단점
 - 프로그램의 Coupling을 높이게 되어 추가 수정의 작업이 있을 경우 사이드 이펙트의 이슈를 가지고 있다.
 - 멀티 쓰레드 응용 프로그램에서 명시적 초기화가 필요한 경우, 쓰레딩 문제를 예방하기 위해 조치를 취해야한다.
 - 멀티 쓰레드 환경에서 사용할 경우, 한 싱글턴 클래스를 여러 쓰레드에서 사용 및 변경하게 되면, 동기화의 이슈가 생기게 된다.
 - 이에 lock을 통해서 쓰레드에서 접근할 때 순차적으로 접근하여 한 쓰레드 씩 사용할 수 있게 처리해줘야 안전하다.

참고자료
[Java]Singleton이란/사용이유/구현방법 : http://mkil.tistory.com/199