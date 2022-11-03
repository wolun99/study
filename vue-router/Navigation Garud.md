## 네비게이션 가드

- Vue router에서 제공하는 탐색하거나 리다이렉션을 하거나 취소하여 라우터를 보호하는데 사용됩니다.
- 전역, 경로별 또는 구성요소 등으로 사용할 수 있습니다.

### 전역 비포 가드

- 전역 비포 가드를 사용하기 위해 router.beforEach를 사용합니다.

  ```js
    const router = createRouter({ ... })

    router.beforeEach((to, from) => {
      // ...
      // 경로로 가지 못하게 하기위해선 false를 사용합니다.
      return false
    })
  ```

- 경로 탐색이 실행될 때마다 호출되기 전에 전역으로 사용합니다.
- 비동기식으로 사용할 수 있고 조건이 해결되기 전에 탐색이 보류 중인걸로 간주합니다.
- 모든 가드는 두가지의 매개변수를 갖습니다.
  - to : 경로의 목표가 되는 정형화된 경로
  - from : 현재 경로 위치
- 선택적으로 다음의 값을 가져갈 수 있습니다.
  - false : 현재 탐색을 취소하고 from의 경로 URL로 이동합니다.
  - A Router Location : router.push()를 사용하는 것처럼 다른 위치로 리다이렉션 합니다, 몇몇 옵션을 사용할 수 있고 현재 탐색이 삭제되고 동일한 from 으로 새 탐색이 생성됩니다.
  ```js
  router.beforeEach(async (to, from) => {
    if (
      // 사용자가 인증되었는지 확인
      !isAuthenticated &&
      // 무한 리다이렉션 금지
      to.name !== 'Login'
    ) {
      // user페이지로 리다이렉션
      return { name: 'Login' };
    }
  });
  ```
- 예상치 못한 에러가 발생한 경우 실행을 취소하고 router.onError()를 통해 등록된 모든 콜백을 호출합니다.
- 비동기 함수 및 promiss 가 동일한 방식으로 동작합니다.

### 세번째 옵셔널 인수 next

- 이전 버전에서 세번째 인수를 사용할 수 있었지만 이것은 일반적인 실수의 원인이였고 제거하였지만 여전히 지원이 됩니다.
- 세번째 인수를 전달할 경우 주어진 경로에서 next를 정확하게 한번 호출해야 합니다.
- 두 번 이상 나타낼 수 있지만 논리적 경로가 겹치지 않는 경우만 가능합니다.
  ```js
  // BAD
  router.beforeEach((to, from, next) => {
    if (to.name !== 'Login' && !isAuthenticated) next({ name: 'Login' });
    // 사용자가 인증되지 않는경우 next가 두번 호출됩니다.
    next();
  });
  ```
  ```js
  // GOOD
  router.beforeEach((to, from, next) => {
    if (to.name !== 'Login' && !isAuthenticated) next({ name: 'Login' });
    else next();
  });
  ```

### Global Resolve Guards

- router.beforeResolve를 사용하여 전역 가드를 등록할 수 있습니다.
- router.beforeEach와 유사하지만 탐색이 되기전 구성 요소 내 모든 가드 및 비동기 경로 구성 요소가 해결된 후 해결 가드가 호출됩니다.
  ```js
  router.beforeResolve(async (to) => {
    if (to.meta.requiresCamera) {
      try {
        await askForCameraPermission();
      } catch (error) {
        if (error instanceof NotAllowedError) {
          // 에러를 핸들리하고 네비게이션을 취소합니다.
          return false;
        } else {
          // 예기치 않은 오류 발생시, 취소하고 오류를 처리기에 전달
          throw error;
        }
      }
    }
  });
  ```
- router.beforeResolve는 사용자가 페이지에 들어갈 수 없을때 피하고 싶은 작업을 수행하기에 이상적입니다.

### 전역 에프터 훅

- 전역 에프터 훅을 등록할 수 있지만 next function을 실행하지않고 탐색에 영향을 주지 않습니다.
  ```js
  router.afterEach((to, from) => {
    sendToAnalytics(to.fullPath);
  });
  ```
- 분석, 페이지 제목 변경, 페이지 발표와 같은 접근성 기능 및 기타 여러 작업에 유용합니다.
- 탐색에 실패하면 세번째 인수를 반영합니다.
  ```js
  router.afterEach((to, from, failure) => {
    if (!failure) sendToAnalytics(to.fullPath);
  });
  ```

### 루트별 가드

- 경로의 객체에서 beforeEnter가드를 직접 정의할 수 있습니다.
  ```js
  const routes = [
    {
      path: '/users/:id',
      component: UserDetails,
      beforeEnter: (to, from) => {
        // 네비게이션을 실행하지않음
        return false;
      },
    },
  ];
  ```
- beforeEnter 가드는 경로에 들어갈 때만 실행하고 매개변수, 쿼리 또는 해시가 변경될 때 실행하지 않습니다.
- 또한 배열을 전달할 수 있습니다. 이는 재사용할 때 유용합니다.

  ```js
  function removeQueryParams(to) {
    if (Object.keys(to.query).length)
      return { path: to.path, query: {}, hash: to.hash };
  }

  function removeHash(to) {
    if (to.hash) return { path: to.path, query: to.query, hash: '' };
  }

  const routes = [
    {
      path: '/users/:id',
      component: UserDetails,
      beforeEnter: [removeQueryParams, removeHash],
    },
    {
      path: '/about',
      component: UserDetails,
      beforeEnter: [removeQueryParams],
    },
  ];
  ```

### 인컴포넌트 가드

- 컴포넌트의 루트에 직접 네비게이션 가드를 정의할 수 있습니다.

#### Option API를 사용

- 컴포넌트의 루트에 beforeRouteEnter,beforeRouteUpdate, beforeRouteLeave를 옵션으로 추가할 수 있습니다.
  ```js
  const UserDetails = {
    template: `...`,
    beforeRouteEnter(to, from) {
      // 구성요소를 경로가 확인되기 전에 호출됩니다.
      // 가드가 호출될 때 아직 생성되지 않았기 때문에
      // 컴포넌트 인스턴스 this에 접근권한이 없습니다.
    },
    beforeRouteUpdate(to, from) {
      // 이 구성 요소를 렌더링하는 경로가 변경되었지만 이 구성 요소가 새 경로에서 재사용될 때 호출됩니다.
      // 예를 들어 `/users/:id` 매개변수가 있는 경로가 주어지면 `/users/1`과 `/users/2` 사이를 탐색할 때
      // 동일한 `UserDetails` 구성 요소 인스턴스가 재사용되며 이 후크가 호출될 때 호출됩니다.
      // 이러한 일이 발생하는 동안 구성 요소가 마운트되기 때문에 탐색 가드는 'this' 구성 요소 인스턴스에 액세스할 수 있습니다.
    },
    beforeRouteLeave(to, from) {
      // 이 구성 요소를 렌더링하는 경로가 이동하려고 할 때 호출됩니다.
      // `beforeRouteUpdate`와 마찬가지로 `this` 구성 요소 인스턴스에 액세스할 수 있습니다.
    },
  };
  ```
- beforeRouteEnter 가드는 새 입력 구성 요소가 생성되지 않았을 때 호출 되기 때문에 이에 접근할 수 없습니다.
- 그러나 콜백을 전달하여 인스턴에 접근할 수 있습니다. 탐색을 확인하면 콜백이 호출되고 인스턴스가 인수로 콜백에 전달됩니다.
  ```js
    beforeRouteEnter (to, from, next) {
      next(vm => {
        // vm인스턴에 접근할수 있습니다.
      })
    }
  ```
- beforeRouteEnter는 콜백 전달을 지원하는 유일한 가드입니다.
- leave guard는 실수로 경로를 떠나는 것을 방지하는데 사용합니다.
- false를 반환하여 취소합니다.
  ```js
    beforeRouteLeave (to, from) {
      const answer = window.confirm('Do you really want to leave? you have unsaved changes!')
      if (!answer) return false
    }
  ```

### composition API를 사용할 때

- 각각 onBeforeRouteUpdate 및 onBeforeRouteLeave를 통해 업데이트를 추가하고 가드를 떠날 수 있습니다.
