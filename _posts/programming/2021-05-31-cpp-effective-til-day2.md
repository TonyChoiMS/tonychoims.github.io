---
layout: post
title:  "Effective C++ Today I Learn (Day2)"
date: 2021-05-31
desc: "Day2 복습"
keywords: "cpp, effective, initalizer list"
categories: [Programming]
comments: true
tags: [cpp, Effective, initalizer list]
icon: icon-html
---

# Effective C++ Day2

> 객체를 사용하기 전에 반드시 그 객체를 초기화 하자!

- 초기화에 런타임 비용이 소모될 수 있는 상황이라면 값이 초기화 된다는 보장이 없습니다.
    - 배열(C++의 C인 부분)은 각 원소가 확실히 초기화된다는 보장이 없습니다.
    - STL의 vector(C++의 STL부분)는 초기화가 된다는 보장을 가지고 있습니다.
    - 이렇기에 모든 객체를 사용하기 전에 **항상** 초기화 하는 것입니다.

**대입**(assignment)을 **초기화**(Initialization)와 헷갈리지 않는 것이 가장 중요합니다.

```cpp
// '초기화'가 아닌 '대입'을 하고 있습니다.
DevRookie::DevRookie(const std::string& name, const std::string& address,
										const std::list<PhoneNumber>& phones)
{
		theName = name;
		theAddress = address;
		thePhones = phones;
		numTimesConsulted = 0;
}
```

- 초기화는 생성자가 호출되기 전에 데이터 멤버의 기본 생성자가 호출되었습니다.
- 그 중 numTimesConsulted은 기본제공 타입의 데이터 멤버이기 때문에 생성자 안에서 대입되기 전에 초기화되리란 보장이 없습니다.

**초기화 리스트**(Initalizer List)를 사용하면 됩니다.

```cpp
// 이제 생성자 본문에서 대입하는 것이 아닌 초기화를 하고 있습니다.
DevRookie::DevRookie(const std::string& name, const std::string& address,
										const std::list<PhoneNumber>& phones)
: theName(name),
	theAddress(address),
	thePhones(phones),
	numTimesConsulted(0)
{		
		// Do Nothing...
}
```

- 데이터 멤버에 사용자가 원하는 값을 주고 시작한다는 점에서는 똑같지만, 초기화 리스트를 사용하는 것이 더 효율적일 가능성이 큽니다.
    - 대입을 사용한 버전에서는 기본 생성자를 호출해서 초기화를 미리 해 놓은 뒤, 생성자에서 곧바로 새로운 값을 대입하는 것입니다.
        - 초기화 직후(데이터 멤버의 생성자) → 대입(복사 대입 연산자 호출)
    - 초기화 리스트에서 쓰이는 인자는 데이터 멤버에 대한 생성자의 인자로 쓰이기 때문에 대입이 일어나지 않습니다.
        - 초기화(복사 생성자 호출)
    - 기본제공 타입의 객체는 초기화와 대입에 걸리는 비용의 차이가 없지만, 같이 초기화 리스트를 사용하는 것이 좋습니다.

- 너무 과한 것 아닌가?

     어떤 데이터 멤버가 멤버 초기화 리스트에 들어가지 않았고, 그 데이터 멤버의 타입이 사용자 정의 타입이면, 컴파일러가 자동으로 그들 멤버에 대해 기본 생성자를 호출하게 되어 있기 때문입니다.

     하지만 초기화 리스트를 애용하는 센스를 보여줘야만, 어쩌다 리스트에서 멤버를 빼먹었을 때 어떤 멤버가 초기화되지 않을 수 있다는 사실을 끌고 가야 하는 부담이 없어지게 됩니다. (초기화가 반드시 이루어진다고 장담을 할 수 없기 때문입니다.)

초기화 리스트를 사용하는 것이 선택이 아닌 **의무**가 될 때도 있습니다. 바로 상수나 레퍼런스로 되어 있는 데이터 멤버의 경우입니다.

- 상수와 레퍼런스는 대입 자체가 불가능하기 때문입니다.

- C++에서 초기화가 변덕스럽지 않은 부분이 하나 있는데, 바로 **객체를 구성하는 데이터의 초기화 순서**입니다.
    1. 기본 클래스는 파생 클래스보다 먼저 초기화 됩니다.
    2. 클래스 데이터 멤버는 선언된 순서대로 초기화 됩니다.
    3. 멤버 초기화 리스트에 넣어진 순서가 다르더라도, 초기화 순서는 그대로입니다.(주의)

- **비지역 정적 객체**의 초기화 순서는 **개별 번역 단위**에서 정해집니다.
    - 정적 객체(static object)는 자신이 생성된 시점부터 프로그램이 끝날 때까지 살아 있는 객체를 일컫습니다.
        - 스택 / 힙 기반 객체는 정적 객체가 될 수 없습니다.
        - 전역 객체의 범주에 들어가는 것은..
            1. 전역 객체
            2. 네임스페이스 유효범위에서 정의된 객체
            3. 클래스 안에서 static으로 선언된 객체
            4. 함수 안에서 static으로 선언된 객체
            5. 파일 유효범위에서 static으로 정의된 객체
        - 1, 2, 3, 5는 비지역 정적 객체(non-local static object)라고 합니다.
        - 4는 지역 정적 객체(local static object)

    - 번역 단위(translation unit)은 컴파일을 통해 하나의 목적 파일(object file)을 만드는 바탕이 되는 소스 코드를 일컫습니다.
        - 기본적으로 소스 파일 하나가 되는데, 그 파일이 #include하는 파일들까지 합쳐서 하나의 번역 단위가 됩니다.

다시 정리하면, 서로 다른 번역 단위에서 정의된 비지역 정적 객체들의 상재거인 초기화 순서는 **정해져 있지 않습니다.**

```cpp
class FileSystem
{
public:
	std::size_t numDisks() const;

};

extern FileSystem tfs;

class Dircetory
{
public:
	DirectoryCache(params);
};

Directory::Directory(params)
{
	std::size_t disks = tfs.numDisks();
}
```

- 이 문제를 해결하기 위해 비지역 정적 객체를 지역 정적 객체로(함수를 호출하는 방식으로) 바꾸면 해결 가능합니다.
    - 이 패턴이 바로 Singleton Pattern 입니다.
    - 지역 정적 개체는 함수 호출 중 그 객체의 정의에 최초로 닿았을 때 초기화가 되도록 C++에서 보장해줍니다.

    ```cpp
    class FileSystem { ... };
    FileSystem& tfs()
    {
    		static FileSystem fs;
    		return fs;
    }

    class Directory { ... };

    Directory::Directory( params )
    {
    		...
    		std::size_t disks = tfs().numDisks();
    		...
    }

    Directory& tempDir()
    {
    		static Directory td;
    		return td;
    }
    ```

    정적 객체 자체를 직접 사용하지 않고, 그 객체에 대한 참조자를 반환하는 함수를 사용하도록 변경한 것입니다.

    - 참조자 반환 함수는 구현이 단순하지만, 다중스레드 시스템에서는 동작에 장애가 생길 우려가 있습니다.
    - 그렇기 때문에 다중스레드가 시작되기 전 미리 참조자 반환 함수를 미리 호출하도록 합니다.
    - 그렇게 되면 초기화에 관계된 Race Condition을 예방할 수 있습니다.

    **Key Point**

    1. 기본제공 타입의 객체는 직접 손으로 초기화합니다.
    2. 생성자 안에서 대입을 통한 데이터 입력 보다는 초기화 리스트를 즐겨 사용합니다. 추가로 초기화 리스트에 데이터를 나열할 때 각 데이터 멤버가 선언된 순서와 똑같이 하면 더 좋습니다.
    3. 여러 번역 단위에 있는 비지역 정적 객체들의 초기화 순서 문제는 피해서 설계해야 합니다. (비지역 정적 객체 → 지역 정적 객체)