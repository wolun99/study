## 동적 경로 일치
- 주어진 패턴으로 경로를 도일한 구성요소에 매핑해야하는데, 사용자 ID에 따른 다른 구성이 필요한 경우 vue router에서 경로를 동적 세그먼트를 사용해 이를 나타내는데 이를 param이라고 합니다.

  ```js
    const user ={
      template : '<div>User</div>'
    }

    const routes = [
      {path:'/users/:id, component : User'}
    ]
  ```
- 매개변수는 콜론으로 표시하며 :이름 경로가 일치하면 해당 매개변수 this.$route.param의 값이 모든 구성요소에서 노출됩니다.
  ```js
    const User = {
      template : '<div>User {{$route.params.id}}</div>'
    }
  ```
- 동일 경로에 여러가지 매개변수를 매핑할 수 있습니다.
- $route.params 객체는 $route 등과 같은 유용한 정보를 노출합니다.

### 매개변수 변경에 반응하기
- 매개변수가 있는 경로를 사용할 때 주의할 점은 이동시 동일한 구성요소 인스턴스가 재사용된다는 것입니다.
- 이러한 점은 새로 인스턴스를 만드는 점 보다 효율적이지만 수명 주기 hook이 호출되지 않습니다.

  ```js
    const User = {
      template: '...',
      created() {
        this.$watch(
          () => this.$route.params,
          (toParams, previousParams) => {
            // react to route changes...
          }
        )
      },
    }
  ```
- 변경 사항에 반응하기 위하여 위와 같은 방법으로 반응성을 나타낼 수 있습니다.
### 모든 경로/404 에러 경로
- 일반 매개변수는 문자만 일치 시키지만 무엇이든 일치시키려면 param바로 뒤의 괄호 안에 정규식을 추가하여 표현할 수 있습니다.
  ```js
    const routes = [
      { path: '/:pathMatch(.*)*', name: 'NotFound', component: NotFound },
      { path: '/user-:afterUser(.*)', component: UserGeneric },
    ]
  ```
- 괄호 사이에 사용자 정의 정규 표현식 pathMatch를 사용하고 선택적으로 반복 가능하게 표현 할 수 있습니다.
### 고급 매칭 패턴
- 라우터는 자체 경로 일치구문을 사용하여 표현하므로 선택적 매개변수, 0개 이상/하나 이상의 요구 사항, 사용자 정의 정규식 패턴과 같은 많은 고급 일치 패턴을 지원합니다.