---
layout: post
title:  "Effective C++ Today I Learn (Day1)"
date: 2021-05-19
desc: "Day1 복습"
keywords: "Direct3d, vector"
categories: [Programming]
comments: true
tags: [cpp, Effective]
icon: icon-html
---

> ***C++를 언어들의 연합체로 바라보는 안목은 필수***

1. C++는 다중패러다임 프로그래밍 언어로 불립니다.
    - 절차적(procedural) 프로그래밍을 기본으로 하여
    - 객체 지향(object-oriented)
    - 함수식(functional)
    - 일반화(generic)
    - 메타프로그래밍(metaprogramming)

2. C++는 한가지 프로그래밍 규칙 아래 있는 통합 ㅇ너어가 아니라, 4개의 하위언어(sublanguage)를 제공하는 연합체로 구성되어 있습니다.
    - C : C++는 여전히 C를 기본으로 하고 있습니다.
    - 객체 지향 개념의 C++ : 클래스(생성자와 소멸자 개념), 캡슐화, 상속, 다형성, 가상 함수(동적 바인딩)
    - 템플릿 C++ : C++의 일반화 프로그래밍. 템플릿 메타프로그래밍(Template MetaProgramming : TMP)
    - STL : 템플릿 라이브러리. 컨테이너, 반복자, 알고리즘, 함수 객체
3.  C++를 사용한 효과적인 프로그래밍 규칙은 경우에 따라 달라집니다.
    - 그 경우란, 바로 C++의 어떤 부분을 사용하느냐입니다.

> ***#define을 쓰려거든 const, enum, inline을 떠올리자***

가급적 선행 처리자보다 컴파일러를 더 가까이 하자.

1. #define ASPECT_RATIO 1.653
    - define을 사용할 경우 사용자에겐 기호식 이름(symbolic name)으로 보이지만, 컴파일러는 선행 처리자가 숫자 상수로 바꾸기 때문에 ASPECT_RATIO라는 이름은 컴파일러가 쓰는 기호 테이블에 들어가지 않게 됩니다.
    - 에러가 발생하게 될 경우 에러 메시지에 ASPECT_RATIO가 아닌 1.653이 나타나게 됩니다.
    - 이 문제는 기호식 디버거(symbolic debugger)에서도 나타날 소지가 있습니다.

```cpp
const double AspectRatio = 1.653;
```

1. 이 문제를 해결하기 위해 매크로 대신 상수를 쓰는 것입니다.
    - 언어 차원에서 지원하는 상수 타입의 데이터이기 때문에 기호 테이블에 들어갑니다.
    - 컴파일을 거친 최종 코드가 #define을 썻을 때보다 작게 나올 수 있습니다.
    - 매크로를 쓰면 코드에 ASPECT_RATIO가 등장하면 선행 처리자가 모두 1.653으로 바꾸면서 목적 코드 안에 1.653의 사본이 등장 횟수만큼 들어가게 되지만, 상수 타입의 경우는 아무리 여러 번 쓰더라도 사본은 딱 한 개만 생기기 때문입니다.

```cpp
const char* const authorName = "Scott Meyers";
const std::string authorName("Scott Meyers");
```

1. #define을 상수로 교체하려고 할 때 주의해야 할 점이 있습니다.
    - 상수 포인터(constant pointer)를 정의하는 경우입니다.
        - 상수 정의는 대게 헤더 파일에 넣는 것이 상례이므로, 포인터는 꼭 const로 선언해 주어야 하고, 이와 더불어 포인터가 가리키는 대상까지 const로 선언하는 것이 보통입니다.
    - 클래스 멤버로 상수를 정의하는 경우, 즉 **클래스 상수**를 정의하는 경우 그 상수의 사본 개수가 한 개를 넘지 못하게 하고 싶다면 정적(static) 멤버로 만들어야 합니다.
        - 상수의 정의는 헤더 파일이 아닌 cpp파일어 둡니다.

        ```cpp
        class GamePlayer
        {
        	private:
        			static const int NumTurns = 5;    // 상수 선언
        			int scores[NumTurns];    
        		//...
        }

        const int GamePlayer::NumTurns;        // 상수 정의.
        ```

        - 상수의 초기값은 해당 상수가 선언된 시점에서 바로 주어지기 때문에 정의(Declaration)에는 상수의 초기값이 있으면 안됩니다. - 선언될 당시 바로 초기화.
        - #define은 유효범위란 무엇인지 모릅니다.
            - 매크로는 정의되면 중간에 #undef되지 않는다면, 컴파일이 끝날 때까지만 유효합니다.
            - 매크로는 어떤 형태의 캡슐화 혜택도 받을 수 없습니다.
2. 나열자(enumerrator) 타입의 값은 int가 사용되야 할 곳에서도 쓸 수 있는 것을 적극 활용해봅니다.
    - 통칭 나열자 둔갑술(enum hack)으로 알려진 기법입니다.
    - 동작방식은 const보다는 #define에 더 가깝습니다.
        - const의 주소를 잡아내는 것은 합당하지만, enum의 주소를 취하는 것은 합당하지 않습니다.
        - enum은 #define과 같이 어떤 형태의 메모리 할당도 하지 않습니다.
    - enum은 상당히 많은 코드에서 이러한 기법이 사용되고 있고, 템플릿 메타 프로그래밍의 핵심 기법이기도 합니다.

```cpp
class GamePlayer
{
	private:
		enum { NumTurns = 5; };
		int scores[NumTurns];
}
```

1. 함수처럼 쓰이는 매크로를 만드려면, #define보다는 인라인 함수를 우선적으로 생각합니다.
    - 이런 매크로를 사용할 경우 인자마다 반드시 괄호를 씌워줘야 합니다.
    - 또한 잘못된 사용이 발생할 수 있기 때문에 지양하고 있습니다.
    - 이렇기 때문에 기존 매크로의 효율을 그대로 유지하면서, 정규 함수의 모든 동작 방식 및 타입 안전성까지 완벽하게 취할 수 있는 인라인 함수에 대한 템플릿을 준비하는 것입니다.

    ```cpp
    // T가 정확히 무엇인지 모르기 때문에, 
    // 매개변수로 상수 객체에 대한 참조자를 사용합니다.
    template<typename T>
    inline void callWithMax(const T& a, const T& b)
    {
    	f(a > b ? a : b);
    }
    ```

    - 템플릿 함수는 동일 계열 함수군(Family of functions)를 만들어 냅니다.

```cpp
// a와 b 중에 큰 것을 f에 넘겨 호출합니다.
#define CALL_WITH_MAX(a, b) f((a) > (b) ? (a) : (b))

int a = 5, b = 0;
CALL_WITH_MAX(++a, b);                  // a가 두 번 증가합니다
CALL_WITH_MAX(++a, b + 10);             // a가 한 번 증가합니다.
```

> ***낌새만 보이면 const를 들이대보자!***

const의 의미로는

- 외부 변경을 불가능하게 하여 '의미적인 제약'을 소스 코드 수준에서 붙입니다.
- 어떤 값이 불변이어야 한다는 제작자의 의도를 컴파일러 및 다른 프로그래머와 나눌 수 있는 수단입니다.

```cpp
char greeting[] = "Hello";    
char *p = greeting;                // 비상수 포인터, 비상수 데이터
const char *p = greeting;          // 비상수 포인터, 상수 데이터
char * const p = greeting;         // 상수 포인터, 비상수 데이터
const char * const p = greeting;   // 상수 포인터, 상수 데이터
```

- 포인터가 가리키는 대상을 상수로 할 수도 있고, 포인터 자체를 상수로 할 수 도 있습니다.
- STL Iterator는 기본 동작 원리가 T* 포인터와 유사합니다.
    - 단, 반복자 앞에 붙는 const는 T* const랑 의미가 동일합니다.
    - 데이터 상수성(const T*)을 원한다면 const_iterator를 사용하면 됩니다.

```cpp
std::vector<int> vec;
const std::vector<int>::iterator iter = vec.begin();
*iter = 10;
++iter;          // 에러
std::vector<int>::const_iterator cIter = vec.begin();
*cIter = 10;     // 에러
++cIter;
```

- 함수에서 const 강력한 존재입니다.
    - 함수 반환값을 상수로 선언하면 안전성이나 효율을 포기하지 않고도 의도하지 않은 버그를 예방할 수 있습니다.

```cpp
class Rational {//...};
const Rational operator*(const Rational* lhs, const Rational& rhs);

Rational a, b, c;
//...
(a * b)  = c;        // const 지정 때문에 대입 방지 가능.
                     // operator*의 결과에 operator=를 호출
```

- **상수 멤버 함수**
    - 해당 멤버 함수가 상수 객체에서도 호출 가능한 함수라는 뜻입니다.
    - 함수 맨 뒤에 const를 붙여서 표현합니다.
    - 클래스의 인터페이스를 이해하기 좋게 하는 효과가 있습니다.
    - 이 키워드를 통해 상수 객체를 사용할 수 있게 하자는 뜻입니다.
    - 상수 객체에 대한 참조자(reference-to-const)로 진행할 때 상수 멤버 함수가 준비되어 있어야 한다는 것이 포인트입니다.
    - const 키워드가 있고 없고의 차이만 있는 멤버 함수들은 오버로딩이 가능합니다.

    ```cpp
    T& operator[] (std::size_t idx);
    const T& operator[] (std::size_t idx) const;
    ```

    - 실제 프로그램에서 상수 객체가 생기는 경우
        1. 상수 객체에 대한 포인터로 객체가 전달될 때
        2. 상수 객체에 대한 참조자로 객체가 전달될 때
    - 물리적 상수성[비트 수준 상수성]
        - 어떤 멤버 함수가 그 객체의 어떤 데이터 멤버도 건드리지 않아야 그 멤버 함수가 'const'임을 인정하는 개념입니다.
            - static 멤버는 제외합니다.
        - 즉, 멤버 포인터가 가리키는 대상의 수정 여부는 판단하지 않습니다.

    ```cpp
    // 부적절하지만 비트수준 상수성이 있어서 허용되는 선언..
    T& operator[] (std::size_t position) cosnt
    { return pText[position]; }
    ```

    - 논리적 상수성
        - 값이 몇개 바뀌어도 사용자가 그걸 알 수 없고, 논리적으로 상수라면, 그것은 상수입니다.
        - mutable 키워드를 사용해 상수 객체에서도 수정 가능한 멤버를 생성할 수 있습니다.
        - 컴파일러가 비트 수준 상수성을 지켜주지만, 개념적인(논리적인) 상수성을 사용하면서 프로그래밍 하는 사람이 되어야합니다.
    - 상수 멤버 및 비상수 멤버 함수가 기능적으로 서로 똑같이 구현되 있을 경우, 비상수 버전이 상수 버전을 호출하게 해서 코드 중복을 피하도록 합니다.
        - const_cast 를 통해 캐스팅을 하는 것은 일반적으로 썩 좋지 못한 아이디어입니다.(나중에 추가적으로 나올 얘기)
        - *this의 타입캐스팅을 하는 방법을 이용해 캐스팅을 한번이 아니라 두번을 하도록 합니다.
            - 첫번째로 *this에 const를 붙이는 캐스팅을 하고,
            - 두번째로 상수 반환 값에서 const를 떼어내는 캐스팅을 합니다.
        - 상수 멤버 함수에서 비상수 멤버 함수를 호출하게 되면, 데이터를 수정하지 않겠다고 약속한 객체를 배신하는 것이 되기 때문에 틀리다는 얘기가 나오는 것입니다.

```cpp
char& operator[] (std::size_t position)
{
    return const_cast<char&>(
        static_cast<cosnt TextBlock&>
             (*this)[position]
        );
}

```

- **KeyPoint**

- const를 붙여 선언하면 컴파일러의 도움을 받을 수 있습니다
const는 어떤 유효범위에 있는 개체, 함수 매개변수 및 반환 타입 그리고 멤버 함수에도 붙을 수 있습니다.
- 컴파일러 쪽에서 보면 비트수준 상수성을 지켜야 하지만, 작성자인 우리는 논리적인 상수성을 사용해서 프로그래밍 해야합니다.
- 상수 멤버 및 비상수 멤버 함수가 기능적으로 서로 똑같게 구현되어 있을 경우에는 코드 중복을 피하는 것이 좋은데, 이때 비상수 버전이 상수 버전을 호출하게 해야합니다.