## transition

- 라우터에서 애니메이션을 적용하기 위해서는 v-slot API를 사용해야 합니다.
  ```html
  <router-view v-slot="{ Component }">
    <transition name="fade">
      <component :is="Component" />
    </transition>
  </router-view>
  ```
- 모든 transition API는 이렇게 동작합니다.

## Per-Route Transition

- 각 경로의 컴포넌트에 각각 다른 transition을 사용하기 위해서는 메타필드와 동적name을 결합하여 나타냅니다.
  ```js
  const routes = [
    {
      path: '/custom-transition',
      component: PanelLeft,
      meta: { transition: 'slide-left' },
    },
    {
      path: '/other-transition',
      component: PanelRight,
      meta: { transition: 'slide-right' },
    },
  ];
  ```
  ```html
  <router-view v-slot="{ Component, route }">
    <!-- 커스텀transition을 사용하고 'fade'로 대체합니다. -->
    <transition :name="route.meta.transition || 'fade'">
      <component :is="Component" />
    </transition>
  </router-view>
  ```

### Route-Based Dynamic Transition

- 대상 경로와 현재 경로간의 관계를 기반으로 동적으로 사용할 route를 결정할 수 있습니다.
  ```html
  <!-- 동적transition name을 사용한 경우 -->
  <router-view v-slot="{ Component, route }">
    <transition :name="route.meta.transitionName">
      <component :is="Component" />
    </transition>
  </router-view>
  ```
- 경로에 깊이에 따라 메타 필드의 정보를 after navigation hook을 추가할 수 있습니다.
  ```js
  router.afterEach((to, from) => {
    const toDepth = to.path.split('/').length;
    const fromDepth = from.path.split('/').length;
    to.meta.transitionName = toDepth < fromDepth ? 'slide-right' : 'slide-left';
  });
  ```

### Forcing a transition between reused views

- 유사하게 보이는 구성요소를 재사용하여 transition을 피할 수 있습니다.
- 이 경우 강제로 전환을 하려하는 경우 키 속성을 추가할 수 있습니다.
- 키 속성을 추가하면 다른 params를 사용하면서 동일한 경로를 유지한 채로 transition을 사용할 수 있습니다.
  ```html
  <router-view v-slot="{ Component, route }">
    <transition name="fade">
      <component :is="Component" :key="route.path" />
    </transition>
  </router-view>
  ```
