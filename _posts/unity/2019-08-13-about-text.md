---
layout: post
title:  "Unity3D Text Component"
date:   2018-08-13
desc: "Unitiy3D Text Component에 대한 정리."
keywords: "Unity, Text, UI, Component"
categories: [Unity]
tags: [Unity, Text, UI, Component]
icon: icon-html
---


# **[Text Component]**
 - 사용자에게 텍스트 메시지를 표현할 때 사용하는 컴포넌트.
 - 다른 GUI 컴포넌트들과 함께 사용해서 UI를 표현할 수 있다.
 
<br />
## *Property*

1. Text : 표시할 텍스트
2. Font : 텍스트에 사용할 폰트
3. Font Size : 표시할 폰트의 크기
4. Line Spacing : 멀티라인의 경우 글자의 상하 사이 간격
5. Rich Text : 입력 텍스트를 마크업 형식으로 표현할 지 여부(마크업 태그 표현 가능)
6. Alignment : 가로, 세로 글 정렬 옵션
7. Horizontal Overflow : Text 가로 영역을 넘어선 글의 처리 방식(Wrap : 자동개행 / Overflow : 범위를 넘어가도록 허용)
8. Vertical Overflow : Text 세로 영역을 넘어선 글의 처리 방식(Wrap / Overflow)
9. Best fit : Font Size를 무시하고 Text 컴포넌트의 범위에 맞게 크기를 조정한다.
10. Color : Text 색상
11. Material : Text에 별도의 머티리얼을 적용할 수 있다.
<br />
## * Text Effect *
 - Shadow 컴포넌트를 새로 추가함으로써, Text에 그림자 효과를 추가할 수도 있다.


![이해를 돕기 위해 Text Component 이미지를 첨부](/static/assets/img/blog/unity/textcomponent.png)



참고 : https://docs.unity3d.com/Manual/script-Text.html

