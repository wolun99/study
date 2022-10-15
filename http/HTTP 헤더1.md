## HTTP 헤더

- header-field = field-name ":" OWS field-value OWS (OWS는 띄어쓰기 허용)
- field-name 대소문자 없음

### 용도

- HTTP 전송에 필요한 모든 부가 정보를 넣는다
- 표준 헤더가 너무많음
- 필요시 임의로 추가 할수 있음

### 과거 HTTP 헤더

- 헤더 분류
  - General 헤더 : 메시지 전체에 적용되는 정보 ex) Connection:close
  - Request 헤더 : 요청 정보 ex) User-Agent:Mozilla/5.0
  - Response 헤더 : 응답 정보 ex) Server:Apache
  - Entity 헤더 : 엔티티 바디 정보 ex)Content-type:text/html,Content-Length:3423
- 메시지 본문은 엔티티 본문을 전달하는데 사용
- 엔티티 본문 요청이나 응답에 전달할 실제 데이터
- 엔티티 헤더는 엔티티 본문의 데이터를 해석할 수 있는 정보제공
  - 데이터 유형(html,json), 데이터 길이, 압축 정보 등등

### 최신 HTTP 헤더

- 메시지 본문(message body)를 통해 표현 데이터 전달
- 메시지 본문 = 페이로드(payload)
- 표현은 요청이나 응답에서 전달할 실제 데이터
- 표현 헤더는 표현 데이터를 해석할 수 있는 정보 제공
  - 데이터 유형(html,json), 데이터 길이, 압축 정보 등등
- 참고: 표현 헤더는 표현 메타데이터와, 페이로드 메시지를 구분해야 한다.

### 표현

- Content-type:표현 데이터의 형식(미디어타입, 문자인코딩)
- Content-Encoding : 표현 데이터의 압축방식(데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가, 데이터를 읽는 쪽에서 데이터 헤더의 정보로 압축해제)
- Content-Language : 표현 데이터의 자연 언어
- Content-Length : 표현 데이터의 길이(바이트 단위, Transfer-Encoding(전송 코딩)을 사용하면 사용하면 안됨)
- 표현 헤더는 : 전송과 응답 둘다 사용

### 협상

- 클라이언트가 선호하는 표현 요청
- Accept: 클라이언트가 선호하는 미디어 타입 전달
- Accept-Charset: 클라이언트가 선호하는 문자 인코딩
- Accept-Encoding: 클라이언트가 선호하는 압축 인코딩
- Accept-Language: 클라이언트가 선호하는 자연 언어
- 협상헤더는 요청시에만 사용

### 협상의 우선순위

- Quality Values(q) 값을 적용
- Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
  - 0~1 높을수록 우선순위
  - 생략하면 1
- Accept: text/_, text/plain, text/plain;format=flowed, _/\*
  - 구체적인 것을 우선한다
  1. text/plain;format=flowed
  2. text/plain
  3. text/\*
  4. _/_
- Accept: text/_;q=0.3, text/html;q=0.7, text/html;level=1,
  text/html;level=2;q=0.4, _/\*;q=0.5
  - 구체적인 것을 기준으로 미디어 타입을 맞춘다.

### 전송 방식

- 단순 전송
  - Content-Length: 3423 만 포장해서 전달
- 압축 전송
  - Content-Encoding: gzip 인코딩한 정보를 전달
- 분할 전송
  - Transfer-Encoding: chunked 전송 내용을 나눠서 전달
- 범위 전송
  - Content-Range: bytes 1001-2000 / 2000 범위를 지정해서 전달

### 일반전송

- From : 유저 에이전트의 이메일 정보(일반적으로 잘 사용하지 않고 검색 엔진 같은 곳에서 주로 사용하고 요청에 사용)
- Referer : 이전 웹 페이지 주소(사용하여 유입 경로 분석 가능, 요청에서 사용)
- User-Agent : 유저 에이전트 애플리케이션 정보(웹 브라우저 정보등등, 통계 정보, 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능, 요청에 사용)
- Server : 요청을 처리하는 오리진 서버의 소프트웨어 정보(응답에 사용)
- Date : 메시지가 생성된 날짜(응답에 사용)

### 특별한 정보

- Host : 요청한 호스트 정보(요청에서 사용, 필수정보, 하나의 서버가 여러 도메인 처리해야 할 때, 하나의 IP주소에 여러 도메인이 적용됬을 때)
- Location : 페이지 리다이렉션(3xx응답 결과에 Location이 있으면 자동 이동)
- Allow : 허용가능 HTTP 메서드(405(Method Not Allowed)에서 응답에 포함해야함)
- Retry-After : 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간(503(Service Unavailable - 서비스가 언제 불능인지 알려줄 수 있음 ))

### 인증

- Authorization : 클라이언트에 인증 정보를 서버를 전달
- WWW-Authenticate : 리소스 접근시 필요한 인증 방법 정의(401 Unauthorized 응답과 함께 사용 ex)WWW-Authenticate: Newauth realm="apps", type=1,
  title="Login to \"apps\"", Basic realm="simple")

### stateless

- 무상태 프로토콜이다.
- 클라이언트와 서버가 응답과 요청을 주고 받으면 연결이 종료
- 클라이언트가 다시 요청하면 이전 요청을 기억하지 못한다.
- 클랑이언트와 서버는 서로 상태를 유지하지 않는다.

### 쿠키

- Set-Cookie: 서버에서 클라이언트에 쿠키 전달(응답)
- Cookie : 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP요청시 서버로 전달
- 사용처 : 사용자 로그인 세션 관리, 광고 정보 트래킹
- 쿠키 정보는 항상 서버에 전송됨
  - 네트워크 트래픽 추가 발생
  - 최소한 정보만 사용(세션 ID, 인증토큰)
  - 서버에 전송하지 않고, 웹브라우저 내부에 데이터 저장하고 싶으면 스토리지를 사용
  #### 생명주기
  - Expires : 만료일이 되면 쿠키 삭제
  - max-age : 0이나 음수를 지정하면 쿠키 삭제
  - 세션 쿠키 : 만료날짜를 생략하면 브라우저 종료시까지 저장됨
  - 영속 쿠키 : 만료날짜를 입력하면 해당 날짜까지 유지
  #### 도메인
  - 명시: 시한 문서 기준 도메인 + 서브 도메인 포함
    - domain = example.org를 지정해서 쿠키 생성
  - 생략: 현재 문서 기준 도메인만 적용
    - example.org 에서 쿠키를 생성하고 domain 지정을 생략
  #### 경로
  - 이 경로를 포함한 하위 경로 페이지만 쿠키 접근
  - 일반적으로 path-/ 루트로 지정
  #### 보안
  - Secure
    - 쿠키는 http,https를 구분하지 않고 전송
    - Secure를 적용하면 https인 경우 전송
  - HttpOnly
    - XSS 공격방지
    - 자바스크립트에 접근 불가(document.cookie)
    - HTTP 전송에만 사용
  - SameSite
    - XSRF 공격방지
    - 요청 도메인과 쿠키에 설정된 도메인과 같은 도메인만 전송
