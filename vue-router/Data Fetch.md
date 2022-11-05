## Data Fetch

- 라우터가 활성화 되었을 경우 서버에서 데이터를 가져와야하는 경우 두가지 방법을 사용하여 수행할 수 있습니다.
  1. Fetching After Navigation:라우터를 수행하고 라이플 사이클 훅을 사용하여 데이터를 가져오고 가져오는 동안 로드 상태를 표시합니다.
  2. Fetching Before Navigation:라우터 수행전 데이터를 가져오고 가드로 진입하여 데이터를 가져와서 라우터를 수행합니다.
- 두가지 방법은 유효하고 사용자 경험에 따라 다릅니다.

### Fetching After Navigation

- 구성요소를 즉시 탐색하고 렌더링하고 생성된 훅을 이용하여 데이터를 가져오는 동안 로드 상태를 표현할 수 있습니다.
- $route.params.id를 기반으로 게시물의 데이터를 가져와야 하는 Post 구성 요소가 있다고 가정해 보겠습니다.

  ```html
  <template>
    <div class="post">
      <div v-if="loading" class="loading">Loading...</div>

      <div v-if="error" class="error">{{ error }}</div>

      <div v-if="post" class="content">
        <h2>{{ post.title }}</h2>
        <p>{{ post.body }}</p>
      </div>
    </div>
  </template>
  ```

  ```js
  export default {
    data() {
      return {
        loading: false,
        post: null,
        error: null,
      };
    },
    created() {
      // 데이터를 다시 가져오기위해 경로를 매개변수로 확인합니다.
      this.$watch(
        () => this.$route.params,
        () => {
          this.fetchData();
        },
        // view가 생성되고 데이터가 확인되고 있을때 데이터를 가져옵니다.
        { immediate: true }
      );
    },
    methods: {
      fetchData() {
        this.error = this.post = null;
        this.loading = true;
        // getPost를 데이터 가져오기 유틸리티/API 래퍼로 바꿉니다.
        getPost(this.$route.params.id, (err, post) => {
          this.loading = false;
          if (err) {
            this.error = err.toString();
          } else {
            this.post = post;
          }
        });
      },
    },
  };
  ```

### Fetching Before Navigation

- 새 경로로 이동하기 전 데이터를 가져옵니다. beforeRouteEnter 가드에서 데이터를 가져올 수 있으며 가져오기가 완료된 경우만 next를 호출하여 전달된 콜백을 마운트시킬 수 있습니다.
  ```js
  export default {
    data() {
      return {
        post: null,
        error: null,
      };
    },
    beforeRouteEnter(to, from, next) {
      getPost(to.params.id, (err, post) => {
        next((vm) => vm.setData(err, post));
      });
    },
    // 라우터가 변경될 때 이미 컴포넌트가 렌더되었다면 이러한 로직은 조금 변경됩니다.
    async beforeRouteUpdate(to, from) {
      this.post = null;
      try {
        this.post = await getPost(to.params.id);
      } catch (error) {
        this.error = error.toString();
      }
    },
    methods: {
      setData(error, post) {
        if (error) {
          this.error = error;
        } else {
          this.post = post;
        }
      },
    },
  };
  ```
- 데이터를 가져오는 동안 사용자는 이전 컴포넌트를 보고 있습니다.
- 그렇기 때문에 진행률을 표시하여 주는 것이 사용자에게 좋고, 데이터를 가져오는 것이 실패했을 경우 전역경고 메시지를 표시해야 합니다.
