# VUE란?

- Javascript 프레임워크중 하나로 복잡한 사용자 인터페이스를 효율적으로 개발하기 위한 선언적, 구성요소 기반 프로그래밍 모델

## VUE의 특징
- MVVM 패턴
    > MVVM 패턴이란 모델(Model)  - 뷰(View) - 뷰 모델(View Model)로 구조화하여 개발하는 방식을 말한다
- 컴포넌트 기반의 프레임 워크
- React(Virtual DOM),Angular(데이터바인딩)의 장점을 가져왔다
- React와 Angular에 비해 속도가 빠르다

## API 스타일

  1. **Options API**
  ```js
  <script>
    export default{
      // 필요한 데이터나 함수는 this를 사용하여 바인딩해서 사용
      data(){ //필요한 데이터등을 담는 곳
        return{
          // key : 값 형태로 데이터 작성
        }
      },
      methods:{
        //데이터변경이나 이벤트실행 함수들을 사용
      },
      mounted(){
        //라이플 사이클 훅으로 특정지점에 실행되는 내용 
      }
    }
  </script>
  ```

  2. **Composition API**
  ```js
  <script setup>
    import{ref,onMounted} from 'vue'

    const count = ref(0) //상태값

    function increment(){ // 실행하고싶은 함수 작성
      count.value++
    }

    //lifecycle hooks
    onmounted(()=>{})
  </script>
  ``` 
  ## Vue 설치 방법

1. 공식문서의 빌드도구 사용

  ```
  npm init vue@latest
  ```

  사용하여 옵션설정등 해주기 

2. 공식문서의 빌드도구 없이 

  ```html
  <script src="https://unpkg.com/vue@3"></script>

  <div id="app">{{ message }}</div>

  <script>
    const { createApp } = Vue

    createApp({
      data() {
        return {
          message: 'Hello Vue!'
        }
      }
    }).mount('#app')
  </script>
  ```

  3.Vue CLI 이용하기

```js
npm install --global @vue/cli
```
Vue CLI 설치후 
```
vue create 프로젝트이름
```
터미널에 실행후 필요한 옵션 선택후 프로젝트 생성
