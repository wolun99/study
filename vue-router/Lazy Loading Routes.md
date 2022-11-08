## Lazy Loading Routes

- 번들러를 이용하여 javascript를 빌드할 때 파일이 커질 수 있으므로 페이지 로딩 속도가 느려질 수 있습니다.
- 그러한 이유로 각 경로별 컴포넌트를 별도의 청크로 분할하고 해당 경로를 방문할 때만 로드한다면 더 효율적일 것입니다.
- vue router는 기본적으로 동적인 import를 지원하므로 정적 import 대신 동적 import로 대체 할 수 있습니다.

  ```js
  // import UserDetails from './views/UserDetails'
  // 위의 정적 import를 동적 import로 대체합니다.
  const UserDetails = () => import('./views/UserDetails.vue');

  const router = createRouter({
    // ...
    routes: [{ path: '/users/:id', component: UserDetails }],
  });
  ```

- component의 옵션은 component의 Promise를 반환하는 함수를 받아 들이고 vue router가 처음으로 페이지에 들어갈 때만 가져오고 캐시된 버전을 사용합니다.
- 즉,Promise를 반환하면 더 복잡한 함수를 사용할 수 있습니다.
  ```js
  const UserDetails = () =>
    Promise.resolve({
      /* component 정의 */
    });
  ```
- 일반적으로 모든 경로를 동적 import를 사용하는것이 좋습니다.

## Grouping Components in the Same Chunk

### With webpack

- 때때로 동일한 경로의 모든 component를 동일한 비동기 청크로 그룹화할 수 있습니다.
- 이를 수행하려면 특수 주석 구문을 사용하여 청크 이름을 지정하여 명명된 청크를 사용해야 합니다.
  ```js
  const UserDetails = () =>
    import(/* webpackChunkName: "group-user" */ './UserDetails.vue');
  const UserDashboard = () =>
    import(/* webpackChunkName: "group-user" */ './UserDashboard.vue');
  const UserProfileEdit = () =>
    import(/* webpackChunkName: "group-user" */ './UserProfileEdit.vue');
  ```
- webpack은 동일한 청크이름을 가지는 모든 비동기 모듈을 동일한 비동기 청크를 이용하여 그룹화합니다.

### with vue

- Vite에서는 rollupOptions 내에서 청크를 정의할 수 있습니다.
  ```js
    // vite.config.js
    export default defineConfig({
      build: {
        rollupOptions: {
          // https://rollupjs.org/guide/en/#outputmanualchunks
          output: {
            manualChunks: {
              'group-user': [
                './src/UserDetails',
                './src/UserDashboard',
                './src/UserProfileEdit',
              ],
            },
        },
      },
    })
  ```
