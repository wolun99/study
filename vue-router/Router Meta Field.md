## Route Meta Fields

- 경로에 접근하기전 경로에 임의의 정보를 추가할 수 있습니다.
- 이는 경로 위치 및 네비게이션 가드에서 접근할 수 있으며 메타 속성을 통하여 적용할 수 있습니다.
  ```js
  const routes = [
    {
      path: '/posts',
      component: PostsLayout,
      children: [
        {
          path: 'new',
          component: PostsNew,
          // 인증된 사용자만 게시글을 작성할 수 있습니다.
          meta: { requiresAuth: true },
        },
        {
          path: ':id',
          component: PostsDetail,
          // 누구나 읽을수 있습니다.
          meta: { requiresAuth: false },
        },
      ],
    },
  ];
  ```
- 경로의 구성의 각 경로 객체를 경로 레코드라 합니다. 이는 중첩될 수 있습니다. 경로가 일치하면 둘 이상의 경로 레코드가 잠재적으로 같을 수 있습니다. 경로와 일치하는 모든 경로 레코드는 $route.matched 배열로 $route의 객체에 노출됩니다.
- 모든 메타 필드를 확인하기 위해 해당 배열을 반복할 수 있지만 부모에서 자식으로 모든 메타 필드를 병합하는 $route.meta를 이용하여 간단하게 작성할 수 있습니다.
  ```js
  router.beforeEach((to, from) => {
    // 모든레코드 경로를 확인하는대신에
    // 몇명 경로를 매치합니다.(record => record.meta.requiresAuth)
    if (to.meta.requiresAuth && !auth.isLoggedIn()) {
      // 이 라우트는 인증이 됬는지 확인하고 그렇지 않을 경우 login페이지를 리다이렉트합니다.
      return {
        path: '/login',
        // 다음에 다시올 경로를 저장합니다.
        query: { redirect: to.fullPath },
      };
    }
  });
  ```
