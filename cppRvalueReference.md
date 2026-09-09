# 8/29 — Rvalue Reference

## Rvalue란 무엇인가?

객체의 이름이나 주소를 통해 식별할 수 없는 값

## Lvalue와 Rvalue의 차이는?

Lvalue는 Rvalue와 달리 명시적인 메모리 주소와 이름을 가진다.

## Rvalue Reference란 무엇인가?

Rvalue를 참조할 수 있도록 만들어진 새로운 참조 타입

## `&&`는 무엇을 의미하는가?

Rvalue Reference를 선언하는 기호

```cpp
int && a = 10;
```

## Rvalue Reference가 Move Semantics와 어떤 관계가 있는가?

Rvalue Reference를 이용하면 Rvalue를 참조할 수 있으며,

이를 통해 이동 생성자나 이동 대입 연산자가 호출되어 객체의 자원을 복사하지 않고 이동시킬 수 있다.

## 복사 생성자와 이동 생성자의 차이는?

복사 생성자는 객체를 위해 메모리를 새로 할당하여 생성하지만
이동 생성자는 원본 자원의 소유권을 넘겨받는다.

## 이동 생성자는 언제 호출되는가?

새로운 객체를 초기화할 때, 우변에 Rvalue가 오거나,

`std::move()` 함수를 통해 Lvalue를 Rvalue로 바꾸어 넘겨줄 때

## 이동 대입 연산자는 무엇인가?

이미 생성되어 있는 객체에 Rvalue를 대입할 때 호출되는 연산자

기존에 자신이 가지고 있던 자원을 먼저 해제하고, 대입되는 Rvalue의 자원 소유권을 넘겨받는다.

## 예시 코드

```cpp
#include <iostream>
#include <utility> // std::move

class MyString {
private:
    char* data; // 동적 할당 자원이라고 가정

public:
    // 1. 기본 생성자
    MyString(): data(nullptr) {
        std::cout << "기본 생성자 호출\n";
    }

    // 2. 복사 생성자 (Lvalue가 들어올 때)
    MyString(const MyString& other) {
        std::cout << "복사 생성자 호출 (Deep Copy 발생!)\n";
        // 실제로는 여기서 메모리를 새로 할당(new)하고 other의 데이터를 복사함
    }

    // 3. 이동 생성자 (Rvalue가 들어올 때) - noexcept 권장
    MyString(MyString&& other) noexcept {
        std::cout << "이동 생성자 호출 (자원 소유권 이전!)\n";
        this->data = other.data; // 자원 가로채기 (Shallow Copy)
        other.data = nullptr;    // 원본은 빈 상태로 만들기
    }

    // 4. 이동 대입 연산자
    MyString& operator=(MyString&& other) noexcept {
        std::cout << "이동 대입 연산자 호출\n";
        if (this != &other) {
            delete[] this->data;     // ★ 핵심: 내가 원래 쥐고 있던 자원 먼저 해제
            this->data = other.data; // 새 자원 가로채기
            other.data = nullptr;    // 원본 비우기
        }
        return *this;
    }
};

int main() {
    std::cout << "--- 1. 객체 생성 ---\n";
    MyString a;                 // 기본 생성자

    std::cout << "\n--- 2. Lvalue 복사 ---\n";
    MyString b = a;             // a는 Lvalue이므로 '복사 생성자' 호출

    std::cout << "\n--- 3. 강제 Rvalue 변환(std::move) ---\n";
    MyString c = std::move(a);  // std::move로 Rvalue 캐스팅 -> '이동 생성자' 호출

    std::cout << "\n--- 4. 임시 객체(Rvalue) 대입 ---\n";
    MyString d;                 // 기본 생성자
    d = MyString();             // MyString()은 이름 없는 임시 객체(Rvalue) -> '이동 대입 연산자' 호출

    return 0;
}
```
