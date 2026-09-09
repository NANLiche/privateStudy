# 9/9 — shared_ptr

## shared_ptr이란 무엇인가?

동적 할당된 메모리에 대해 **공동 소유권**을 가질 수 있게 하는 스마트 포인터

## shared_ptr은 왜 필요한가?

더 이상 객체를 가리키는 포인터(소유권을 가진 포인터)가 없다면, 메모리를 자동으로 해제하여 **메모리 누수를 방지**하기 위해.

## shared_ptr의 소유권은 어떻게 관리되는가?

내부적으로 **제어 블록(Control Block)**이라는 메모리 공간을 만들어, 이 제어 블록 안에 **참조 카운트**를 두어 객체의 소유권을 관리한다.

## shared_ptr의 참조 카운트란 무엇인가?

해당 객체를 **소유하고 있는 `shared_ptr`의 개수**

## shared_ptr의 객체 수명은 어떻게 결정되는가?

**참조 카운트가 0이 되는 순간 객체가 삭제되며, 이 과정에서 객체의 소멸자가 호출된다.**

## shared_ptr은 어떻게 복사되는가?

`shared_ptr`을 복사하면 **참조 카운트가 1 증가**하며 복사된다.

## shared_ptr과 unique_ptr의 차이는?

`unique_ptr`은 **이동만 가능**한 반면,
`shared_ptr`은 **복사가 가능**하다.

또한 `shared_ptr`은 제어 블록을 사용하기 때문에 **`unique_ptr`보다 메모리 및 성능 오버헤드가 크다.**

## shared_ptr의 단점이나 주의할 점은?

두 객체가 서로를 `shared_ptr`로 가리키면 **순환 참조(Circular Reference)**가 발생하여 참조 카운트가 영원히 0이 되지 않을 수 있다.

이 경우 객체가 삭제되지 않아 **메모리 누수**가 발생할 수 있다.

## 사용법

```
std::shared_ptr<int> ptr = std::make_shared<int>(10);

std::shared_ptr<int> ptr2 = ptr;
```

ptr.use_count() = 참조카운트 수 반환 // 위 코드에서는 2
