---
layout: post
title:  "Unity3D C# Delegate"
date:   2018-07-30
desc: "C#에서 사용되는 Delegate와 Event, Action에 대한 정리"
keywords: "Unity, Delegate, Event, Action, Func, C#"
categories: [Unity]
tags: [Unity, Delegate, Event, Action, Func, C#]
icon: icon-html
---

최종수정일 : 2018-08-13
<br />
# Delegate
<br />
1. 메소드에 대한 참조를 나타내는 방
2. 메소드 대신해서 호출하는 역할
* 메소드의 대리인 역할을 해주는 변수
* 메소드를 직접적으로 호출하는 방식이 아닌, 델리게이트를 호출함으로써 해당 메소드를 호출(실행)할 수 있는 방식.
* 델리게이트를 '인스턴스화' 하면 호환되는 파라미터 타입/개수와 리턴 타입이 같은 모든 메소드를 참조할 수 있게 된다.
3. C++의 함수 포인터와 동일한 형태로 사용가능하지만, 안전하게 캡슐화하여 사용할 수 있다는 장점이 있다.
4. 콜백(CallBack) 메소드를 구현할 때 효율적이다.
* CallBack Method란? 
 - A 메소드를 호출할 때 B 메소드를 넘겨줘서 A 메소드로 하여금 B 메소드를 호출하도록 하는 것. 이 때 A 메소드를 콜백 메소드라고 한다.
5. Delegate Chain : 하나의 델리게이트에 여러개의 메소드를 연결시키는 것.
함수를 멀티캐스트(Multicast)할 때 사용하면 유용하다.
<br />

### _예제 코드_
```
using UnityEngine;

using System.Collections;

public class DelegateTest : MonoBehavior
{
    // 델리게이트에 연결할 함수의 원형 정의
    delegate void CalNumDelegate(int num);


    // 델리게이트 변수 선언
    CalNumDelegate calNum;

    void Start()
    {
        // calNum 델리게이트 변수에 OnePlusNum 함수 연결
        calNum = OnePlusNum;
        // 함수 호출
        calNum(4);


        // calNum 델리게이트 변수에 PowerNum 함수 연결
        calNum = PowerNum;

        // 함수 호출
        calNum(5);
    }

    void OnPlusNum(int num)
    {
        int result = num + 1;
        Debug.Log(“One Plus = “ +result);
    }

    void PowerNum(int num)
    {
        int result = num * num;
        Debug.Log(“Power = “ +result);
    }
}
```
<br />
<br />
## Event와 Delegate의 차이점

* 델리게이트가 public이라면, 이벤트 변수는 private 같은 느낌이다.
* 델리게이트 변수는 자신이 속한 클래스 외부에서도 호출이 가능하다.
* 이벤트 변수는 외부에서 호출이 불가능하고, 변수가 속한 클래스 내부에서만 사용하도록 제한되어있다. 
* 이벤트는 특정 조건(사건)이 발생했을 때 자동으로 메소드를 호출하는 용도로 사용된다.
<br />
<br />
## Func & Action

* 무명 델리게이트
* 미리 선언된 델리게이트 변수로써, 별도의 선언없이 사용가능하다.\
<br />
<br />
## Func Delegate

* Func은 반환값(Return Type)이 '있는' 메소드를 참조하는 델리게이트 변수
* .NET Framework에는 매개변수가 없는 메소드부터 매개변수가 16개인 메소드까지 총 17가지의 Func 델리게이트가 준비되어있다.
* Func Delegate를 사용할 때는 반드시 반환형을 지정해줘야 한다.
<br />
<br />
## Action Delegate

* Action은 반환값(Return Type)이 '없는'메소드를 참조하는 델리게이트 변수
* Func Delegate와 그 쓰임새나 형식은 같으나, 반환값(Return Value)가 없다.
<br />
<br />
## 람다식 (Lamda)
* 무명 메소드를 단순 계산식으로 표현한 것.
* 메소드는 크게 매개변수와 내부 식, 반환 값으로 구성되어있는데, 이들만 가지고 메소드를 계산으로 표현한다.
* 추후에 좀 더 자세하게 알아볼 필요성이 있음.
Ex) button.addListener(() => 메소드명);
