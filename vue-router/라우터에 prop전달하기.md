## 라우터에 prop 전달하기

- $route를 사용하면 특정 URL에서만 사용할 수 있어 재사용성이 떨어지게 됩니다.
- 이러한 경우 props 옵션을 사용하여 분리할 수 있습니다.
  ```js
  const User = {
    template: '<div>User {{ $route.params.id }}</div>',
  };
  const routes = [{ path: '/user/:id', component: User }];
  ```
  ```js
  const User = {
    // 매개변수와 같은이름의 prop을 추가해야합니다.
    props: ['id'],
    template: '<div>User {{ id }}</div>',
  };
  const routes = [{ path: '/user/:id', component: User, props: true }];
  ```
- 위와 같이 대체할 수 있습니다.

## Boolean mode

- props가 true일 경우 route.params를 component prop으로 구성할 수 있습니다.

## 명명된 뷰

- 명명된 뷰의 경우 각각의 뷰에 props 옵션을 정의해야 합니다.
  ```js
  const routes = [
    {
      path: '/user/:id',
      components: { default: User, sidebar: Sidebar },
      props: { default: true, sidebar: false },
    },
  ];
  ```

## 객체

- prop가 객체인 경우 컴포넌트 props를 있는 그대로 사용합니다.
- props가 정적일때 유용합니다.
  ```js
  const routes = [
    {
      path: '/promotion/from-newsletter',
      component: Promotion,
      props: { newsletterPopup: false },
    },
  ];
  ```

## 함수

- props를 반환하는 함수를 만들수 있습니다.
- 이를 통해 매개변수를 다른유형으로 보낼수 있고, 정적 값을 경로 기반 값과 결합하는 작업을 수행할 수 있습니다.
  ```js
  const routes = [
    {
      path: '/search',
      component: SearchUser,
      props: (route) => ({ query: route.query.q }),
    },
  ];
  ```
- props는 무상태로 유지해야 하고 라우터가 변경될 때만 변경되어야 합니다.
- state에 prop을 정의해야 하는 경우 wrapper component를 사용하여 vue의 반응성을 유지해야 합니다.
