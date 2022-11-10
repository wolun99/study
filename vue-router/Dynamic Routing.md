## Dynamic Routing
- router에 routes 추가하는 것은 항상 routes 옵션을 사용하지만 어떤 경우 애플리케이션이 이미 실행되는 동안 route를 추가하거나 제거할 수 있습니다.
### Adding Routes
- 동적 라우팅은 주로 router.addRoute() 와 router.removeRoute()로 동작합니다.
- 두가지 함수는 항상 새로운 route를 추가합니다, 즉 새로운 경로가 현재 위치와 일치하면 해당 새 경로를 렌더링하기 위해서는 router.push()또는 router.replace()를 사용하여야 합니다.
  ```js
    const router = createRouter({
      history: createWebHistory(),
      routes: [{ path: '/:articleName', component: Article }],
    })
  ```
- 어느 페이지를 가더라도 Article Component가 렌더링됩니다.
  ```js
    router.addRoute({ path: '/about', component: About })
  ```
- 위와 같이 추가하더라도 여전히 Article Componet가 표시되고 이를 수동을 router.replace()를 호출하여 현재 위치에 변경할 component를 지정해야 합니다.
  ```js
    router.addRoute({ path: '/about', component: About })
    // 이것(this.$route or route = useRoute() (inside a setup))을 사용할 수도 있습니다.
    router.replace(router.currentRoute.value.fullPath)
  ```
- 새 경로가 표시될 때까지 기다려야하는경우 await router.replce()를 사용할 수 있습니다.
### Adding Routes inside navigation guards
- 네비게이션 가드 안에서 routes를 추가하거나 제거하기로 결정했다면 router.replace()를 호출하지 말고 새로운 경로를 리다이렉션이 발생하도록 해야합니다.
  ```js
    router.beforeEach(to => {
      if (!hasNecessaryRoute(to)) {
        router.addRoute(generateRoute(to))
        // 리다이렉션이 발생하도록 하기
        return to.fullPath
      }
    })
  ```
- 위 예제는 두가지 가정을 가집니다. 첫째, 새로 추가된 경로가 대상위치와 일치하여 실제로 접근하려는 경로와 다른 위치에 있습니다. 둘째, hasNecessaryroute()는 무한 리다이렉션을 피하기 위해 새경로를 추가한 후 false를 반환합니다.
- 리다이렉션 중이므로 효과적으로 진행중인 탐색을 대체합니다.
- 추가는 탐색 가드 외부에서 발생할 가능성이 더 높습니다.
### Removing routes
- 기존 경로를 변경하는 방법은 몇가지가 있습니다.
1. 이름이 충돌하는 경로를 추가하면 기존 경로는 삭제하고 추가된 경로를 추가합니다.
    ```js
      router.addRoute({ path: '/about', name: 'about', component: About })
      //이름이 동일하고 이름이 고유하기 때문에 이전에 추가한 경로가 제거됩니다.
      router.addRoute({ path: '/other', name: 'about', component: Other })
    ```
2. router.addRoute()에 의해 반환된 콜백을 호출하여
    ```js
      const removeRoute = router.addRoute(routeRecord)
      removeRoute() // 경로가 존재하는 경우 삭제합니다.
    ```
    - 경로에 이름이 없을 경우 유용합니다.
3. router.removeRoute()를 사용하여 이름으로 경로를 제거합니다.
    ```js
      router.addRoute({ path: '/about', name: 'about', component: About })
      // 경로를 제거합니다.
      router.removeRoute('about')
    ```
    - 이 기능을 사용할 때 이름의 충돌을 피하려는 경우 Symbols 사용할 수 있습니다.
- 경로가 제거될 때 모든 속성이 제거 됩니다.
### Adding nested routes
- 중첩된 경로를 기존 경로에 추가하려면 router.addRoute()에 첫번째 매개 변수로 전달할 수 있습니다.
  ```js
    router.addRoute({ name: 'admin', path: '/admin', component: Admin })
    router.addRoute('admin', { path: 'settings', component: AdminSettings })
  ```
  ```js
    router.addRoute({
      name: 'admin',
      path: '/admin',
      component: Admin,
      children: [{ path: 'settings', component: AdminSettings }],
    })
  ```
- 위 두개의 예제는 같습니다.
### Looking at existing routes
- 존재하는 routes를 확인하기 위해 두가지의 함수를 제공합니다.
  - router.hasRoute() : route가 존재하는지 확인합니다.
  - router.getRoutes() : 모든 route가 포함된 배열을 가져옵니다.
  