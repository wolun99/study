## scoll behavior

- 클라이언트 사이드 라우팅을 할 때 맨위로 스크롤하거나 실제페이지를 로드하는 것처럼 컨텐츠 항목의 스크롤을 유지할 수 있습니다.
- vue-router에서는 인스턴스를 생성할 때 scrollBehavior 함수를 사용하여 제공합니다.
  ```js
    const router = createRouter({
      history: createWebHashHistory(),
      routes: [...],
      scrollBehavior (to, from, savedPosition) {
        // 원하는 위치를 반환
      }
    })
  ```
- scrollBehavior 함수는 to 와 from을 객체로 전달받습니다.
- 세번째 인수로 받은 savedPosition은 브라우저의 앞/뒤를 표현하는 popstate일 때만 사용가능합니다.
- 이러한 함수는 ScrollToOption 객체를 반환합니다.
  ```js
  const router = createRouter({
    scrollBehavior(to, from, savedPosition) {
      // 항상 맨위를 유지
      return { top: 0 };
    },
  });
  ```
- el을 통해 css선택 또는 DOM요소를 전달할 수 있습니다. 위쪽과 왼쪽은 해당 요소에 대한 상대의 오프셋으로 처리됩니다.
  ```js
  const router = createRouter({
    scrollBehavior(to, from, savedPosition) {
      // #main 보다 항상 10px위에 있습니다.
      return {
        // 또한 el 을 통해 선택할 수 있습니다.
        el: '#main',
        top: -10,
      };
    },
  });
  ```
- 거짓 값이나 빈 값을 반환하면 스크롤이 발생하지 않습니다.
- savePosition을 반환하면 앞/뒤 버튼을 눌렀을 때와 같게 동작합니다.
  ```js
  const router = createRouter({
    scrollBehavior(to, from, savedPosition) {
      if (savedPosition) {
        return savedPosition;
      } else {
        return { top: 0 };
      }
    },
  });
  ```
- 브라우저가 스크롤 동작을 지원하는경우 부드럽게 만들 수 있습니다.
  ```js
  const router = createRouter({
    scrollBehavior(to, from, savedPosition) {
      if (to.hash) {
        return {
          el: to.hash,
          behavior: 'smooth',
        };
      }
    },
  });
  ```

### Delaying the scroll

- 페이지에서 스크롤 하기 전에 조금 기다려야 합니다. 예를 들어 전환 처리를 할 때 스크롤하기 전에 전환이 완료되기를 기다립니다.
- 원하는 위치 설명자를 반환하는 Promise를 반환할 수 있습니다.
  ```js
  const router = createRouter({
    scrollBehavior(to, from, savedPosition) {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve({ left: 0, top: 0 });
        }, 500);
      });
    },
  });
  ```
- 페이지 전환 요소의 이벤트와 전환이 함께 스크롤 동작이 원활하게 실행되도록 할 수 있습니다.
- 그러나 가변성과 복잡성때문에 사용자 영역을 구현하기 위하여 기본 요소만 제공하면 됩니다.
