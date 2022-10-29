## 중첩 경로

- vue router를 이용하면 중첩된 경로를 구성할 수 있습니다.
- 중첩된 경로를 사용하려면 children 옵션을 사용하여 구성할 수 있습니다.
  ```js
  const routes = [
    {
      path: 'user/:id',
      component: User,
      children: [
        {
          path: 'profile',
          component: UserProfile,
        },
        {
          path: 'write',
          component: UserWrite,
        },
      ],
    },
  ];
  ```
- 중첩경로는 path앞에 /를 사용하여 구별합니다.
- 빈 경로를 사용하여 중첩경로를 제공할 수 있습니다
  ```js
  const routes = [
    {
      path: 'user/:id',
      component: User,
      children: [{ path: '', component: UserHome }],
    },
  ];
  ```

## 중첩된 경로 명명

- Named Routes를 다룰땐 자식 라우트에 name을 사용하여 표현합니다.
  ```js
  const routes = [
    {
      path: '/user/:id',
      component: User,
      children: [{ path: '', name: 'user', component: UserHome }],
    },
  ];
  ```
- 위와 같이 항상 중첩경로를 표현할 수 있습니다.
- 중첩경로를 표시하지 않고 이동하려할 때 부모 경로의 이름을 지정할 수 있지만 페이지를 리로드하면 항상 중첩된 자식 라우트의 내용이 표시됩니다.
  ```js
      const routes = [
    {
      path: '/user/:id',
      name: 'user-parent'
      component: User,
      children: [{ path: '', name: 'user', component: UserHome }],
    },
  ]
  ```
