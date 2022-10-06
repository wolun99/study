## Props
  ### props 선언
  - 명시적인 props 선언을 요구하여 외부에서 컴포넌트를 넘길 때 어떤 속성이 처리가 되어야 하는지 알 수 있다.
  - props는 prosp 옵션을 사용하여 선언한다.
    ```js
      export default{
        props:['example'],
        created(){
          console.log(this.example)
        }
      }
    ```
  - 문자 배열을 사용하여 선언할 수 있음
  - 객체선언 문법으로 사용할 수 있음
    ```js
      export default{
        props:{
          example1 : String,
          example2 : Number
        }
      }
    ```
  - 위 예제와 같이 객체형태로 사용하면 전달하는 데이터가 어떤 타입 형태인지 나타내는 것이 좋다.
  ### props 전달 심화
  - props 이름 케이싱
    - camelCase를 사용하여 긴 속성명을 정함
    - 관례적으로 HTML 송성 표기법과 동일하게 kebab-case로 표기해서 사용해야 한다.
    ```html
      <Example hello-message = "hello"/>
    ```
  - props의 경우 v-bind(:)를 사용하여 동적으로 할당할 수 있다.
  - 어떤 타입의 값도 prop로 전달할 수 있다.
  - 객체의 모든 속성을 props로 전달하려면 v-bind(:)를 사용할 수 있다.
  - props는 부모 속성에서 자식 속성으로 내려주는 하향식 단방향 바인딩이기 때문에 부모 속성이 변경되면 자식 속성이 변경되지만 자식 속성이 변경되도 부모 속성은 변경되지 않습니다.
  - 바인딩된 props는 변경할 수 없지만 객체 또는 배열의 중첩 속성을 변경할 수는 있다.
  ### Prop 유효성 검사
  - props에 타입을 지정할 수 있고 지정한 사항을 충족하지 않으면 콘솔에서 경고를 띄우기 때문에 개발시 유용합니다.
  - 유효성 검사를 지정하려면, props 옵션에 문자열로 구성된 배열대신, 유효성 검사 요구 사항이 있는 객체를 제공합니다.
  ```js
    export default {
      props: {
        // 기본 타입 체크
        //  (`null`과 `undefined`는 모든 타입에서 허용됩니다)
        propA: Number,
        // 여러 타입 허용
        propB: [String, Number],
        // 문자열 필수
        propC: {
          type: String,
          required: true
        },
        // 기본 값을 가지는 숫자형
        propD: {
          type: Number,
          default: 100
        },
        // 기본 값을 가지는 객체
        propE: {
          type: Object,
          // 객체 또는 배열 기본값은 팩토리 함수에서 반환되어야 합니다.
          // 함수는 컴포넌트에서 받은 rawProps를 인자로 받습니다.
          // (rawProps: 부모 컴포넌트에게 받은 props 전체 객체)
          default(rawProps) {
            return { message: '안녕!' }
          }
        },
        // 사용자 정의 유효성 검사 함수
        propF: {
          validator(value) {
            // 값은 다음 문자열 중 하나와 일치해야 합니다.
            return ['성공', '경고', '위험'].includes(value)
          }
        },
        // 기본값이 있는 함수
        propG: {
          type: Function,
          // 기본값 객체나 배열을 정의하는 팩토리 함수가 아니라
          // 기본값으로 사용할 함수입니다.
          default() {
            return 'Default function'
          }
        }
      }
    }
  ```
  - required는 반드시 사용해야 하는가를 나타내는 옵션
  - prop의 타입이 Boolean이 아니고 선택사항인 경우 누락되면 undefined값을 가집니다.
  - prop의 타입이 Boolean 이고 누락된 경우 false가 기본값이 됩니다.
  - prop이 누락 되었거나 선언 된값이 undefined 이고 default 값이 정이 되어 있으면 정의 된 값을 사용합니다.
  - Boolean 타입의 props 특별한 캐스팅 규칙이 있다.
  - 여러 타입의 props를 가지게 선언되면 Boolean에 대한 캐스팅 규칙은 타입 선언 순에 관계없이 적용된다.
  ```js
  export default {
    props: {
      disabled: Boolean
    }
  }
  ```
  ```
  <Example disabled/>
  <Example/>
  ```
  ```js
   export default {
      props: {
        disabled: [Boolean, Number]
      }
    }
  ```