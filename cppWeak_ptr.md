# 9/9 — weak_ptr

## weak_ptr이란 무엇인가?

`shared_ptr`이 관리하는 객체를 참조할 수는 있지만, 객체의 소유권은 가지지 않는 스마트 포인터

## weak_ptr은 왜 필요한가?

주로 `shared_ptr`의 가장 큰 단점인 **순환 참조 문제를 해결**하기 위해 사용.

객체의 수명에 관여하지 않으면서 해당 객체가 살아있는지 확인하고 싶을 때 필요하다.

## weak_ptr은 객체의 소유권을 가지는가?

가지지 않는다.

## weak_ptr과 shared_ptr의 관계는?

`weak_ptr`은 `shared_ptr`이나 다른 `weak_ptr`로부터 생성하여 관찰할 수 있다.

객체에 실제로 접근하려면 `lock()` 메서드를 호출해야 하며,

객체가 살아있다면 임시 `shared_ptr`을 반환하고, 이미 소멸했다면 비어있는 `shared_ptr`을 반환한다.

## 순환 참조란 무엇인가?

A와 B `shared_ptr`이 서로를 가리켜서 소멸되지 않는 상태.

## 순환 참조가 발생하면 어떤 문제가 생기는가?

메모리 누수가 발생한다.

## weak_ptr은 순환 참조를 어떻게 해결하는가?

A와 B 중 한쪽을 `weak_ptr`로 바꿨을 때, B를 소유하는 참조 카운터가 0이 되어 정상적으로 메모리가 정리된다.

---

## 예시코드 및 부연설명

제어 블록 안에는
**강한 참조 카운터**와
**약한 참조 카운터**가 있다.

강한 참조 카운터가 0이 되면 해당 객체는 `shared_ptr`의 RAII 구조에 의해 소멸한다.

약한 참조 카운터는 `weak_ptr`의 참조를 카운트한다.

제어 블록은 강한 참조 카운터와 약한 참조 카운터가 모두 0이 되어야 소멸한다.

강한 참조 카운터가 0이 되어 소멸한 객체를 `weak_ptr`로 관찰할 수 있는 이유가 이것이다.

```cpp
#include <iostream>
#include <memory>

struct Node {
    std::shared_ptr<Node> next; // 강한 참조
    std::weak_ptr<Node> prev;   // 약한 참조 (순환 참조 방지!)

    ~Node() { std::cout << "Node 소멸\n"; }
};

int main() {
    auto nodeA = std::make_shared<Node>();
    auto nodeB = std::make_shared<Node>();

    nodeA->next = nodeB; // A -> B (강한 참조 카운트 증가)
    nodeB->prev = nodeA; // B -> A (약한 참조이므로 카운트 증가 X)

    // B에서 A에 접근하고 싶을 때 lock() 사용
    if (std::shared_ptr<Node> tempA = nodeB->prev.lock()) {
        std::cout << "A가 아직 살아있습니다. 접근 가능!\n";
    } else {
        std::cout << "A가 이미 소멸되었습니다.\n";
    }

    // main 함수가 종료될 때 nodeA와 nodeB 모두 정상적으로 소멸됨 (메모리 누수 없음)
    return 0;
}
```
