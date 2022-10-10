## KeepAlive

- 여러 컴포넌트 간 동적으로 전환될 때, 조건부로 캐시할 수 있는 컴포넌트

### 기본사용법

- 활성 컴포넌트가 비활성되면 가지고 있던 상태(정보)가 손실됩니다.
- 이러한 상황에서 비활성된 컴포넌트의 상태를 보존하고자 하는 컴포넌트를 KeepAlive로 래핑해서 보존합니다.
  ```html
  <KeepAlive>
    <component :is="active" />
  </KeepAlive>
  ```

### Include/Exclude

- 인스턴스를 캐시할 때 include 및 exclude prop을 사용하여 정의할 수 있습니다.
- 쉼표로 구분된 문자열이나, 정규식 또는 둘 중 하나에 해당하는 배열이 올 수 있습니다.

  ```html
  <!-- 쉼표로 구분되는 문자열 -->
  <KeepAlive include="a,b">
    <component :is="view" />
  </KeepAlive>

  <!-- 정규식 (`v-bind`를 사용해야 함) -->
  <KeepAlive :include="/a|b/">
    <component :is="view" />
  </KeepAlive>

  <!-- 배열 (`v-bind`를 사용해야 함) -->
  <KeepAlive :include="['a', 'b']">
    <component :is="view" />
  </KeepAlive>
  ```

- name 옵션이 일치하는지 비교하므로 캐시 되어야하는 컴포넌트는 name을 명시적으로 표현해야 합니다.

### 최대 캐시 인스턴스

- max prop을 통해 캐시할 수 있는 인스턴스의 최대 수를 제한할 수 있습니다.
  ```html
  <KeepAlive :max="10">
    <component :is="activeComponent" />
  </KeepAlive>
  ```
- 최대 인스턴스를 초과하면 가장 최근에 접근해 인스턴스가 파괴되어 새로운 인스턴스를 만듭니다.

### 캐시된 인스턴스의 생명주기

- KeepAlive에 의해 캐시된 인스턴스는 마운트 해제가 아닌 비활성 상태로 바뀌며 캐시트리 일부가 DOM에 삽입되면 활성화 됩니다.
- actived 및 deactived 훅을 사용하며 두가지 상태에 생명주기 훅으로 등록할 수 있습니다.
  ```js
  export default {
    activated() {
      // 초기 마운트 시 또는
      // 캐시상태에서 다시 삽입될 때마다 호출됨.
    },
    deactivated() {
      // DOM에서 제거되고 캐시로 전환될 시 또는
      // 마운트 해제될 때마다 호출됨.
    },
  };
  ```
- 두 훅 모두 <KeepAlive>에 의해 캐시된 루트 컴포넌트뿐만 아니라 캐시된 트리의 자식 컴포넌트에서도 작동합니다.
