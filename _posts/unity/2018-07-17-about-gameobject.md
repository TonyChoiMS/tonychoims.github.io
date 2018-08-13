---
layout: post
title:  "Unity3D GameObject"
date:   2018-07-17
desc: "Unity3D GameObject와 그에 따른 API에 대해서 알아보자."
keywords: "Unity, Awake, component, componentcache, gameobject, gamobject private, public, keyword, 기본함수"
categories: [Unity]
comments: true
tags: [Unity, Awake, component, componentcache, gameobject, gamobject private, public, keyword, 기본함수]
icon: icon-html
---

최종 수정일 : 2018-08-13
<br />
# > **[GameObject]**
<br /><br />
 - 유니티는 컴포넌트 기반 개발(CBD : Component Based Development) 방법론을 지원한다.
 - CBD는 독립적인 기능 단위로 컴포넌트를 제작해 필요한 기능을 조립하는 방식.
 - 컴포넌트란 게임오브젝트의 기능을 담당하는 부분.
 - CBD는 컴포넌트의 재사용이 가능하고, 높은 생산성이 장점이다.
 - GameObject는 특정 속성이나 기능을 갖춘 오브젝트를 담을 수 있는 상자에 비유.
 - 유니티에서는 일반적으로 사용되는 오브젝트를 일부 템플릿 형태로 제공
 - Light, 3D Object, Particle, Camera
 - 캐릭터, 아이템, 상자, 몬스터 등 모든 것이 게임 오브젝트이다.
 - GameObject들은 기본적으로 Transform Component를 포함하고있다.
 - Transform Component를 통해 해당 Object가 월드 상에 어디에 위치하고 있는지, 얼마나 회전하고 있는지, 어느정도 크기인지 결정되기 때문.
<br />
<br />
## __유니티에서 GameObject에게 제공하는 기본함수__
<br />
 1. Awake
 - 스크립트가 실행될 때 한 번만 호출되는 함수.
 - 상태 값 또는 변수의 초기화에 사용된다.
 - 스크립트 함수 중, 가장 먼저 호출된다.
 - 스크립트가 비활성화 되어있어도 호출된다.
 - Coroutine으로 실행 불가.
<br />
2. Start
- Update 함수가 호출되기 이전에 한 번만 호출되는 함수.
- 스크립트가 활성화 되어있어야 실행된다.
- 다른 스크립트의 모든 Awake가 모두 다 실행된 이후에 실행된다.
- Coroutine으로 실행 가능
<br />
3. Update
- 매 프레임마다 호출되는 함수.
- 주로 게임의 핵심 로직을 작성하는데 사용.
- 스크립트가 활성화 돼 있어야 실행된다.
<br />
4. LateUpdate
<br />
- 모든 Update 함수가 호출되고 나서 한 번씩 호출된다.
- Update 함수에서 전처리가 끝난 후 실행해야하는 로직에 사용된다.
- 카메라 이동 로직에 주로 사용하는 함수.
- 스크립트가 활성화 돼 있어야 실행된다.
<br />
5. FixedUpdate
<br />
- 물리엔진의 시뮬레이션 계산주기로 기본값은 0.02초다.
- 발생하는 주기가 일정하다.
<br />
6. OnEnable
<br />
- 게임 오브젝트 또는 스크립트가 활성화 됐을 때 호출된다.
- 이벤트 연결 시 사용한다.
- Coroutine 사용 불가.
<br />
7. OnDisable
<br />
- 게임오브젝트 또는 스크립트가 비활성화 됐을 때 호출된다.
- 이벤트 연결을 종료할 때 사용한다.
- Coroutine 사용 불가.
<br />
8. OnGUI
<br />
- 레거시 GUI 관련 함수를 사용할 때 사용한다.
<br />
----------------------------------------------------------------------------------
<br />
## __Component Cache 처리__
<br />
> Update는 프레임마다 한 번씩 호출되는 함수로서 항상 최적화에 주의를 기울여야 한다.
 - 이동 로직의 경우 Transform Component의 Position 속성을 조금씩 변경하는 것으로 프레임마다 Transform Component에 접근하는 방식은 바람직하지 않다.
 - 따라서 Update 함수에서 접근해야 할 컴포넌트는 Awake 또는 Start 함수에서 미리 변수에 할당한 후에 Update 함수에서 사용하는 것을 권장한다.
<br />
## __키워드__
<br />
<br />
### 접근 지시자 public
<br />
 - 기본적으로 다른 클래스에서 접근할 수 있게 해주는 접근 지시자.
 - 유니티에서는 변수를 public으로 선언할 경우, Inspector View에 해당 변수가 노출되서, 변수의 값을 직접 수정할 수 있다.
<br />
### 접근 지시자 private
<br />
- 다른 클래스에서 접근할 수 없고, 해당 클래스에서만 사용할 수 있는 접근 지시자.
- 유니티에서는 Inspector View의 모드를 Debug Mode로 설정하면, private 변수값도 확인할 수 있다.
- Debug Mode로 설정할 경우, Inspector View는 읽기 전용(Read-Only)가 된다.
- Inspector View의 Default Mode는 Normal Mode.
- 또는 [SerializeField] 키워드를 해당 변수 private 앞에 선언할 경우, private 속성은 유지한 채, Inspector View에 해당 변수를 노출시킬 수 있다.
<br />
### this
<br />
- this 키워드를 사용한 해당 스크립트(클래스)를 지시.
- this.gameObject
- 이 스크립트(클래스)가 추가된 게임오브젝트를 의미한다.