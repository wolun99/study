## URI(Uniform Resource Identifier)
- URI는 URL(Resource Locator)과 URN(Resource Name)의 범위를 가짐
- Uniform : 리소스 식별하는 방식
- Resource : 자원,URI로 식별할 수 있는 모든 정보(제한 없음)
- Identifier : 다른 항목과 구분하는데 필요한 정보
- URL - Locator: 리소스가 있는 위치를 지정
- URN - Name: 리소스에 이름을 부여
    - 위치는 변할 수 있지만, 이름은 변하지 않음

## URL
- scheme://[userinfo@]host[:port][/path][?query][#fragment]
- scheme : http,https와 같은 프로토콜 사용
- userinfo : 거의 사용하지 않음
- host : 호스트 도메인명 또는 IP주소
- port : 생략가능 생략시 http는 80 https 443
- 리소스 경로, 계층적 구조
- query : key:value 형태로 들어감 ?로 시작 &로 추가 가능, query parameter, query string 등으로 부름
- fragment : html 내부 북마크 등에서 사용함

## 웹브라우저 흐름
1. DNS 조회
2. 포트 정보 확인
3. HTTP 요청 메시지 생성
    - 요청 메시시 : GET/경로 HTTP/1.1(버전) HOST:호스트정보
4. 패킷 전송 과정을 거침
5. 패킷 도착하면 포장했던 TCP/IP 정보에서 HTTP 메시지 확인
6. HTTP 메시지의 데이터를 서버에서 찾음
7. HTTP 응답 메시지를 생성하고
8. TCP/IP 패킷으로 감싸서 클라이언트로 다시 전송
9. 클라이언트가 받아서 TCP/IP 패킷내의 응답 메시지를 확인해서 렌더링해서 화면에 보여줌