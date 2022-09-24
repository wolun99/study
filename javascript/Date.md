## Date
- 빌트인 객체인 Date는 날짜와 시간을 위한 메서드를 제공하는 빌트인 객체이며 생성자 함수이다.
- UTC(협정 세계시)를 기준으로 한다.
- KST(한국 표준시)는 UTC에 9시간을 더한 시간이다.
## Date 생성자 함수
- Date는 생성자 함수이다.
- 객체 내부적으로 날짜와 시간을 나타내는 값을 갖는데 1970년 1월 1일 00:00:00을 기점으로 나타낸다.
- Date 생성자 함수로 객체를 생성하는 방업은 4가지가 있다.
    1. new Date()
        - 생성자 함수를 인수 없이 new 연산자와 호출하면 현재 날짜와 시간을 가지는 객체를 반환한다.
        - new 연산자 없이 호출하면 날짜와 시간정보를 나타내는 문자열을 반환한다.
    2. new Date(milliseconds)
        - Date 함수에 숫자 타입의 밀리초를 인수로 전다랗면 1970년 1월1일 00:00:00을 기점으로 인수로 전달된 시간만큼 지난 객체를 반환한다.
    3. new Date(dateString)
        - Date 생성자 함수에 날짜와 시간을 문자열로 인수 전달하면 지정된 날짜와 시간을 나타내는 객체를 반환한다. 이때 전달한 문자열은 Date.parse 메서드에 의해 해석 가능한 형식이여야 한다.
    4. new Date(year,month[,day,hour,minute,second,millisecond])
        - 연,월,일,시,분,초,밀리초를 의미하는 수자를 인수로 전다랗면 지정된 날짜와 시간을 나타내는 객체를 반환한다. 이때 연,월은 반드시 지정해야 한다
## Date 메서드 
1. Date.now
    - 1970년 1월 1일 00:00:00을 기점으로 현재 시간까지 경과한 밀리초를 숫자로 변환한다.
2. Date.parse
    - 1970년 1월 1일 00:00:00을 기점으로 인수로 전달된 지정 시간까지의 밀리초를 숫자로 반환한다.
3. Date.UTC
    - 1970년 1월 1일 00:00:00을 기점으로 인수로 전달된 지정 시간까지의 밀리초를 숫자로 반환한다.
    - 기준이 KST가 아닌 UTC임을 주의하자
4. Date.prototype.getFullyear
    - 연도를 나타내는 정수를 반환한다.
5. Date.prototype.getFullyear
    - 연도를 나타내는 정수를 설정한다. 연도 이외에 월,일도 설정할 수 있다.
6. Date.prototype.getMonth
    - 월을 나타내는 0~11의 정수를 반환한다.
7. Date.prototype.setMonth
    - 월을 나타내는 0 ~ 11 의 정수를 설정한다. 옵션으로 일도 가능
8. Date.prototype.getDate
    - 날짜를 나타내는 정수를 반환
9. Date.prototype.setDate
    - 날짜를 나타내는 정수를 설정한다.
10. Date.prototype.getDay
    - 요일을 나타내는 정수를 반환한다.
11. Date.prototype.getHour
    - 시간을 나타내는 정수를 반환한다.
12. Date.prototype.setHour
    - 시간을 나타내는 정수를 설정한다. 시간 외에도 옵션으로 분, 초 ,밀리초도 설정할 수 있다.
13. Date.prototype.getMinutes
    - 분을 나타내는 정수를 반환한다.
14. Date.prototype.setMinutes
    - 분을 나타내는 정수를 설정한다. 분 이외에 옵션으로 초,밀리초도 설정할 수 있다.
15. Date.prototype.getSeconds
    - 초를 나타내는 정수를 반환한다.
16. Date.prototype.setSeconds
    - 초를 나타내는 정수를 설정한다. 초 이외에 옵션으로 밀리초도 설정할 수 있다.
17. Date.prototype.getMilliseconds
    - 밀리초를 나타내는 정수를 반환한다.
18. Date.prototype.setMilliseconds
    - 밀리초를 나타내는 정수를 설정한다.
19. Date.prototype.getTime
    - 1970년 1월 1일 00:00:00을 기점으로 경과한 밀리초를 반환한다.
20. Date.prototype.setTime
    - 1970년 1월 1일 00:00:00을 기점으로 경과된 밀리초를 설정한다.
21. Date.prototype.getTimezoneOffset
    - 로캘시간과의 차이를 분단위로 반환한다.
22. Date.prototype.toDateString
    - 사람이 읽을 수 있는 형식의문자열로 Date 객체와 날짜를 반환한다.
23. Date.prototype.toTimeString
    - 사람이 읽을 수 있는 형식으로 Date 객체의 시간을 표현한 문자열을 반환한다.
24. Date.prototype.toISOString
    - ISO 8601 형식으로 날짜와 시간을 표현한 문자열을 반환한다.
25. Date.prototype.toLocaleString
    - 인수로 전달한 로캘을 기준으로 Date 객체의 날짜와 시간을 문자열로 반환한다. 인수를 생략하면 브라우저가 알아서 지정한다.
26. Date.prototype.toLocaleTimeString
    - 인수로 전달한 로캘을 기준으로 Date 객체의 시간을 표현한 문자열을 반환한다.