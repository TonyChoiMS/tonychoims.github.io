---
layout: post
title:  "Unity3D Canvas"
date:   2018-08-04
desc: "Unity3d의 UI를 담당하는 Canvas에 대해서 알아보자."
keywords: "Unity, Canvas, EventSystem, Rect Transform, Anchor, Component"
categories: [Unity]
tags: [Unity, Canvas, EventSystem, Rect Transform, Anchor, Component]
icon: icon-html
---

최종 수정일 : 2018-08-13
<br />
<br />
# __GameObject Canvas__
 - Unity에서 모든 UI Element(텍스트, 이미지, 버튼, 슬라이더 등)는 반드시 이 Canvas 객체 하위에 위치해야만 한다.
 - Rect Transform, Canvas, Canvas Scaler, Graphic Raycaster. 총 4개의 컴포넌트로 구성된 GameObject.
 - 한 Scene에서 여러개 생성하거나 다른 Canvas 객체의 하위로 차일드화 할 수 있다.
 - Hierarchy View에 Canvas를 생성할 경우, Event System도 자동으로 생성된다.
<br />
## EventSystem
 - 시스템에서 발생하는 키보드, 조이스틱, 스크린터치 등의 입력 정보를 Canvas 하위에 있는 UI 항목에 전달하는 역할.
 - Standalone Input Module 컴포넌트를 포함하고 있다.
 - First Selected 속성을 통해 처음 포커스를 갖는 UI 항목을 지정할 수 있다.
 - EventSystem이 없다면, UI 항목이 클릭 또는 터치와 같은 이벤트에 반응하지 않는다.
<br />
## Rect Transform
 - Canvas 및 UI 항목에 자동적으로 추가되어있다.
 - 앵커(Anchors), 피봇(Pivot), 크기(W, H), 위치(Pos X, Pos Y, Pos Z)와 회전 및 스케일 정보를 저장하고 있다.
 - UI용 Transform 컴포넌트 / 기존 Transform 컴포넌트와 동일한 역할
 - 속성을 직접 수정할 수 없으며, 화면의 크기에 따라 자동으로 설정된다.
<br />
## Anchor Point
 - UI 항목 상위의 Canvas 영역을 기준으로 표시하는 것.
 - UI 항목의 정렬(Align)과 크기 조절(Stretch)을 설정한다.
 - 앵커 포인트는 각각 4개의 삼각형으로 구성돼 있으며, 각각 개별적으로 움직일 수 있다.
 - 앵커 포인트는 UI 항목 자기 자신의 Rect Transform이 기준이 아니라 그 상위 객체의 Rect Transform을 기준으로 삼는다.
<br />
## Anchors Min & Max
 - 앵커 값의 범위를 나타내며, % float 형식의 값이 들어가며, %로 표현된다.
 - Pivot
<br />
## Anchor Preset
 - 각 UI 항목의 정렬과 크기를 미리 정의해놓은 집합.
 - UI 항목의 Inspector View의 Rect Transform의 가장 왼쪽에 있는 것.
 - UGUI의 기본이 되는 개념
 - 앵커 프리셋은 각각 일반 마우스를 클릭했을 때와 Alt 키와 Shift키의 조합에 따라 다른 조합을 볼 수 있다. [Alt + Click] [Shift + Click] [Alt + Shift + Click]
<br />  
## anchoredPosition
 - Rect Transform 속성 맨 위에 있는 Pos X, Pos Y, Pos Z는 해당 UI 항목의 ‘앵커 포인트를 기준’으로 상대적으로 얼마만큼 떨어져 있는지를 나타내는 anchoredPosition이다.
<br />
## Canvas Component
1. UI 항목을 화면에 배치하고 렌더링하는 역할.
2. Render Mode 옵션에 따라 UI 항목의 화면 배치 방식을 결정할 수 있다.
3. Screen Space - Overlay
 - 기본 설정값으로 UI 항목은 씬의 가장 상위 계층에서 표현되며, 화면의 해상도에 맞춰 자동으로 스케일이 조절된다.
4. Screen Space - Camera
 - 씬의 가장 상위에 UI 항목이 표시되는 것은 Overlay방식과 같지만, UI 항목을 렌더링하는 별도의 카메라를 설정할 수 있다.
 - 씬을 비추는 Main Camera와 UI를 위한 카메라로 이원화할 수 있다.
 - Render Camera 속성에 원하는 카메라를 연결하면 된다.
 - UI Camera의 Projection 속성을 Perspective로 설정
 - UI Camera를 따로 설정할 경우, Main Camera와 충돌이 없도록 반드시 Clear Flag, Culling Mask, Depth속성을 적절히 설정해야 한다.
5. World Space
 - 씬 내에 있는 다른 게임오브젝트에 직접 UI 항목을 추가한다.
 - 대표적으로 HUD(Head Up Display)를 구현할 때 사용.
 - 특정 게임오브젝트에 Canvas 객체를 추가하고 Render Mode를 World Space로 설정하면 해당 Canvas는 더는 Rect Transform의 영향을 받지 않으며, 해당 게임오브젝트의 위치에 영향을 받는다.
<br />
![Canvas Component Render Mode 변경에 따른 내용](/static/assets/img/blog/Unity/canvas1.png)
![Canvas Component Render Mode 변경에 따른 내용](/static/assets/img/blog/Unity/canvas2.png)
![Canvas Component Render Mode 변경에 따른 내용](/static/assets/img/blog/Unity/canvas3.png)