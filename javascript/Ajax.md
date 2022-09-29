## Ajax란?
- 자바스크립트를 사용하여 브라우저가 서버에게 비동기 방식으로 데이터를 요청하고 , 서버가 응답한 데이터를 수신하여 웹페이지를 동적으로 갱신하는 프로그래밍을 말한다.
- Web API인 XMLHttpRequest 객체를 기반으로 동작한다.
- 전통적인 방식은 이전 웹페이지와 차이가 없어서 변경할 필요가 없는 부분까지 변경해서 다시 렌더링을 하고 클라이언트와 서버와의 통신이 동기 방식으로 동작하기 때문에 블로킹이 발생한다.
- Ajax가 등장하고 서버로부터 웨페이지 변경에 필요한 데이터만 비동기 방식으로 전송받아 필요없는 부분은 다시 렌더링하지 않기 때문에 부드럽고 빠른 화면 전환이 가능해졌다.
## JSON
- JSON은 클라이언트와 서버 간의 HTTP 통신을 위한 텍스트 데이터 포맷이다.
    1. JSON 표기 방식
        - 자바스크립트의 객체 리터럴과 유사하게 키와 값으로 구성된 순수한 텍스트이다.
        - 키는 반드시 큰따옴표로 묶어야 한다.
    2. JSON.stringify
        - 객체를 JSON 포맷의 문자열로 변환한다.
        - 클라이언트가 서버로 객체를 전송하려면 객체를 문자열화해야 하는데 이를 직렬화라 한다.
    2. JSON.parse
        - JSON 포맷의 문자열을 객체로 벼노한한다.
        - 서버에서 클라이언트로 JSON 데이터를 전송하는데 이때 문자열을 객체화 해야하는데 이를 역직렬화라 한다.
## XMLHttpRequest
- 자바스크립트를 사용하여 HTTP 요청을 전송하려면 XMLHttpRequest 객체를 사용한다.
    1. XMLHttpRequest 객체 생성
        - XMLHttpRequest 생성자 함수를 호출하여 생성한다.
    2. XMLHttpRequest 객체의 프로퍼티와 메서드
        - readyState : HTTP 요청의 현재 상태를 나타내는 정수
            - UNSENT : 0
            - OPENED : 1
            - HEADERS_RECEIVED : 2
            - LOADING : 3
            - DONE : 4
        - status : HTTP 요청에 대한 응답 상태를 나타내는 정수
        - statusText : HTTP 요청에 대한 응답 메시지를 나타내는 문자열
        - responseType : HTTP 응답 타입
        - response : HTTP 요청에 대한 응답 몸체.
        - responseText : 서버가 전송한 HTTP 요청에 대한 응답 문자열
        - onreadystatechange : readyState 프로퍼티 값이 변경된 경우
        - onloadstart : HTTP 요청에 대한 응답을 받기 시작한 경우
        - onprogress : HTTP 요청에 대한 응답을 받는 도중 주기적으로 발생
        - onbort : abort 메서드에 의해 HTTP 요청이 중단된 경우
        - onerror : HTTP 요청에 에러가 발생한 경우
        - onload : HTTP 요청이 성공적으로 완료한 경우
        - ontimeout : HTTP 요청 시간이 초과한 경우
        - onloadend : HTTP 요청이 완료한 경우 . HTTP 요청이 성공 또는 실패하면 발생
        - open : HTTP요청 초기화
        - send : HTTP요청 전송
        - abort : 이미 전송된 HTTP요청 중단
        - setRequestHeader : 특정 HTTP 요청 헤더의 값을 설정
        - getResponseHeader : 특정 HTTP 요청 헤더의 값을 문자열로 반환
    3. HTTP요청 전송
        - 전송하는 경우 순서
            1. XMLHttpRequest.prototype.open 메서드로 HTTP요청을 초기화 한다.
            2. 필요에 따라 XMLHttpRequest.prototype.setRequestHeader 메서드로 특정 HTTP요청의 헤더값을 설정한다.
            3. XMLHttpRequest.prototype.send 메서드로 HTTP요청을 전송한다.
        - XMLHttpRequest.prototype.open
            - 서버에 전송을 HTTP 요청을 초기화 한다.
            - xhr.open(method(GET,POST,PUT,DELETE등), url,비동기 요청 여부(async))
        - XMLHttpRequest.prototype.send
            - open 메서드로 초기화된 HTTP 요청을 서버에 전송한다.
            - HTTP 요청메서드가 GET인 경우 send 메서드에 페이로드로 전달한 인수는 무시되고 요청 몸체는 null로 설정된다.
        - XMLHttpRequest.prototype.setRequestHeader
            - 특정 HTTP 쵸엉의 헤더 값을 설정한다.
    4. 응답 처리 
        - 서버가 전송한 응답을 처리하려면 XMLHttpRequest 객체가 발생시키는 이벤트를 캐치해야 한다.
        - readystatechange 이벤트나 load 이벤트를 캐치해서 확인한다.
        
    