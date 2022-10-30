## 다른 위치로 이동

- 라우터 인스턴스의 $router를 호출할 수 있습니다.
- 다른 URL로 이동하기 위하여 router.push를 사용하는 합니다.
- 이는 <router-link :to="...">를 호출하는 것과 같습니다.
  ```js
  router.push('/user/mypage');
  //오브젝트 형태
  router.push({ path: '/user/mypage' });
  // parmas를 이용한 형태
  router.push({ path: 'user', params: { username: 'mypage' } });
  // query를 사용한 형태
  router.push({ path: '/register', query: { plan: 'private' } });
  // hash를 사용한 형탱
  router.push({ path: '/about', hash: '#team' });
  ```
- query 같은 경우 같은 경로가 제공 되지않으면 무시되며, 경로의 이름 대신 매개 변수를 이용하여 전체 경로를 지정해야 합니다.
  ```js
  const username = 'eduardo';
  // URL을 수동으로 지정할 수 있지만 직접적으로 적용해야 합니다.
  router.push(`/user/${username}`); // -> /user/eduardo
  router.push({ path: `/user/${username}` }); // -> /user/eduardo
  // name과 params의 사용이 가능하면 자동지정의 이점을 이용할 수 있습니다.
  router.push({ name: 'user', params: { username } }); // -> /user/eduardo
  // parmas는 path와 함께 사용할 수 없습니다.
  router.push({ path: '/user', params: { username } }); // -> /user
  ```
- 매개변수를 지정할 때는 숫자나 문자열을 지정해야합니다.
- 다른 데이터타입은 자동으로 문자열로 변경됩니다.
- 선택적으로 매개변수를 사용하는 경우 빈 문자열("")을 지정할 수 있습니다.
- prop의 to를 사용하는 것은 router.push 와 같은 종류의 객체이므로 둘 다 똑같은 규칙이 적용됩니다.
- route.push는 탐색이 완료될 때까지 기다렸다가 성공 또는 실패의 Promise를 반환합니다.

## 현재 위치를 대신하기

- router.push와 다르게 새로운 항목을 푸시하는것이 아닌 대체를 하기 위해서는 router.replace를 사용합니다.
- 이는 <router-link :to="..." replace>와 같게 동작합니다.
- router.push에 replace:true 속성을 등록하여 사용할 수 있습니다.
  ```js
  router.push({ path: '/home', replace: true });
  // 동일함
  router.replace({ path: '/home' });
  ```

## Traverse history

- window.history.go(n)와 유사하게 히스토리 스택을 사용하여 이동할 단계를 정수로 매개변수로 전달합니다.

  ```js
  // 앞으로 이동
  router.go(1);

  // 뒤로가기
  router.go(-1);

  // 3페이지 뒤로가기
  router.go(3);

  //실패했을때
  router.go(-100);
  router.go(100);
  ```

## 히스토리 조작

- Vue 라우터 탐색 방법(push, replace, go)은 라우터 인스턴스를 생성할 때 전달되는 히스토리 옵션의 종류와 상관없이 일관되게 작동합니다
