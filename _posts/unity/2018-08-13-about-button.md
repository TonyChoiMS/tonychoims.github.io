---
layout: post
title:  "Unity3D Button Component"
date:   2018-08-13
desc: "Unitiy3D Button Component에 대한 정리."
keywords: "Unity, Button, UI, Component"
categories: [Unity]
tags: [Unity, Button, UI, Component]
icon: icon-html
---


# **[Button Component]**

 - 컴포넌트의 이름에 맞게 Button Component가 추가된 UI를 사용자가 누를 경우 이벤트를 실행할 수 있도록 설계된 Component다.
 - Web Form의 Submit 또는 Cancel과 유사한 컴포넌트.
 
<br />
## *Property*

1. Interactable : Button 기능을 활성/비활성화 한다. Transition 속성이 Animation일 경우 이 옵션을 언체크하면 Disabled Trigger가 발생한다.
2. Transition
 * 버튼은 Normal, Highlighted, Pressed, Disabled 총 4가지의 상태를 가지고 있다.
 * 이 때, 버튼의 클릭, 롤오버, 비활성화 등의 상태 및 버튼의 외형의 변화를 어떻게 변경할 것인지 설정한다.[None/ColorTint/SpriteSwap/Animation]
 * None : 버튼 상태가 바뀌어도 아무런 변화가 없다.
 * Color Tint : 버튼 상태에 따라 색상의 변화를 준다. Color Multiplier로 변하는 색상의 농도를 조절할 수 있다. Fade Duration은 다른 상태로 페이드인, 아웃 되는 시간을 조절할 수 있다.
 * SpriteSwap : 버튼 상태에 따라 이미지를 변경한다. 기존의 Target Graphic은 Normal상태의 이미지로 지정되고, 그 외 상태일 때의 이미지를 지정할 수 있는 속성이 추가된다.
 * Animation : 애니메이션 효과를 적용할 수 있으며, 'Auto Generate Animation' 버튼을 누를 경우 애니메이션 컨트롤러가 자동 생성된다.
3. Navigation
 * 키보드 입력 포커스를 받은 후 키를 통해 다음 버튼으로 이동하는 방식을 설정한다.
 * None : 포커스 이동 기능을 사용하지 않는다.
 * Horizontal : 좌우 화살표 키만 허용한다.
 * Vertical : 상하 화살표 키만 허용한다.
 * Automatic : 상하좌우 화살표 키를 모두 사용하며 자동으로 이동 순서가 결정된다.
 * Explict : 포커스 이동을 직접 선택할 수 있으며, 전후좌우 방향 이동이 자유롭다.
4. OnClick : 버튼을 클릭했을 때 수행할 함수를 연결하는 이벤트 속성이다.


![이해를 돕기 위해 Button Component 이미지를 첨부](/static/assets/img/blog/Unity/buttoncomponent.png)



참고 : https://docs.unity3d.com/Manual/script-Button.html

