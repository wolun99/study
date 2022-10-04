## HTTP (HyperText Transfer Protocol)
- HTML,TEXT
- IMAGE,음성,영상,파일
- JSON,XML(API)
- 거의 모든 형태를 전송
- 서버간 데이터 전송을 주고 받을 때도 HTTP 사용
    ### HTTP의 역사
    - HTTP/0.9(1991년):GET메서드만 지원 HTTP 헤더X
    - HTTP/1.0(1996년):메서드, 헤더 추가
    - HTTP/1.1(1997년):가장 많이 사용,그래서 중요함
    - HTTP/2(2015년):성능개선
    - HTTP/3(진행중):TCP대신에 UDP 사용
    ### 기반 프로토콜
    - TCP : HTTP/1.1,HTTP/2
    - UDP : HTTP/3
    - 주로 HTTP/1.1 사용
    ### HTTP 특징
    1. 클라이언트 서버 구조
    2. 무상태 프로토콜(스테이스리스), 비연결성
    3. HTTP 메시지
    4. 단순함, 확장 가능

## 클라이언트 서버 구조
- Request Response 구조
- 클라이언트는 서버에 요청을 보내고 응답을 대기(UX를 어떻게 그릴지)
- 서버는 요청에 결과로 응답을 만듬(비지니스 로직이나 복잡한 데이터를 다룸)
- 분리하여 서로가 따로따로 진화할 수 있다.

## 무상태 프로토콜(stateless)
- 서버가 클라이언트 상태를 보존하지 않음
- 장점: 확장성이 좋아짐(스케일 아웃 - 수평 확장 유리)
- 단점: 데이터를 너무 많이 보내야함 
    ### stateful, stateless 차이
    - 상태 유지(stateful) :  중간에 다른 서버로 변경하면 안된다(변경시 데이터를 항상 넘겨줘야함) 
    - 무상태(statless) : 중간에 서버가 바뀌어도 클라이언트에서 데이터를 포함해서 전달하기 때문에 괜찮음, 응답 서버를 쉽게 바꿀 수 있어 서버 증설이 용이함
    ### stateless 한계
    - 모든것을 무상태로 설계할 수 있는 경우가 있고 없는 경우가 있음
    - 상태 유지가 필요없는 로그인이 없는 간단한 페이지 경우 사용가능
    - 로그인이나 데이터가 유지 되어야 하는 경우는 사용 불가
    - 상태유지는 최소한으로
## 비연결성
- HTTP는 기본이 연결을 유지하지 않음
- 일반적으로 빠른 응답
- 동시에 수천명이 서비스를 요청해도 실제로 동시 처리하는 요청은 수십개 정도임
- 연결하고 응답이 완료되면 연결을 종료하므로 효율을 높힐 수 있음
    ### 비연결성의 한계
    - TCP/IP 연결을 새로 맺어야함 - 3 way handshake 시간 추가
    - 웹 브라우저로 사이트에 접속하면 여러 리소스들이 다운로드됨
    - HTTP 지속연결(Persistent Connetion)로 문제 해결
    - HTTP/2 와 HTTP/3에서는 더 최적화가 잘되있음
## HTTP 메시지
- HTTP 요청 메시지의 구조는 맨위부터 start-line(시작라인) - header(헤더) - empty line(공백라인 반드시 있어야함!) - message body
    ### 요청메시지
    - 시작 라인
        - request-line = method SP(공백) request-target SP HTTP-version 엔터(마무리)
        - 요청대상(/ 절대경로로 사용)
        - HTTP 메서드(GET:조회,POST:요청 내역 처리,PUT,DELETE)
    ### 응답메시지
    - 시작 라인
        -status-line = HTTP-version SP(공백) status-code SP reason-phrase 엔터(마무리)
        - status-code(상태코드):요청의 성공, 실패를 나타냄
            - 200:성공
            - 400:클라이언트 오류
            - 500:서버 오류
- HTTP 헤더
    - header-field = field-name":"OWS field-value OWS(띄어쓰기 허용)
    - field-name은 대소문자 구별없음
    - HTTP 전송에 필요한 모든 부가정보
    - 표준 헤더가 너무 많음
    - 임의의 헤더 추가가능
- HTTP 메시지 바디
    - 실제 전송할 데이터
    - HTML 문서, 이미지, 영상, JSON 등 byte로 표현 가능한 모든 데이터 전송가능