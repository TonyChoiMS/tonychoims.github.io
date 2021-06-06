---
layout: post
title:  "Effective C++ Today I Learn (Day3)"
date: 2021-06-01
desc: "Day3 복습"
keywords: "cpp, effective, constructor, destuctor"
categories: [Programming]
comments: true
tags: [cpp, Effective, constructor, destuctor]
icon: icon-html
---


## Effective C++ Day3

> **C++가 은근슬쩍 만들어 호출해 버리는 함수들에 촉각을 세우자**

C++에는 클래스 안에 직접 선언하지 않으면 컴파일러가 자동으로 생성해주는 멤버 함수들이 있습니다.

- 복사 생성자 (Copy Constructor)
- 복사 대입 연산자 (Copy Assignment Operator)
- 생성자와 소멸자 (Constructor & destructor)
    - C++11에서 이동생성자와 이동대입연산자도 추가되었다고 합니다. 이 부분에 대해서는 뒷부분에서 더 알아볼 예정입니다.

이들은 모두 public 멤버이며, inline함수입니다.

```cpp
class Empty{};
```

```cpp
class Empty
{
	public:
		Empty() { ... }
		Empty(const Empty& rhs) { ... }
		~Empty() { ... }

		Empty& operator=(const Empty& rhs) { ... }
};
```

---

소멸자는 클래스가 상속한 기본 클래스의 소멸자가 가상 소멸자로 되어 있지 않으면 비가상 소멸자로 만들어집니다.

```cpp
template<typename T>
class NamedObject
{
	public:
		NamedObject(const char *name, const T& value);
		NamedObject(const std::string& name, const T& value);

	private:
		std::string nameValue;
		T objectValue;
}
```

 이처럼 클래스 안에 생성자가 존재할 경우, 컴파일러는 기본 생성자를 만들어내지 않습니다.

 → 인자를 받는 생성자를 직접 만들었는데, 컴파일러가 인자를 받지 않는 생성자를 만들진 않을까 걱정할 필요가 없습니다.

반면, 이 코드에서 복사 생성자와 복사 대입 연산자는 컴파일러에 의해 기본형으로 만들어집니다.

---

컴파일러가 함수를 자동으로 생성하려면 최종 결과 코드가 '적법'(legal)해야 하고, '이치에 닿아야만(reasonable)'합니다.

```cpp
template<class T>
class NamedObject
{
	public:
		// 이 생성자는 이제 상수 타입의 name을 취하지 않습니다.
		// nameValue가 비상수 string의 참조자가 되었기 때문입니다. 
		// 참조할 string을 가져야 하기 때문에 char*는 없앱니다.
		NamedObject(std::string& name, const T& value);
	private:
		std::string& nameValue;
		const T objectValue;
}

std::string newDog("Persephone");
std::string oldDog("Satch");

NamedObject<int> p(newDog, 2);
NamedObject<int> s(oldDog, 36);

p = s;
```

 C++의 참조자는 자신이 참조하고 있는 것과 다른 객체를 참조할 수 없습니다.

그렇기에 해당 코드는 컴파일러가 에러를 통해 거부하게 됩니다.

 그렇기 때문에 참조자를 데이터 멤버로 갖고 있는 클래스의 대입 연산을 지원하려면, 직접 복사 대입 연산자를 정의해줘야 합니다.

 데이터 멤버가 상수 객체인 경우에도 비슷하게 동작하게 됩니다.

 **파생 클래스 쪽에서 호출할 권한이 없는 멤버 함수(private)는 컴파일러에 의해 암시적으로 생성되는 함수를 가질 수 없습니다.** 

## **KeyPoint**

컴파일러는 경우에 따라 클래스에 대해 기본 생성자, 복사 생성자, 복사 대입 연산자, 소멸자를 암시적으로 만들어 놓을 수 있습니다.