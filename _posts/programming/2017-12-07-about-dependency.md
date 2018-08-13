---
layout: post
title:  "Dependency 의존성"
date: 2017-12-07
desc: "MVP Pattern에 대해 잘 이해하기 위해 의존성에 대해서 알아보자."
keywords: "Dependency, mvp pattern"
categories: [Programming]
comments: true
tags: [Dependency, mvp pattern]
icon: icon-html
---


# __Dependency!!__
MVP Pattern을 알기 전에 Dependency(의존성)에 대해서 한번 알아보자
<br />
## Dependency란?
 - 코드에서 두 모듈 간의 연결.
 - 객체지향언어에서는 두 클래스 간의 관계라고도 말함.
 - 일반적으로 둘 중 하나가 다른 하나를 어떤 용도를 위해 사용함.
<br />
## Dependency가 위험한 이유
 - 하나의 모듈이 바뀌면 의존한 다른 모듈까지 변경이 이루어지기 때문.
 - 테스트 가능한 어플을 만들 때 의존성이 있으면 유닛테스트 작성이 어려움.
 - 유닛테스트의 목적 자체가 다른 모듈로부터 독립적으로 테스트하는 것을 요구하기 때문.(Mock 객체로 대체가능)
<br />
## Dependency Injection(의존성 주입)이 필요한 이유
 - 위 Dependency가 위험한 이유를 해결하기 위해서 사용.
 - ‘new’ 키워드를 사용해 모듈 내에서 다른 모듈을 초기화하지 않으려면 객체 생성은 다른 곳에서 하고, 생성된 객체를 참조하면 된다.
 - 의존성 주입은 Inversion of Control 개념을 바탕으로 합니다. 클래스가 외부로부터 의존성을 가져야합니다.
 - 클래스는 다른 클래스를 인스턴스화해야 하지만, 구성 클래스에서 인스턴스를 가져와야 합니다.
 - Java 클래스가 new 연산자를 통해 다른 클래스의 인스턴스를 생성하면 해당 클래스와 독립적으로 테스트하고 사용할 수 없으며 이를 하드종속성이라고 합니다.
<br />
## 클래스 외부에서 종속성을 제공하면 생기는 이점
 - 클래스를 재사용 할 가능성을 높이고, 다른 클래스와 독립적으로 클래스를 테스트 할  수 있습니다.
 - 비즈니스 로직의 특정 구현이 아닌 클래스를 생성하는데 매우 효과적
<br />
## 의존성 주입(Dependency Injection)을 어떻게 할 것인가?
 - Contructor Injection : 생성자 삽입
 - Field Injection : 멤버 변수 삽입( 비공개 안됨)
 - Method Injection : 메소드 매게 변수 삽입.
<br />
## JSR330에 따른 종속성 주입 순서
 - Constructor
 - Field
 - Method
 - @Inject로 주석처리된 메소드나 필드가 호출되는 순서는 JSR330에 의해 정의되지 않습니다. 
<br />
### 종속성 소비자는 커넥터를 통해 종속성 공급자의 종속성(Object)을 필요로 합니다.
 - Dependency provider : @Module 어노테이션 된 클래스는 삽입 할 수 있는 객체를 제공합니다. 이러한 클래스는 @Provides 어노테이션메소드를 정의합니다(@Module -> @Provides) 이 메소드의 리턴된 오브젝트는 종속성 삽입에 사용 가능합니다.
 - Dependency consumer : @Inject 어노테이션은 의존성을 정의하는데 사용된다.
 - Connecting consumer and producer : @Component 어노테이션 인터페이스는 객체 제공자(Module)와 의존 관계를 표현하는 객체 사이의 연결을 정의합니다. 이 연결에 대한 클래스는 Dagger에 의해 생성됩니다.
<br />
## Dependency Injector란?
 - 모듈의 인스턴스를 제공하며 의존성을 주입하는 모듈
<br />
예제 및 참고 페이지
[아키텍트 코스 - Dependency Injection 이해하기] - http://imcreator.tistory.com/106 
[Dagger2 소개, 안드로이드에서 Dependency Injection 사용하기 전에] - http://www.kmshack.kr/2017/06/dagger-2-%EC%86%8C%EA%B0%9C-%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C%EC%97%90%EC%84%9C-dependency-injection-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0%EC%A0%84%EC%97%90/