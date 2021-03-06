---
layout: post
title:  "Unity3D Graphics, Light"
date:   2018-07-16
desc: "Unreal Engine에서 사용하고 있는 Actor Class에 대한 생각과 고민에 대한 블로깅"
keywords: "Graphics, Light, Material, Mesh, Shader, Texture, Unity, unity3d, gameprogramming"
categories: [Unity]
comments: true
tags: [Graphics, Light, Material, Mesh, Shader, Texture, Unity, unity3d]
icon: icon-html
---

최종 수정일 : 2018-08-13
<br />
# **[Graphics]**
<br />
<br />
## __Texture__  
<br />
> 3D 모델의 표면에 매핑시킬 이미지 파일을 지칭.
<br />
<br />  
### Texture 기능으로 Mesh, Particle 및 Interface에 이미지를 매핑.
<br />
	- 매핑 - 이미지 또는 동영상을 오브젝트에 겹치거나 둘러싸는 것.
	- PSD(포토샵), PNG, JPEG, TIFF, GIF, BMP, TGA 등 다양한 이미지 파일 포맷  지원
	- PSD 파일에 있는 여러 개의 레이어를 자동으로 평면화(Flatten)한다.
	- 텍스쳐의 원본을 보존한 상태로 다양한 압축 포맷으로 용량을 줄이는 기능을 제공.
	- 텍스쳐의 크기가 가로세로 2^n 형태일 때 압축 지원 속도가 가장 빠르다.  
    - 모바일 플랫폼을 사용할 경우 이 형태를 사용하는게 가장 유리하다.
<br />
### Texture Type
<br />
 - Texture : 모든 텍스처에서 사용되는 가장 일반적인 설정.
 - Normal Map : 색상 채널을 실시간 노멀 매핑에 맞는 형식으로 변경.
 - Editor GUI : 텍스처가 임의의 HUD/GUI 컨트롤에서 사용된다면 사용 권장. 
 - Sprite(2D and UI) : 텍스처가 2D게임에서 Sprite로 사용할 경우 권장. 
 - Cubemap : 큐브 맵으로 알려져 텍스처의 반사를 만드는데 사용.
 - Cookie : 텍스처에서 라이팅의 쿠키에서 사용하는 기본 파라미터 설정.
 - Advanced : 텍스처에서 특정 파라미터를 이용해 세부적인 제어를 하고 싶을 경우 설정.
<br />
### Material
<br />
- 3D 모델에 적용할 텍스쳐의 다양한 속성을 설정하는 역할.
- “어떤 텍스처를, 어떤 간격으로 반복하고, 표면의 재질은 어떻게 표현하느냐”
<br />
### Mesh Filter
<br />
 - 애니메이션이 적용되지 않은 3D모델은 Mesh Filter와 Mesh Renderer Component를 가지고 있다.
 - 해당 모델의 3차원 형상 정보인 Mesh 데이터를 가지고 있는 컴포넌트.
 - Asset에서 Mesh 데이터를 가져와서 화면상에서 렌더링하기 위해 Mesh Renderer에 전달.
 - Scene 내의 Mesh를 확인하려면 Mesh Renderer를 게임 오브젝트에 추가하면 된다. 
 - 기본적으로 Mesh Filter Component를 게임 오브젝트에 추가할 경우 Mesh Renderer가 같이 추가 되지만, 임의로 삭제했을 경우 수동으로 다시 추가해줘야한다.
 - Mesh Renderer가 없는 경우에도 Mesh는 Scene(및 컴퓨터 메모리)에 존재하고 있지만, 그려지지는 않는다.
<br />
### Mesh Renderer
<br />
 - Mesh Filter가 가지고 있는 Mesh 데이터를 토대로 화면에 렌더링 처리를 하는 Component
 - 유니티에서 제공하는 ~Renderer 계열의 컴포넌트는 반드시 Material 속성을 가지고 있기 때문에 텍스처 정보를 가지고 있는 머티리얼을 연결하는 속성이 있다는 것을 의미한다.
<br />
### Shader
<br />
> Material에 적용한 텍스처를 렌더링할 때 표면의 재질감을 표현하는 방식을 결정한다.
<br />

### Rendering Mode
<br />  
 - Opaque : 기본값으로 불투명한 텍스처를 표현하는 옵션. 투명이 전혀 없는 Solid 객체에 적합.
 - Cutout : 불투명한 부분과 투명한 부분을 동시에 표현하는 옵션. 풀, 그물망 등을 표현할 때 적합.
 - Transparent : 투명한 플라스틱 또는 유리와 같이 재질을 표현하는 옵션.
 - Fade : 투명 속성값을 갖고 있는 객체를 페이드 아웃 시키는 옵션. 페이드 인/아웃을 애니메이션 처리할 수 있다. 홀로그램(Hologram) 효과 구현에 용이.
 - Albedo : 빛을 반사하는 정도. 반사율이라고 한다. 현실의 물체는 모두 각각 다른 빛 반사율을 가진다.
 - Metallic : 객체 표면에 금속의 재질을 표현하기 위한 텍스쳐. 슬라이드 값이 1에 가까워질수록 금속 재질에 가까워지는 특성.
 - Normal Map : 표면의 세밀한 입체감이나 질감을 표현하기 위한 텍스처의 일종으로 3D모델링으로 많은 폴리곤을 소모하지 않고 같은 효과를 낼 수 있다. 속성값이 
 커질수록 음영효과를 낸다.
 - Height Map : 텍스처로 높낮이를 표현하는 것. 노멀맵과 비슷하지만 사물을 더 돌출시켜 뒤에 있는 사물을 가리는 Occlusion 효과를 낼 수 있다.
 - Occlusion : 흑백의 텍스처로 간접조명에 의해 생기는 명암을 더욱 뚜렷이 표시해 사물의 입체감과 깊이감을 살리는 데 사용.
 - Emission : 스스로 빛을 방출하는 속성. 속성값을 변경하면 객체의 표면에서 방출되는 빛의 강도와 빛을 색상을 설정할 수 있는 항목이 나타남. 전역 조명에 반영하기 위한 옵션도 포함.
 - Detail Mask : Secondary Maps에 적용할 마스크를 설정하는 텍스처 슬롯. 특정 부분을 좀 더 세부적인 텍스쳐를 표현할 때 사용
<br />
### Prefab
<br />
> 유니티에서 사용하는 Asset Type.
 - 컴포넌트 및 프로퍼티가 있는 게임 오브젝트를 저장할 수 있다.
 - 자주 사용하는 객체를 미리 정의해놓은 GameObject 및 Component의 컬렉션을 재사용할 수 있게 하는 기능.
 - 씬에서 새로운 오브젝트 인스턴스를 생성하는 템플릿으로 사용.
 - 복사가 가능한 원본의 개념으로, 프리팹의 복사본(Clone)은 원본의 속성과 일치한다.
 - 따라서 원본을 수정할 경우 그에 따라 복사본도 같이 수정된다.
 - 각 인스턴스의 컴포넌트와 설정을 개별적으로 ‘오버라이드’ 할 수 있다.
<br />
#  **[Light]**
<br />
<br />
## __Directional Light__
<br />
 - 해당 라이트의 위치와 관계없이, 전체 화면에 균일한 빛을 비춘다. 
 - 다만, 빛을 비추는 각도에 따라 그림자의 방향과 길이가 달라진다.
 - 실시간 그림자 지원
<br />
## __Point Light__
<br />
 - 백열전구와 같은 성격. 
 - Point Light가 위치한 좌표를 중점으로 주변으로 퍼져나가는 조명. 
 - 빛의 범위를 설정할 수 있는 Range 속성이 있다.
 - 실시간 그림자 지원
<br />
## __Spot Light__
<br />
 - 손전등과 같이 Corn 모양으로 빛을 내는 조명/ 실시간 조명 중 가장 비싼 조명. 
 - 빛이 뻗어 나가는 각도를 조절할 수 있는 Spot Angle 속성이 있다.
 - 실시간 그림자 지원
<br />
## __Area Light__
<br />
 - 사각형 형태의 조명으로 한쪽 면에서 빛을 발하는 조명. 
 - 라이트맵을 Bake해야만 확인할 수 있다. 
 - 유일하게 실시간 조명이 아니며 주로 간접 조명으로 사용.
 - 실시간 그림자 미지원
 <br />
## __Shadow Type__
<br />
 - No Shadows : 기본 설정값으로, 실시간 그림자를 적용하지 않는다.
 - Hard Shadows : 실시간 그림자를 표현하나 외곽선을 부드럽게 처리하지 않는다.
 - Soft Shadows : 부드러운 실시간 그림자를 표현하지만 가장 많은 부하를 준다.
<br />
# **[LOD]**
<br />
<br />
## __Level Of Detail__
<br />
> 화면을 렌더링하는 카메라로부터 멀리 떨어질수록 낮은 폴리곤으로 변경해서 렌더링 부하를 줄여주는 기법
<br />
## __Culled__
<br />
 - LOD 구간 중, 카메라로부터 너무 멀리 떨어져 있는 경우, 완전히 보이지 않게 하는 기법.
 - 멀티플레이를 구현 할 때 메모리 활용할 때 유용하며, 모바일 게임의 최적화 기법 중 중요한 요소.