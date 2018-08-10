---
layout: post
title:  "Unity3D RigidBody Component"
date:   2018-07-17
desc: "Unitiy3D RigidBody Component에 대한 정의 및 정리."
keywords: "Unity, rigidbody, 리지드바디"
categories: [Unity]
tags: [Unity, rigidbody, 리지드바디]
icon: icon-html
---


# **[Rigidbody Component]**

 - GameObject가 물리 제어로 동작하게 하는 컴포넌트

 - 물리 시뮬레이션을 통해서 오브젝트의 위치를 조절.

 - 중력, 충돌에 대한 오브젝트의 반응의 크기를 계산.

## *Property*

1. Mass : 질량. 상대적인 의미의 질량으로, 일반적인 kg, g 등의 무게 단위는 아니다. ‘A 물체 mass가 1, B 물체 mass가 10이라고 할 때 B물체는 A물체보다 10배 더 무겁다.’ 라고 해석하는 것. 보통은 1Mass = 1Kg이라고 가정 후 작업하는 것이 일반적.

2. Drag : 이동할 때 적용되는 마찰계수(저항)

3. Angular Drag : 회전할 때 적용되는 마찰계수(저항)

4. Use Gravity : 중력 적용 여부

5. Is Kinematic : 체크하면(True) 물리엔진의 영향을 받지 않으며, Transform 컴포넌트를 이용해 이동한다.

6. Interpolate : 물리력을 이용한 움직임이 끊어지는 현상이 발생할 때 보간해준다.

7. Interpolate : 이전 프레임의 Transform에 맞게 처리

8. Extrapolate : 다음 프레임의 Transform의 변화를 추정해 움직임을 처리

9. Collision Detection : 세밀한 충돌을 검출하기 위한 옵션값

10. Discrete -> Continuous -> Continuous Dynamic 순서로 정밀 검출

11. Freeze Position : X,Y,Z 축 중에서 해당 축으로의 이동을 막는다.

12. Freeze Rotation : X,Y,Z 축 중에서 해당 축을 기준으로 한 회전을 막는다.


![이해를 돕기 위해 Rigidbody Component 이미지를 첨부](/static/assets/img/blog/rigidbody.png)



참고 : https://docs.unity3d.com/kr/530/ScriptReference/Rigidbody.html

