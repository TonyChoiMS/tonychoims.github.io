---
layout: post
title:  "Unity3D Quaternion Component"
date:   2018-07-23
desc: "Unity3D에서 회전을 담당하는 Quaternion에 대해서 알아보자."
keywords: "Unity, Quaternion"
categories: [Unity]
tags: [Unity, Quaternion]
icon: icon-html
---

* 최종 수정일 : 2018-08-13
<br />
# *__Quaternion__*
<br />
<br />
## *__[ Quaternion 이란 ? ]__*
<br />
 - 유니티에서 사용되는 각도의 단위
 - 유니티에서 회전을 표현하기 위해 사용되는 구조체(Struct)
 - 수학적인 용어로 복소수 4차원 벡터(Four-Deminsional Complex Number)
<br />
1. 각도를 4개의 원소로 표현한 것. ( = 사원수)
<br />
2. x, y, z, w로 표현되어 있음.
<br />
 - 우리가 알고 있는 1도, 45도, 90도 등의 표현은 오일러 각(Euler Angle)이라고 한다.
<br />
<br />
## *__[ Quaternion이 나오게 된 이유 ]__*
<br />
 - 오일러 각은 3차원 공간의 절대 좌표를 기준으로 물체가 얼마나 회전했는지 측정하는 방식이다.
 - 오일러 각은 회전 시킬 때, X, Y, Z 축을 차례대로 회전 시키는 방식을 사용하고 있다.
 - 이 때 X, Y, Z 축 중 2개의 축이 겹쳐 졌을 때 어느 축으로도 회전되지 않고 잠기는 현상이 발생하는데, 이를 짐벌락(Gimbal Lock)이라고 한다.
 - 유니티에서는 이 짐벌락 현상을 해결하기 위해 Quaternion이 제시되어, 세 축을 차례대로 회전시키는 것이 아닌, 세 축을 동시에 회전시키는 방식을 사용하고 있다.
 - 이렇게 때문에 유니티 게임오브젝트를 회전시킬 때 사용하는 Rotate 함수는 유니티 내부에서 Quaternion으로 자동 변형되며, rotation은 Quaternion의 타입의 속성으로 Quaternion.Euler(x, y, z) 함수를 이용해 오일러 각을 Quaternion 타입으로 변형해서 대입해야 한다.
<br />
<br />
## *__[ 참 고 ]__*
<br />
Quaternion.identity
 - 이것은 Quaternion 타입의 한 속성으로 API 문서에는 "회전 없음" 을 의미한다고 적혀있다.
 - 추가로 월드 좌표 축 또는 부모의 축으로 정렬된다고 나와 있다.
 - 하지만 이는 "회전 없음" 이라고 보기 보다는, "특정 회전 값 없이 생성하려는 프리팹 또는 3D 모델의 원래 회전각도로 적용한다" 라고 보는 것이 좀 더 정확할 것 같다.
 - API문서를 본다면 또 "쿼터니언은 복잡한 수를 기반으로 하고, 직관적으로 이해하기 쉽지 않습니다. 따라서 거의 접근하지 않거나 개별 쿼터니언 컴포넌트(x,y,z,w)를 수정하지 않습니다." 라고 적혀있는데, 유니티는 다 배운 이후, Quaternion에 대해 좀 더 깊숙하게 공부해 볼 필요성이 있을 것 같다.




참고 : 유니티 API
https://docs.unity3d.com/kr/530/ScriptReference/Quaternion.html
