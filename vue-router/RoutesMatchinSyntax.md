## 경로 일치 구문
- param 내용을 기반으로 두 경로를 구분해야 하는 경우 이를 구분하기 위해 가장 쉬운 방법은 정적섹션을 추가하는 것입니다.
  ```js
    const routes = [
      // matches /o/3549
      { path: '/o/:orderId' },
      // matches /p/books
      { path: '/p/:productName' },
    ]
  ```
- 이처럼 섹션을 추가하지 않고 표현하고 싶다면 표현식으로 구분이 가능하게 만들수 있습니다.
  ```js
    const routes = [
      // /:orderId -> matches only numbers
      { path: '/:orderId(\\d+)' },
      // /:productName -> matches anything else
      { path: '/:productName' },
    ]
  ```
### 반복 가능한 매개변수
- 여러 섹션이 있는 경로를 일치시키려면 * 나 + 를 사용하여 반복 가능하게 표시해야 합니다.
  ```js
    const routes = [
      // /:chapters -> matches /one, /one/two, /one/two/three, etc
      { path: '/:chapters+' },
      // /:chapters -> matches /, /one, /one/two, /one/two/three, etc
      { path: '/:chapters*' },
    ]
  ```
- 이렇게 표시하면 매개변수는 배열이 제공 되며 경로를 사용할 때 배열을 전달합니다.
  ```js
    // given { path: '/:chapters*', name: 'chapters' },
    router.resolve({ name: 'chapters', params: { chapters: [] } }).href
    // produces /
    router.resolve({ name: 'chapters', params: { chapters: ['a', 'b'] } }).href
    // produces /a/b

    // given { path: '/:chapters+', name: 'chapters' },
    router.resolve({ name: 'chapters', params: { chapters: [] } }).href
    // throws an Error because `chapters` is empty
  ```
- 닫는 괄호 뒤에 사용자 정의 정규식과 결합할 수 있습니다.
  ```js
    const routes = [
      // only match numbers
      // matches /1, /1/2, etc
      { path: '/:chapters(\\d+)+' },
      // matches /, /1, /1/2, etc
      { path: '/:chapters(\\d+)*' },
    ]
  ```
### 엄격한 경로 옵션
- 모든 경로를 기본적으로 대소문자를 구분하지 않으며 후행 슬래시가 있거나 없는 경로와 일치합니다.
  ```js
    const router = createRouter({
      history: createWebHistory(),
      routes: [
        // will match /users/posva but not:
        // - /users/posva/ because of strict: true
        // - /Users/posva because of sensitive: true
        { path: '/users/:id', sensitive: true },
        // will match /users, /Users, and /users/42 but not /users/ or /users/42/
        { path: '/users/:id?' },
      ],
      strict: true, // applies to all routes
    })
  ```
### 선택적 매개변수
- ? 수정자(0또는1)을 사용하여 매개변수를 선택사항으로 표시할 수 있습니다.
  ```js
    const routes = [
    // will match /users and /users/posva
    { path: '/users/:userId?' },
    // will match /users and /users/42
    { path: '/users/:userId(\\d+)?' },
  ]
  ```
  