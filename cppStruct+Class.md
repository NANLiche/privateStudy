# Struct / Class

2026-08-15

## struct와 class란 무엇인가?

Struct는 구조체를 뜻하고
Class는 클래스를 의미한다

Struct와 같은 경우 C에도 이미 존재했던 객체이고,
Class는 C의 struct에서 멤버함수, 접근 지정자 등의 기능을 추가한 C++에 존재하는 매우 유사한 개념의 객체이다.

(C의 sturct의 경우 함수 포인터를 사용해야함)

---

## struct와 class의 차이는?

Struct는 기본적으로 멤버 접근이 public으로 선언되지만
Class는 Private로 선언이된다.

(GPT: 그리고 정확히는 **기본 접근 지정자가 private**라는 뜻이야)

---

## 객체란 무엇인가?

객체란? 말 그대로 객체이다.
변수와 함수들을 묶어놓은 집합체?
그런 느낌

(GPT:
객체 == 어떤 클래스 타입으로 생성된 실제 개체

예를 들어:

```cpp
class Character
{
public:
    int hp;


    void Attack();
};


Character player;
```

여기서 Character는 클래스, player는 객체야.)

---

## 멤버 변수와 멤버 함수란?

멤버 변수는 해당 객체에 속한 변수고
멤버 함수는 해당 객체에 속한 함수다.

---

## public / private이란?

public같은 경우 객체 밖에서 `C.value1 = 3;` 처럼 수정이 가능하다.

하지만 private로 선언했을 경우는 불가능하다.

그래서 보통 함수를 public으로 선언해놓고 private한 변수를 조작하는 식으로 쓰는 걸로 알고있다.

---

## 생성자란 무엇인가?

객체가 생성될때 호출되는 함수

(인자를 받을 수 있고, 그거를 멤버 변수에 넣으면서 초기화가 가능하다)

---

## 소멸자란 무엇인가?

객체가 소멸할때 호출되는 함수

---

## 객체는 메모리에 어떻게 존재하는가?

연속된 메모리에 존재한다.

만약 객체에 int 변수가 3개 라면 12바이트를 차지하는 객체가 되는... 줄 알았으나?

컴파일러가 메모리 정렬을 위해 padding을 넣을 수 있다고 한다.

그리고 일반적인 멤버 함수는 객체 크기에 포함되지 않는다.(Code영역에서 구현되므로)

---

# ++GPT햄 추가 설명++

## 가상함수

부모 클래스의 포인터나 참조를 통해 자식 객체의 함수를 호출할 때, 실제 객체의 함수를 호출할 수 있도록 하는 함수이다.

```cpp
class Animal
{
public:
    virtual void Speak();
};


class Dog : public Animal
{
public:
    void Speak() override;
};
Dog dog;
Animal* animal = &dog;


animal->Speak(); // Dog::Speak()
```

일반적인 컴파일러 구현에서는 가상 함수를 사용하기 위해 vtable과 vptr을 사용할 수 있다.

vtable → 가상 함수들의 주소를 가지고 있는 테이블
vptr → 객체에서 vtable을 가리키는 포인터

64비트 환경에서는 vptr이 일반적으로 8바이트

가상 함수 자체가 8바이트인 것은 아님

가상 함수가 여러 개 있어도 일반적으로 객체에 vptr이 함수 개수만큼 추가되는 것은 아님

vtable/vptr은 C++ 표준이 구체적인 구현 방식으로 강제하는 것은 아니며, 대표적인 구현 방식임
