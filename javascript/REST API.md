## REST API
- HTTP를 기반으로 하는 클라이언트가 서버의 리소스에 접근하는 방식을 규정한 아키텍처
## REST API의 구성
- REST API는 자원, 행위 , 표현 의 3가지 요소로 구성된다.
    - 자원 : URI(엔드포인트)
    - 행위 : HTTP 요청 메서드
    - 표현 : 페이로드
## REST API 설계원칙 
- 중요한 것은 두가지이다 . URI는 리소스를 표현하는데 집중하고 행위에 대한 정의는 HTTP요청 메서드를 통해 하는것이 RESTful API를 설계하는 중심 규칙이다.
    1. URI는 리소스를 표현해야한다.
        - 리소스를 식별할 수 있는 이름은 동사보다 명사를 사용한다.
    2. 리소스에 대한 행위는 HTTP 요청 메서드로 표현한다.
        - 주로 5가지 요청 메서드(GET,POST,PUT,PATCH,DELETE)를 이용하여 CRUD를 구현한다.
## JSON Server를 이용한 REST API 실습
- JSON Server를 사용해 가상 REST API 서버를 구축하여 HTTP 요청을 전송하고 응답을 받는 실습을 할 수 있다.
    1. JSON Server 설치
        - npm을 사용하여 JSON Server를 설치하자
    2. db.json 파일생성
        - 프로젝트 루트 폴더에 db.json파일을 생성한다. 이는 데이터베이스 역활을 한다.
    3. JSON Server 실행
        - json-server --watch db.json
        - db.json파일의 변경을 감지하려면 watch 옵션을 추가한다.
    4. GET 요청
    5. POST 요청
        - POST 요청시에는 setRequestHeader메서드를 사용하여 요청 몸체에 담아 전송할 페이로드의 타입을 지정해야 한다.
    6. PUT 요청 
        - 특정 리소스 전체를 교체할 때 사용한다.
        - PUT 요청시에는 setRequestHeader메서드를 사용하여 요청 몸에체 담아 전송할 페이로드의 타입을 지정해야 한다.
    7. PATCH 요청
        - 특정 리소스의 일부를 수정할 때 사용한다.
    8. DELETE 요청
