## DOM
- HTML 문서를 계층적 구조와 정보를 표현하며 이를 제어할 수 있는 API,즉 프로퍼티와 메서드를 제공하는 트리 자료구조다.
## 노드
1. HTML 요소와 노드 객체
    - HTML 요소는 HTML문서를 구성하는 개별적인 요소를 의미한다.
    - 렌더링 엔진에 의해 요소의 어트리뷰트는 어트리뷰트 노드로, 텍스트 콘텐츠는 텍스트 노드로 변환된다.
    - HTML 문서는 HTML 요소들의 집합으로 이뤄지며 중첩 관계를 갖는다.
    - 노드 객체들로 구성된 트리 자료구조를 DOM이라 한다.
2. 노드 객체의 타입
    - 노드 타입에는 12개의 종류가 있다. 이 중 중요한 노드타입은 4가지이다.
        1. 문서 노드
        2. 요소 노드
        3. 어트리뷰트 노드
        4. 텍스트 노드
3. 노드 객체의 상속 구조
    - DOM을 구성하는 노드 객체는 자신의 구조와 정보를 제어할 수 있는 DOM API를 사용할 수 있다. 이를 통해 노드 객체는 자신의 부모, 형제 ,자식을 탐색할 수 있으며 , 자신의 어트리뷰트와 텍스트를 조작할 수도 있다.
    - 노드 객체도 자바스크립트 객체이므로 프로토타입에 의한 상속 구조를 갖는다.
    - 노드 객체의 상속구조는 개발자 도구의 Elements 패널의 우측 Properties 패널에서 확인할 수 있다.
## 요소 노드 취득 
- HTML의 구조나 내용 또는 스타일을 동적으로 변경하려면 요소 노드를 취득해야한다. 
    1. id를 이용한 요소 노드 취득
    - Document.prototype.getElementBYID 메서드를 통해 id 어트리뷰트 값을 갖는 하나의 요소 노드를 탐색하여 반환한다.
    - 여러개의 id가 있을 수 있지만 인수로 갖는 첫번째 요소 노드만 반환한다.
    2. 태그 이름을 이용한 요소 노드 취득
    - Document.prototype/Element.prototype.getElementByTagName 메서드는 인수로 전달한 태그이름을 갖는 모든 요소 노드를 탐색하여 반환한다.
    - 모든 요소 노드를 취득하기 위해서는 *을 인수로 던달하면 된다.
    3. class를 이용한 요소 노드 취득
    - Document.prototype/Element.prototype.getElementsByClassName 메서드는 인수로 전달한 class 어트리뷰트 값을 갖는 모든 요소 노드를 참색하여 반환한다.
    4. CSS 선택자를 이용한 요소 노드 취득
    - Document.prototype/Element.prototype.querySelector 메서드는 인수로 전달한 css 선택자를 마족시키는 하나의 요소 노드를 탐색하여 반환한다. 
    - 모든 요소 노드를 취득하려면 querySelectorAll 메서드의 인수로 *를 전달한다.
    5. 특정 요소 노드를 취드그할 수 있는지 확인
    - Element.prototype.matches 메서드는 인수로 전달한 css 선택자를 통해 특정 요소 노드를 취득할 수 있는지 확인한다.
    6. HTMLCollection과 NodeList
    - DOM 컬렉션 객체인 HTMLCollection과 NodeList는 DOM API가 여러 개의 결과값을 반환하기 위한 컬렉션 객체이다.
    - 모두 유사 배열이며 이터러블이다.
    - 특징으로는 상태 변화를 신시간으로 반영하는 살아 있는 객체라는 것이다.
## 노드 탐색
- 취득한 요소 노드를 기점으로 DOM 트리의 노드를 옮겨 다니며 부모, 형제, 자식 노드 등을 탐핵해야 할 때가 있다.
- 노드 탐색 프로퍼티는 모두 접근자 프로퍼티다. setter없이 getter만 존재하여 참조하므로 읽기 전용 접근자 프로퍼티이다.
    1. 공백 텍스트 노드
        - HTML 요소 사이의 스페이스, 태 , 줄바꿈 등의 공백문자는 텍스트 노드를 생성한다.
        - 노드 탐색할 때는 공백 문자가 생성한 공백 텍스트 노드에 주의해야 한다.
    2. 자식 노드 탐색
    - 자식노드를 탐색하기 위해서는 다음과 같은 노드 탐색 프로퍼티를 사용한다.
        - Node.prototype.childNodes : childNodes 프로퍼티가 반환한 NodeList에는 요소노드뿐만 아니라 텍스트 노드도 포함되어 있을 수 있다.
        - Element.prototype.children : children 프로퍼티가 반환한 HTMLCollection에는 텍스트 노드가 포함되지 않는다.
        - Node.prototype.firstChild : 첫번째 자식 노드를 반환한다.
        - Node.prototype.lastChild : 마지막 요소를 반환한다.
        - Element.prototype.firstElementChild : 첫 번째 자식 요소 노드를 반환한다.
        - Element.prototype.lastElementChild : 마지막 자식 요소 노드를 반환한다.
    3. 자식 노드 존재 확인
        - 자식 노드가 존재하는지 확인하려면 Node.prototype.hasChildNodes 메서드를 사용한다. 불리언 값으로 반환한다.
    4. 요소 노드의 텍스트 노드 탐색
        - 요소 노드의 텍스트 노드는 요소 노드의 자식 노드이다. 
        - firstChild 프로퍼티로 접근할 수 있다.
    5. 부모 노드 탐색
        - 부모 노드를 탐색하려면 Node.prototype.parentNode 프로퍼티를 사용한다. 
        - DOM트리의 최종단 노드인 리프 노드이므로 부모 노드가 텍스트 노드인 경우는 없다. 
    6. 형제 노드 탐색 
        - Node.prototype.previousSibling : 부모 노드가 같은 형제 노드 중에서 자신의 이전 형제 노드를 탐색하여 반환한다.
        - Node.prototype.nextSibling : 부모 노드가 같은 형제 노드 중에서 자신의 다음 형제 노드를 탐색하여 반환한다.
        - Element.prototype.previousElementSibling : 부모 노드가 같은 형제 노드 중에서 자신의 이전 형제 노드를 탐색하여 반환한다.
        - Element.prototype.nextElementSibling : 부모 노드가 같은 형제 노드 중에서 자신의 다음 형제 노드를 탐색하여 반환한다.
## 노드 정보 취득
- Node.prototype.nodeType : 노드 객체의 종류 , 즉 노드 타입을 나타내는 상수를 반환한다.
- Node.prototype.nodeName : 노드의 이름을 문자열로 반환한다.
## 요소 노드의 텍스트 조작
1. nodeValue
    - setter와 getter 모두 존재하는 접근자 프로퍼티다. 참조와 할당 모두 가능하다.
    - nodeValue 프로퍼티를 참조하면 노드 객체의 값을 반환한다.
2. textContent
    - setter와 getter 모두 존재하는 접근자 프로퍼티로서 요소 노드의 텍스트와 모든 자손 노드의 텍스트를 모두 취득하거나 변경한다.
    - 요소 노드의 콘텐츠 영역 내의 텍스트를 모두 반환한다. 이때 HTML 마크업은 무시된다.
## DOM 조작
- 새로운 노드를 생성하여 DOM에 추가하거나 기존 노드를 삭제 도는 교체하는 것
- DOM 조작에 의해 DOM에 새로운 노드가 추가되거나 삭제되면 리플로우와 리페인팅이 발생한다.
    1. innerHTML
        - 접근자 프로퍼티로서 요소 노드의 HTML 마크업을 취득하거나 변경한다.
        - 요소 노드의 컨텐츠 영역 내에 포함된 모든 HTML 마크업을 문자열로 반환한다.
        - textContent와 다르게 마크업이 포함된 문자열을 그대로 반환한다.
        - 사용자로부터 입력 받은 그대로 innerHTML 프로퍼티에 할당하는 것은 크로스 사이트 스크립팅 공격(XSS)에 취약하므로 위험하다.
    2. insertAdjacentHTML
        - 기존 요소를 제거하지 않으면서 위치를 지정해 새로운 요소를 삽입한다.
        - 두번째 인수로 전달한 HTML ㅁ마크업 문자열을 파싱하고 결과로 생성된 노드르르 첫 번째 인수로 전달한 위치에 삽입하여 DOM에 반영한다.
        - 첫 번재 인수로 전달할 수 있는 문자열은 'beforebegin','afterbegin','beforeend','afterend'
        - 크로스 사이트 스크립팅 공격에 취약하다는 점은 동일하다.
    3. 노드 생성과 추가
        - Document.prototype.createElement 메서드는 요소 노들르 생성하여 반환한다. 생성만 할 뿐 돔 요소에 추가하지는 않는다.
        - Document.prototype.createTextNode 메서드는 텍스트 노드를 생성하여 반환한다. 매개변수 에는 텍스트 노드 값으로 사용할 문자열을 인수로 전달한다.
        - Node.prototype.appendChild 매개변수로 인수로 전달한 노드를 appendChild 메서드를 호출한 노드의 마지막 자식 노드로 추가한다.부자 관계로 연결 되어 있지만 아직 기존DOM에 추가되지 않은 상태이다.
    4. 복수의 노드 생성과 추가
        - 요소를 반복하여 추가 하는 것은 비효율적이므로 미리 부모 요소를 만들어 자식 노드를 추가해 그곳에 추가한다면 효율적으로 사용할 수 있다.
    5. 노드 삽입
        - Node.prototype.appendChild 인수로 전달받은 노드를 자신을 호출한 노드의 마지막 자식 노드로 DOM에 추가한다.
        - Node.prototype.inserBefore(newNode,childNode) 첫 번째 인수로 전달받은 노드를 두 번째 인수로 전달받은 노드 앞에 삽입한다.
    6. 노드 이동
        - appendChild 또는 insertBefore 메서드를 사용하여 다시 추가하면 노드가 이동한다.
    7. 노드 복사 
        - Node.prototype.cloneNode([deep:true|false]) 노드의 사본을 생성하여 반환한다.
        - 매개변수 deep에 true를 인수로 전달하면 깊은 복사하여 모든 자손 노드가 포함된 사본을 생성, false를 인수로 전달하거나 생략하면 노드를 얕은 복사 하여 노드 자신만의 사본을 생성한다.
    8. 노드 교체
        - Node.prototype.replaceChild(newChild, oldChild)메서드는 자신을 호출한 자식 노드를 다른 노드로 교체한다.
    9. 노드 삭제
        - Node.prototype.removeChild(child) 메서드는 child 매개변수에 인수로 전달한 노드를 DOM에서 삭제한다.
## 어트리뷰트
1. 어트리뷰트 노드와 attributes 프로퍼티
    - HTML 문서의 구성요소인 HTML 요스는 여러개의 어트리뷰트를 가질 수 있다.
    - 어트리뷰트는 어트리뷰트 이름 = "어트리뷰트 값" 형식으로 정의한다.
    - 요소 노드의 모든 어트리뷰트 노드느느 Element.prototype.attributes 프로퍼티로 취득할 수 있다.
    - geetter만 존재하는 읽기 전용 접근자 프로퍼티이며 요소의 모든 어트리뷰트 노드의 참조가 담긴 NamedNodeMap객체를 반환한다.
2. HTML 어트리뷰트 조작
    - Element.prototype.getAttribute/setAttribute 메서드를 사용하면 attribute 프로퍼티를 통하지 않고 직접 변경할 수 있어서 편하다.
3. HTML 어트리뷰트 vs DOM 프로퍼티
    - 요소 노드 객체에는 HTML 어트리뷰트에 대응하는 프로퍼티가 존재한다.
    - HTML 어트리뷰트의 역할은 HTML 요소의 초기 상태를 지정하는 것이다. 즉 , HTML 어트리뷰트 값은 HTML 요소의 초기 상태를 의미하며 이는 변하지 않는다.
    - 요소 노드는 2개의 상태 , 초기 상태와 최신 상태를 관리해야 한다. 요소 노드의 초기 상태는 어트리뷰트 노드가 관리하며 , 요소 노드의 최신 상태는 DOM 프로퍼티가 관리한다.
4. data 어트리뷰트와 dataset 프로퍼티
    - data어트리뷰트와 dataset 프로퍼티를 사용하면 자바스크립트 간에 데이터를 교환할 수 있다.
## 스타일
1. 인라인 스타일 조작
    - HTMLElement.prototype.style프로퍼티는 접근자 프로퍼티로서 요소 노드의 인라인 스타일을 취득하거나 추가 또는 변경한다.
    - css 프로퍼티는 케밥 케이스를 따른다.
2. 클래스 조작
    - .으로 시작하는 클래스 선택자를 사용하여 css class를 미리 정의한 다음 HTML 요소의 class 어트리뷰트 값을 변경하여 HTML 요소의 스타일을 변경할 수도 있다.
3. 요소에 적용되어 있는 CSS 스타일 참조
    - style 프로퍼티는 인라인 스타일만 반환한다. 그래서 클래스를 적용한 스타일이나 상속을 통해 암묵적으로 적용된 스타일은 style 프로퍼티로 참조 할 수 없다.
    - 적용되어 있는 모든 CSS스타일을 참조 해야 할 경우 getComputedStyle 메서드를 사용한다.
    - 첫 번째 인수로 전달한 요소 노드에 적용되어 있는 평가된 스타일을 CSSStyleDeclaratio 객체에 담아 반환한다. 
    - 두 번째 인수로 :after, :before와 같은 의사 요소를 지정하는 문자열을 전달할 수 있다. 일반요소의 경우 두 번째 인수는 생략한다.