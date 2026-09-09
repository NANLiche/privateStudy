# 8/28 — Move Semantics

## 1. Move Semantics란 무엇인가?

객체의 자원을 복사하는 대신 이동시키는 메커니즘

## 2. Move Semantics는 왜 필요한가?

불필요한 복사를 방지하여 오버헤드를 줄이기 위해서

## 3. 복사와 이동은 무엇이 다른가?

**복사:** 새로운 메모리를 할당하여 원본의 데이터를 복사(대입)한다.

**이동:** 원본이 가진 자원을 가져와 새 변수에 옮기고 원본 객체의 자원은 유효하지만 비어있는 상태로 만든다.

## 4. 객체를 복사할 때 어떤 비용이 발생할 수 있는가?

새로운 메모리를 할당하는데 시간과 연산에서 비용이 발생한다.

## 5. 객체를 이동한다는 것은 무엇을 의미하는가?

기존 객체가 가진 자원을 새로운 객체로 이전하고, 기존 객체의 자원은 유효하지만 비어있는 상태가 된다.

## 6. Move Semantics와 자원 소유권은 어떤 관계가 있는가?

Move Semantics가 곧 자원 소유권의 이전을 통한 이동 방법이라고 할 수 있다. 기존 사용하던 메모리를 넘겨줌으로서 오버헤드를 방지한다.

## 7. Move Semantics는 언제 유용한가?

* 함수에서 메모리 비용이 큰 객체를 반환할 때.
* `std::vector` 같은 컨테이너에 요소를 추가하거나, 컨테이너의 크기가 재할당될 때.
* 두 변수의 값을 교환할 때.

## 8. Move Semantics와 unique_ptr은 어떤 관계가 있는가?

`unique_ptr`을 다른 함수로 넘기거나 컨테이너에 넣을 때는 오직 Move Semantics를 통해서만 소유권을 넘겨줄 수 있다.

---

## 예시 코드

```cpp
#include <iostream>
#include <vector>
#include <string>

int main() {
    std::string str1 = "매우 긴 문자열 데이터..."; 
    std::string str2 = "또 다른 긴 문자열 데이터...";

    // 1. 복사(Copy)를 통한 방식 (C++11 이전)
    // 값을 3번 복사함. 문자열 전체를 복사하는 비용이 3번 필요.
    /*
    std::string temp = str1;
    str1 = str2;
    str2 = temp;
    */

    // 2. 이동(Move)을 통한 방식 (C++11 이후 모던 C++)
    // 데이터 복사 없이 기존 자원을 새로운 객체로 이전함
    std::string temp = std::move(str1); // str1의 자원을 temp로 이동 (str1은 비워짐)
    str1 = std::move(str2);             // str2의 자원을 str1로 이동 (str2는 비워짐)
    str2 = std::move(temp);             // temp의 자원을 str2로 이동

    return 0;
}
```
