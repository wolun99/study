## Extending RouterLink
- RouterLink component는 대부분 기본 애플리케이션에 충분한 요소를 가지고 있지만 모든 상황에 가능한 것은 아니기에 v-slot을 사용하여 몇몇 상황을 해결할 수 있습니다.
- 대부분의 중대형 애플리케이션에서 여러 사용자 지정 RouterLink component가 아니더라도 하나를 만들어 애플리케이션 전체에 재사용할 수 있습니다.
  ```html
    <template>
      <a v-if="isExternalLink" v-bind="$attrs" :href="to" target="_blank">
        <slot />
      </a>
      <router-link
        v-else
        v-bind="$props"
        custom
        v-slot="{ isActive, href, navigate }"
      >
        <a
          v-bind="$attrs"
          :href="href"
          @click="navigate"
          :class="isActive ? activeClass : inactiveClass"
        >
          <slot />
        </a>
      </router-link>
    </template>

    <script>
    import { RouterLink } from 'vue-router'

    export default {
      name: 'AppLink',
      inheritAttrs: false,

      props: {
        // 만약 타입스크립트를 사용한다면 @ts-ignore을 추가하십시오
        ...RouterLink.props,
        inactiveClass: String,
      },

      computed: {
        isExternalLink() {
          return typeof this.to === 'string' && this.to.startsWith('http')
        },
      },
    }
    </script>
  ```
- 위 예제는 외부링크를 처리하고 사용자 지정 비활성 클래스를 추가하는 예제입니다.
- 만약 렌더함수를 사용하거나 computed 속성을 사용하는 경우 Composition API에서 useLink를 사용할 수 있습니다.
  ```js
    import { RouterLink, useLink } from 'vue-router'

    export default {
      name: 'AppLink',

      props: {
        // 만약 타입스크립트를 사용한다면 @ts-ignore을 추가하십시오
        ...RouterLink.props,
        inactiveClass: String,
      },

      setup(props) {
        // props에는 to를 비롯해 <router-link>에 들어가는 속성이 포함됩니다.
        const { navigate, href, route, isActive, isExactActive } = useLink(props)
        return { isExternalLink }
      },
    }
  ```
- 응용 프로그램의 다른 부분에 AppLink component를 사용할 수 있습니다.
  ```html
    <template>
      <AppLink
        v-bind="$attrs"
        class="inline-flex items-center px-1 pt-1 border-b-2 border-transparent text-sm font-medium leading-5 text-gray-500 focus:outline-none transition duration-150 ease-in-out hover:text-gray-700 hover:border-gray-300 focus:outline-none focus:text-gray-700 focus:border-gray-300 transition duration-150 ease-in-out"
        active-class="border-indigo-500 text-gray-900 focus:border-indigo-700"
        inactive-class="text-gray-500 hover:text-gray-700 hover:border-gray-300 focus:text-gray-700 focus:border-gray-300"
      >
        <slot />
      </AppLink>
    </template>
  ```