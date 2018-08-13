---
layout: post
title:  "Unity3D Generic Collection, Boxing and Unboxing"
date:   2018-07-28
desc: "C#에서 사용되는 Generic Collection과 Boxing, Unboxing에 대한 정리"
keywords: "Unity, Generic Collection, Boxing, unboxing, 일반화 콜렉션, C#"
categories: [Unity]
comments: true
tags: [Unity, Generic Collection, Boxing, unboxing, 일반화 콜렉션, C#]
icon: icon-html
---

최종 수정일 : 2018-08-13
<br />
# __일반화 컬렉션__
<br />
 - 종류 : List, Queue, Stack, Dictionary
 - ArrayList, Queue, Stack, HashTable의 일반화 버전
 - using System.Collection.Generic; 네임스페이스 안에 존재하기 때문에 사용 선언 필수.
<br />
> 일반화 컬렉션(Generic Collection)을 사용하는 이유.
 - C# 언어 내부에서 제공하는 Collection(Stack, Queue, ArrayList, HashTable)에 데이터의 입, 출력이 있으면 그때마다 박싱과 언박싱이 계속해서 발생하게 되고, 데이터가 많아질수록 컴퓨터 성능에 상당한 부하가 발생하게 된다.
 - 부하가 발생하는 원인 : 컬렉션은 데이터의 어떤 타입도 전부 object 타입으로 저장하기 때문에, 데이터에 접근할 때마다 본래 타입으로의 형식변환이 일어나기 때문이다. => Boxing과 UnBoxing.
 - 성능 상의 이슈가 문제가 된다면, 컬렉션보단 일반화 컬렉션(Generic Collection)을 사용하기로 한다.
<br />
<br />
# __Boxing__
 - 값(Value) 형식을 Object형식 또는 이 값 형식에서 구현된 임의의 인터페이스 형식으로 변환하는 프로세스.
 - 값 형식을 참조 형식으로 바꾸는 것.
 - 메모리의 Stack 영역에서 Heap 영역으로 데이터가 복사되고, 그 복사된 데이터를 object가 참조하게 한다.(값 형식 -> 참조 형식)
 - 암시적이다.
 ![Boxing의 예시](/static/assets/img/blog/Unity/boxing.png)
<br />
<br />
# __UnBoxing__
 - Boxing된 데이터를 Heap 영역에서 Stack영역으로 복사한다.(참조 형식 -> 값 형식)
 - 명시적이다.
![UnBoxing의 예시](/static/assets/img/blog/Unity/unboxing.png)
<br />
참고 : https://docs.microsoft.com/ko-kr/dotnet/csharp/programming-guide/types/boxing-and-unboxing