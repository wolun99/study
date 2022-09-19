## Data 속성
- data 옵션은 함수이고 하나의 객체를 반환함
- data 가 반환 하는 객체에 모든 속성이 존재 해야 하는지 확인해야 하며 당장 값을 사용할 수 없다면 null이나 undefined 또는 다른 값을 지정해야 한다.

## Methods 
- methods 옵션은 동작하기 원하는 메서드들을 담은 하나의 객체
- data안의 값을 사용하고 싶다면 this를 사용하여 바인딩하여야함
- ES6의 화살표함수를 사용하면 바인딩이 되지 않기 때문에 methods를 쓸때는 화살표 함수는 사용하지 않아야 함

## 디바운싱과 쓰로틀링
- 디바운싱이나 쓰로틀링의 경우 제공하고 있지 않다
  > 디바운싱 : 연이어 호출되는 함수들 중 마지막 함수(또는 제일 처음)만 호출하도록 하는것\
  쓰로틀링 :마지막 함수가 호출된 후 일정 시간이 지나기 전에 다시 호출되지 않도록 하는 것