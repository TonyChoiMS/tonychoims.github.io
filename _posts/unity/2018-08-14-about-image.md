---
layout: post
title:  "Unity3D Image Component"
date:   2018-08-14
desc: "Unitiy3D Image Component에 대한 정리."
keywords: "Unity, Image, UI"
categories: [Unity]
tags: [Unity, Image, UI]
icon: icon-html
---


# **[Image Component]**
 - 화면에 텍스쳐를 표시하는 컴포넌트
 - Sprite로 변환된 텍스처만 사용할 수 있다.
<br />

## **Property**

1. Source Image : 화면에 표시하려는 이미지(Sprite만 허용)
2. Color : 이미지의 색상 지정(RGBA)
3. Material : 이미지를 렌더링하기 위한 머티리얼(노멀맵 적용 시 사용 가능)
4. Image Type : 이미지를 표시하는 방식으로 4가지 옵션.
 - Simple
    * 반복이 필요 없거나 이미지 고정 크기인 경우의 옵션
    * Preserve Aspect를 선택 후 이미지 크기를 조절하면, 원본 이미지의 가로/세로 비율에 맞춰 자동으로 조절된다.
    * 또는 모든 UI 항목은 Shift 키를 누른 채 크기 조절을 하면 등비율로 조절된다.

 <br />

 - Sliced
    * 이미지 리사이즈를 해도 이미지 왜곡이 없이 표현하는 옵션
    * 크기를 조절해도 외곽선의 뭉개짐이나 깨짐이 없도록 Sprite Editor를 통해서 설정할 수 있다.
    * 말풍선이나 로그인 대화상자 같은 윈도우를 제작할 때 유용하게 사용됨.
    * Fill Center 속성은 가운데 이미지를 채울 것인가에 대한 속성.
 <br />


 - Tiled
    * 이미지를 타일링 처리할 수 있는 옵션
    * 이미지 크기가 바뀌어도 동일한 패턴이 크기에 상관없이 반복됨.
 <br />


 - Filed
    * 이미지를 부분적으로 채울 수 있는 옵션
    * 특정 방향으로 채워서 그릴 수 있는 것으로, Fill Method  속성에 정의
    * 어느 위치에서부터 채워지기 시작하는지는 Fill Origin 속성으로 선택할 수 있다.
    * Clockwise 속성은 시계방향 또는 반대방향을 결정하는 속성이다.
    * Fill Amount 속성은 0.0f ~ 1.0f까지의 값을 지정할 수 있으며, 이미지가 채워지는 비율을 선택하는 속성이다.
    * Filled Image Type은 게임 개발 시 생명 게이지 또는 스킬 버튼의 쿨링타임을 표현할 때 유용하다.
<br />



![이해를 돕기 위해 Image Component 이미지를 첨부](/static/assets/img/blog/Unity/ImageComponent.png)

# **[RawImage Component]**
 - 배경 이미지와 같이 큰 이미지에 사용되는 컴포넌트.
 - Sprite 타입 뿐만 아니라 일반 Texture 타입의 이미지도 사용할 수 있다.
 - Sprite Atlas는 포함되지 않는다. (메모리 낭비를 방지하기 위함)
 - UV Rect X, Y 속성은 이미지의 위치를 보정할 수 있는 Offset이다.
 - UV Rect W, H 속성은 가로/세로의 확대 비율이다.

참고 
 - Unity UI는 Z-Order의 개념을 하이러키 뷰의 순서로 결정한다.
 - 하이러키 뷰에 배치된 순서에 따라 Z-Order가 결정되니, UI를 작업할 때는 유의해서 배치해야한다.(큰 UI로 인해 작은 UI가 가려질 수 있음.))

참고 : https://docs.unity3d.com/Manual/script-Image.html

