### Prop 드릴링
- 부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달할 때 props를 사용하는데 컴포넌트의 트리가 있고 그 깊이가 깊을때 prop이 필요하지 않는 컴포넌트들도 선언하고 전달을 해야하는데 이러한 과정을 prop 드릴링이라고 합니다.
- provide와 inject로 이러한 드릴링을 해결할 수 있습니다.
## Provide
- provide 옵션을 사용하여 하위 항목에 데이터를 전달할 수 있습니다.
  ```js
    export default {
      provide: {
        message: '안녕!'
      }
    }
  ```
- 인스턴스별로 상태를 제공해야 하는 경우, provide는 함수 값을 사용합니다.
  ```js
    export default {
      data() {
        return {
          message: '안녕!'
        }
      },
      provide() {
        // 함수 구문을 사용하여 `this`에 접근할 수 있습니다.
        return {
          message: this.message
        }
      }
    }
  ```
- 주입된 값은 반응형이 아니기 때문에 다시 렌더링이 발생하지 않습니다.
- 다음과 같이 사용할 수도 있습니다.
  ```js
  import { createApp } from 'vue'

  const app = createApp({})
  app.provide(/* 키 */ 'message', /* 값 */ '안녕!')
  ```
- 이렇게 사용하면 전역으로 선언하는 것이기 때문에 어디서든 사용할 수 있습니다.
## Inject
- inject 옵션을 사용하여 부모 컴포넌트에 데이터를 주입할 수 있습니다.
  ```js
    export default {
      inject: ['message'],
      created() {
        console.log(this.message) // 주입된 값
      }
    }
  ```
- inject는 컴포넌트 자체 보다 먼저 구성되므로 data()에서 주입된 속성에 접근할 수 있습니다.
  ```js
    export default {
      inject: ['message'],
      data() {
        return {
          // 주입된 값을 기반으로 하는 초기 데이터
          fullMessage: this.message
        }
      }
    }
  ```
- 다른 로컬키를 사용하여 속성을 주입하려면 객체 구문을 사용해야 합니다.
  ```js
    export default {
      inject: {
        /* 로컬 키 */ localMessage: {
          from: /* 주입된 키 */ 'message'
        }
      }
    }
  ```
- 주입시 필수적으로 값을 사용하지 않을 것이면 default를 사용하여 기본 값을 지정할 수 있다.
  ```js
    export default {
      // 주입에 대한 기본값을 선언할 때
      // 객체 구문이 필요합니다.
      inject: {
        message: {
          from: 'message', // 주입 시 키와 같은 이름을 사용하는 경우 선택사항입니다.
          default: '이것은 기본 값 문자열 입니다.'
        },
        user: {
          // 생성하는 데 비용이 많이 드는 기본이 아닌 값 또는 컴포넌트 인스턴스마다
          // 고유해야 하는 값에 대해 팩토리 함수를 사용합니다.
          default: () => ({ name: '철수' })
        }
      }
    }
  ```
## 반응형으로 만들기
- 반응형으로 만들기 위해서는 computed함수를 사용하여 계산된 속성을 제공합니다.
  ```js
    import { computed } from 'vue'

    export default {
      data() {
        return {
          message: '안녕!'
        }
      },
      provide() {
        return {
          // 계산된 속성을 명시적으로 제공
          message: computed(() => this.message)
        }
      }
    }
  ```

### 심볼키 사용하기
- 대규모 앱작업이나 다른 개발자와 협업할 경우 잠재적 충돌을 피하기 위해 Symbol을 공개키로 지정하는 것이 좋습니다
  ```js
    export const myInjectionKey = Symbol()
  ```
  ```js
    // 제공하는 곳의 컴포넌트에서
    import { myInjectionKey } from './keys.js'

    export default {
      provide() {
        return {
          [myInjectionKey]: {
            /* 제공할 데이터 */
          }
        }
      }
    }
  ```
  ```js
    // 주입되는 곳의 컴포넌트에서
    import { myInjectionKey } from './keys.js'

    export default {
      inject: {
        injected: { from: myInjectionKey }
      }
    }
  ```