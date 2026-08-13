# const

## const란 무엇인가?

const는 변수를 상수화시키는 키워드다.

## const 변수는 무엇을 제한하는가?

const 변수는 변수의 값 변경을 제한한다.

## const와 포인터를 함께 사용하면 어떤 경우들이 있는가?

const int*
int * const
const int * const

cppPointer.md 문서 참고

## const int*와 int* const의 차이는?

전자는 값 변경 X
후자는 주소 변경 X

## const int* const는 무엇을 의미하는가?

값과 주소 변경 모두 X

## 함수 매개변수에서 const를 사용하는 이유는?

함수에서 직접 값이 변경되는 것을 방지하기 위해

(원본 데이터 변경 방지)
