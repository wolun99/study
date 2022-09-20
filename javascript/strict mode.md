## strict mode
- 자바스크립트의 언어의 문버을 엄격하게 적용하여 오류 발생키리 가능성이 높거나 최적화 작업에 문제를 일으킬 수 있는 코드에 대해 에러를 발생시킨다.
## strict mode의 적용
- 선두에 'use strict';를 추가한다.
## strict mode를 전역에 적용하는 것은 피하자
- strict mode 스크립트와 non-strict mode 스크립트를 혼용하는 것은 오류를 발생시킬 수 있기 때문에 전역에 적용하는 것은 바람직 하지않다.
## 함수단위로 strict mode를 적용하는 것도 피하자
## strict mode가 발생시키는 에러
1. 암묵적 전역\
    선언하지 않은 젼수를 참조하면 ReferenceError가 발생한다.
2. 변수, 함수 , 매개변수의 삭제\
    delete 연산자로 변수, 함수, 매개변수를 삭제하면 SyntaxError가 발생한다.
3. 매개변수 이름의 중복\
    중복된 매개변수 이름을 사용하면 SyntaxError가 발생한다.
4. with 문의 사용\
    with 문을 사용하면 SyntaxError가 발생한다.
## strict mode 적용에 의한 변화
1. 일반 함수의 this\
    일반 함수로서 호출하면 this에 undefined가 바인딩 된다.
2. arguments 객체\
    매개변수에 전달된 인수를 재할당하여 변경해도 arguments 객체에 반영되지 않는다.
