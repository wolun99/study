## Number 생성자 함수
- Number 객체는 생성자 함수 객체이다.
- Number 생성자 인수로 숫자가 아닌 인수를 넣으면 강제로 변환하여 NaN을 내부 슬롯에 할당한 Number 래퍼 객체로 생성한다.
- 명시적으로 타입변환을 하는데 사용하기도 한다.

## Number 프로퍼티
1. Number.EPSILON
    - ES6에서 도입된 것으로 1과 1보다 큰 수자중에서 가장 작은 숫자와의 차이와 같다
    - 부동소수점으로 인해 발생하는 오차를 해결하기 위해 사용한다.
2. Number.MAX_VALUE
    - 자바스크립트에서 표현할 수 있는 가장 큰 양수값(1.7976931348623157 * 10<sup>308</sup>)이다.
3. Number.MIN_VALUE
    - 자바스크립트에서 표현할 수 있는 가장 작은 양수 값(5*10<sup>-324</sup>)이다.
4. Number.MAX_SAFE_INTEGER
    - 자바스크립트에서 안전하게 표현할 수 있는 가장 큰정수값(9007199254740991)이다.
5. Number.MIN_SAFE_INTEGER
    - 자바스크립트에서 안전하게 표현할 수 있는 가장 작은 정수값(-9007199254740991)이다.
6. Number.POSITIVE_INFINITY
    - 숫자값 Infinity와 같다
7. Number.NEGATIVE_INFINITY
    - 숫자값 -Infinity와 같다
8. Number.NaN
    - 숫자가 아님을 나타내는 숫자값
## Number메서드
1. Number.isFinite
    - 인수로 전달된값이 정상적인 유한수 인지 검사하여 불리언 값으로 표현
    - 인수가 NaN이면 항상 false를 반환한다.
2. Number.isInteger
    - 인수로 전달된 숫자값이 정수인지 검사하여 불리언 값으로 반환한다. 검사하기 전에 인수를 숫자로 암묵적 타입 변환하지 않는다.
3. Number.isNaN
    - 인수로 전달된 숫자값이 NaN인지 검사하여 불리언값으로 반환
    - 암묵적 타입변환은 하지않고 숫자가 아닌 인수가 주어졌을대 값은 언제나 false이다.
4. Number.isSafeInteger
    - 인수로 전달한 숫자값이 안전한 정수인지 검사하여 불리언값으로 반환
5. Number.prototype.toExponential
    - 숫자를 지수 표기법으로 변환하여 문자열로 반환한다. 
    - 숫자 리터럴과 함께 사용하면 에러가 발생한다.
6. Number.prototype.toFixed
    - 숫자를 반올림하여 문자열로 반환한다. 
    - 반올림하는 소수점이하 자릿수를 0~20 사이의 정수값을 인수로 전달할 수 있다.
    - 생략하면 기본값은 0이다.
7. Number.prototype.toPrecision
    - 인수로 전달받은 전체 자릿수까지 유효하도록 나머지 자릿수를 반올림하여 문자열로 반환한다.
    - 자릿수는 0~21 사이의 정수값을 인수로 전달할수 있다
8. Number.prototype.toString
    - 숫자를 문자열로 변환하여 반환한다. 진법을 나타내는 2~36사이의 정수값을 인수로 전달할 수 있다.
    - 기본값은 10진법이 지정된다.
