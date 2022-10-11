## Teleport
- 컴포넌트 템플릿의 일부를 해당 컴포넌트의 DOM 계층 외부의 DOM노드로 이동할 수 있게 해주는 빌트인 컴포넌트 입니다.
### 기본 사용법
- 대표적으로 모달을 구현할 때 사용하며 사용하고자 하는 부분을 Teleport를 사용하여 감싸서 사용한다.
  ```html
    <button @click="open = true">모달 열기</button>

    <Teleport to="body">
      <div v-if="open" class="modal">
        <p>짜자잔~ 모달입니다!</p>
        <button @click="open = false">닫기</button>
      </div>
    </Teleport>
  ```
- to에는 이동하려는 경로를 작성하므로 id,클래스 선택자나 데이터 선택자를 넣을 수 있다.
### 컴포넌트와 사용하기
- 렌더링된 DOM 구조만 변경하기때문에 논리적 구조에 영향을 주지않아 컴포넌트 상의 부모와 자식 상태를 변경하지 않습니다.
### 비활성화
- 조건부로 비활성화 할 수 있으며, disabled prop을 지원합니다.
### 같은대상에 여러 텔레포트 사용
- 여러 teleport 컴포넌트 컨텐츠를 동일 대상에 탑재할 때는 순서대로 대상 엘리먼트 내에 마운트 합니다.
  ```html
  <Teleport to="#modals">
    <div>A</div>
  </Teleport>
  <Teleport to="#modals">
    <div>B</div>
  </Teleport>
  ```
  ```html
    <div id="modals">
      <div>A</div>
      <div>B</div>
    </div>
  ```