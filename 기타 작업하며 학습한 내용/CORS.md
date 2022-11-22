## CORS

- 교차 출저 리소스 공유로 웹페이지 상의 제한된 리소스를 최초 자원이 서비스된 도메인 밖의 다른 도메인으로 부터 요청할 수 있게 허용하는 구조
- 특정 교차 도메인 간 요청은 기본적으로 금지됩니다.
- 출처(Origin)란 URL구조에서 Protocal, Host, Port를 합친 것을 말합니다.
- 개발도구에서 location.origin을 실행하면 출처를 확인할 수 있습니다.

## 동일 출처 정책(Same-Origin Policy)

- 브라우저에서 발생하는 현상으로 다른 출처의 리소스 접근을 금지하는 현상
- 장점으로는 XSS나 XSRF등의 보안 취약점을 노린 공격을 방어할 수 있습니다.

## CORS의 동작원리

- 브라우저는 다른 Origin으로 요청을 보낼 때 Origin 헤더에 자신의 Origin을 설정하고 Access-Control-Allow-Origin 헤더에 설정된 목록이 Oringin헤더 값과 같은지 확인하는 것이다.

## CORS 에러 해결 방법

- 웹 브라우저 실행 옵션이나 플로그인을 통한 동일 출처 정책 회피하기
- jsonp 방식으로 json데이터 가져오기
- 서버에서 Access-Control-Allow-Origin 세팅하기
- axios의 경우 withCredentials 옵션부분을 전역 설정하여 처리하거나 옵션 인자로 넣어 보낼수 있습니다.

```js
// 1. axios 전역 설정
axios.defaults.withCredentials = true; // withCredentials 전역 설정
```

- node 서버의 경우 cors 모듈을 사용하여 해결할 수 있습니다.
