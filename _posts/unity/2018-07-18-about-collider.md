---
layout: post
title:  "Unity3D Collider Component"
date:   2018-07-18
desc: "Unity3D Collider Component의 종류와 기능, API에 대해서 알아보자."
keywords: "Unity, component, collider, box collider, capsule collider, sphere collider, mesh collider, collision"
categories: [Unity]
tags: [Unity, component, collider, box collider, capsule collider, sphere collider, mesh collider, collision]
icon: icon-html
---
<br />
최종 수정일 : 2018-08-13
<br />
# __[Collider Component]__
<br />
<br />
 - 충돌을 감지하는 센서 역할을 하는 컴포넌트
<br />
 - Box, Sphere, Capsule, Mesh, Wheel, Terrain 의 형태 Collider 제공
<br />
## _Box Collider_
<br />
 - 가장 다용도로 사용.
 - Center, Size 속성으로 박스 형태를 조절
<br />
![BoxCollider Component](/static/assets/img/blog/Unity/boxcollider.png)
<br />
## _Sphere Collider_
<br />
 - 가장 속도 처리가 빠른 Collider.
 - Radius 속성으로 구체의 반지름을 조절
 - 정밀한 충돌 감지를 해야하는 경우를 제외하고서는 대부분 Sphere Collider 사용하는 것을 권장.
<br />
![SphereCollider Component](/static/assets/img/blog/Unity/spherecollider.png)
<br />
## _Capsule Collider_
<br />
 - 주로 인체 또는 나무, 가로등과 같은 모델의 충돌체로 사용.
 - Height 속성으로 캡슐의 높이 조절 가능.
 - Direction 속성은 Height 값을 변경했을 때 커지는 축을 설정. 기본 Y축.
<br />
![CapsuleCollider Component](/static/assets/img/blog/Unity/capsulecollider.png)
<br />
## _Mesh Collider_
<br />
 - CPU 부하가 가장 높은 Collider
 - 아주 세밀한 충돌 감지에 사용된다.
 - 유니티에서는 Mesh Collider 간의 충돌 감지가 안되도록 기본값 설정.
 - 속도 저하를 방지하기 위함
 - Convex 속성을 체크하면 Mesh 간의 충돌 감지 가능하나, 단순 메쉬로 변경.
<br />
![MeshCollider Component](/static/assets/img/blog/Unity/meshcollider.png)
<br />
## _Wheel Collider_
<br />
 - 차량의 바퀴에 사용할 목적으로 제공.
 - 바퀴의 서스펜션, 바닥과의 마찰저항과 미끄러지는 저항을 세밀하게 조절 가능.
<br />
## _Terrain Collider_
<br />
 - 유니티에 내장된 Terrain Engine을 이용해 생성한 지형에 적용되는 Collider.
 - 지형의 복잡도에 따라 Collider의 부하가 높아진다.
 - 로우폴리 Mesh를 이용해 Mesh Collider로 대체하는 것도 좋은 방법.
<br />
## _충돌 감지 조건_
<br />
 - 충돌을 일으키는 양쪽 게임오브젝트 모두 Collider 컴포넌트가 추가돼 있어야 한다.
 - 두 게임오브젝트 중 움직이는 쪽에는 반드시 Rigidbody Component가 있어야한다.
<br />
## _연산 처리 속도가 빠른 Collider_
<br />
 - Sphere Collider > Capsule Collider > Box Collider
<br />
## _충돌 이벤트._
<br />
 - Collider 컴포넌트를 포함한 게임오브젝트 간의 충돌이 발생할때 호출되는 이벤트.
 - 모든 Collider Component에는 IsTrigger 속성이 있다.
 - 이 속성을 체크할 경우 충돌은 감지되지만, 물리적인 충돌은 일어나지 않는다.
 - 주로 감지 센서 역할을 하는 게임오브젝트에서 많이 사용하는 속성.
<br />
### void OnCollisionEnter
<br />
 - IsTrigger UnCheck했을 시,
 - 두 물체 간의 충돌이 일어나기 시작했을 때
 <br />
### void OnCollosionStay
<br />
 - IsTrigger UnCheck했을 시,
 - 두 물체 간의 충돌이 지속될 때
<br />
### void OnCollisionExit
<br />
 - IsTrigger UnCheck했을 시,
 - 두 물체가 서로 떨어졌을 때
<br />
### void OnTriggerEnter
<br />
 - IsTrigger Check했을 시,
 - 두 물체 간의 충돌이 일어나기 시작했을 때
<br />
### void OnTriggerStay
<br />
 - IsTrigger Check했을 시,
 - 두 물체 간의 충돌이 지속될 때
<br />
### void OnTriggerExit
<br />
 - IsTrigger Check했을 시,
 - 두 물체가 서로 떨어졌을 때

<br />
참고 자료
 - https://docs.unity3d.com/kr/2017.4/Manual/class-BoxCollider.html
 - https://docs.unity3d.com/kr/2017.4/Manual/class-SphereCollider.html
 - https://docs.unity3d.com/kr/2017.4/Manual/class-MeshCollider.html
 - https://docs.unity3d.com/kr/2017.4/Manual/class-CapsuleCollider.html
