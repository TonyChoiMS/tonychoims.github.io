---
layout: post
title:  "Direct3D Vector"
date: 2018-10-17
desc: "Vector 정리"
keywords: "Direct3d, vector"
categories: [Programming]
comments: true
tags: [Direct3d, vector]
icon: icon-html
---

### 벡터(Vector, 방향량)
 - 크기(Magnitude)와 방향(Direction)을 모두 가진 수량(Quantity)을 가리키는 말
 - 좀 더 정확하게는 벡터값 수량(Vector-valued quantity)이라고 부른다.
 - 힘이나 변위, 속도(Velocity)를 나타내는 데 쓰인다.
 - 힘의 크기를 제외한 순수한 방향만을 표현할 때에도 벡터가 쓰인다.
 - 벡터를 시각적으로 표현할 때는 방향이 있는 선분으로 표현한다.
 - 선분의 길이는 벡터의 크기를 나타내고, 선분의 화살표 방향은 벡터의 방향을 나타낸다.
 - 이 때 벡터를 그리는 위치는 중요하지 않다. 위치 이동은 벡터의 크기와 방향에 영향을 주지 않기 때문이다.
 - 벡터는 크기와 방향이 같으면 위치와 상관없이 같은벡터로 인정된다.

벡터 수량값의 예로는
힘, 변위, 속도가 있다.

# 힘(Force)
 - 힘은 특정한 방향과 세기로 가해진다.
 - 여기서 세기는 힘의 크기를 의미한다.

# 변위(Displacement)
 - 한 입자의 최종적인 이동 방향 및 거리

# 속도
 - 빠르기와 방향

### 좌표계
 - 컴퓨터는 벡터를 기하학적으로 다루지 못하므로, 좌표계를 통해 벡터를 수치적으로 지정한다.
