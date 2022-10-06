## Form 입력 바인딩
- Form 입력 엘리먼트 상태를 동기화 해야하는 경우가 많음
```html
<input :value="text" @input='event => text = event.target.value'>
```
- 이러한 작업 대신 v-model을 사용해 바인딩을 함
```html
<input v-model="text">
```
- input뿐만 아니라 textarea,select 에서도 사용가능
- input과 textarea는 value 속성과 input 이벤트를 사용
- checkbox와 radio의 경우 checked 속성과 change 이벤트를 사용
- select는 value 속성과 change 이벤트를 사용
- 한국어 적용시 업데이트가 바로 적용되지 않기 때문에 input 이벤트와 value 바인딩으로 적용할 수 있다.

## 기본 사용법
- 텍스트
    ```html
      <p>메세지 : {{message}}</p>
      <input v-model="message"/>
    ```
- 여러줄 텍스트
    ```html
    <p>{{text}}}</p>
    <textarea v-model="text"></textarea>
    ```

- 체크박스
    ```html
    <input type="checkbox" id="checkbox" v-model="checked"/>
    <label for="checkbox">{{checked}}</label>
    ```
- 라디오 
    ```html
      <div>선택한 것 : {{picked}}</div>
      <input type="radio" id="one" value="하나" v-model="picked" />
      <label for="one">하나</label>

      <input type="radio" id="two" value="둘" v-model="picked" />
      <label for="two">둘</label>
    ```
- 셀렉트
  - 단일셀렉트와 다중선택(배열로 바인딩)이 있고 셀렉트의 옵션은 v-for를 사용하여 동적으로 바인딩 가능
    ```html
      <div>선택됨: {{ selected }}</div>
      <select v-model="selected" multiple>
        <option>가</option>
        <option>나</option>
        <option>다</option>
      </select>
    ```
## 수식어
  - .lazy
    - change이벤트 이후에 동기화를 위해 사용
  - .number
    - 사용자 입력이 숫자로 변환하도록 parseFloat()으로 파싱할 수 없으면 원래 값 사용
    type="number"이면 자동 적용
  - .trim
    - 공백을 자동으로 가지려면 사용