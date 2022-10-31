## 명명된 경로

- 모든경로에 path와 함께 name을 사용할 수 있습니다. 이에 따른 장점
  1. 하드코딩된 URL이 없습니다.
  2. params의 자동 인코딩/디코딩
  3. URL 오타를 방지합니다.
  4. 순위를 무시합니다.
- <route-link>로 정의하는 곳의 to속성에도 전달할 수 있습니다.
  ```js
    <router-link :to="{ name: 'user', params: { username: 'erina' }}">
      User
    </router-link>
  ```
  ```js
  router.push({ name: 'user', params: { username: 'erina' } });
  ```
- router.push()을 하는것과 같습니다.

## 명명된 뷰

- 여러가지 보기를 동시에 표현해야하는 경우 명명된 뷰를 사용하는 것이 유용합니다.
- 하나의 view에 name을 사용하여 구별이 가능하고 name을 지정하지 않은 view는 default가 됩니다.
  ```html
  <router-view class="view left-sidebar" name="LeftSidebar"></router-view>
  <router-view class="view main-content"></router-view>
  <router-view class="view right-sidebar" name="RightSidebar"></router-view>
  ```
- rendering 하기 위해서는 component가 필요하기 때문에 여러 view를 표현하기 위해서는 여러 component가 필요합니다.
  ```js
  const router = createRouter({
    history: createWebHashHistory(),
    routes: [
      {
        path: '/',
        components: {
          default: Home,
          LeftSidebar,
          RightSidebar,
        },
      },
    ],
  });
  ```

## 중첩된 명명된 뷰

- 중첩된 뷰를 사용하여 복잡한 레이아웃을 만들 수 있습니다.
  ```
    /settings/emails                                       /settings/profile
  +-----------------------------------+                  +------------------------------+
  | UserSettings                      |                  | UserSettings                 |
  | +-----+-------------------------+ |                  | +-----+--------------------+ |
  | | Nav | UserEmailsSubscriptions | |  +------------>  | | Nav | UserProfile        | |
  | |     +-------------------------+ |                  | |     +--------------------+ |
  | |     |                         | |                  | |     | UserProfilePreview | |
  | +-----+-------------------------+ |                  | +-----+--------------------+ |
  +-----------------------------------+                  +------------------------------+
  ```
  - Nav는 일반 구성요소입니다.
  - UserSetting은 상위 뷰 요소입니다.
  - UserEmailsSubscriptions, UserProfile, UserProfilePreview 중첩된 뷰입니다.
- 이렇게 설계한 레이아웃은 이렇게 표현할 수 있습니다.
  ```js
    {
      path: '/settings',
      // 상단에 명명된 보기를 가질 수도 있습니다.
      component: UserSettings,
      children: [{
        path: 'emails',
        component: UserEmailsSubscriptions
      }, {
        path: 'profile',
        components: {
          default: UserProfile,
          helper: UserProfilePreview
        }
      }]
    }
  ```
