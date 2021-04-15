## HTTPForEveryDeveloper


based on this lecture: 
<br>https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC


### 1. 인터넷 네트워크

인터넷 프로콜 스택의 4계층
- 애플리케이션 계층: HTTP, FTP
- 전송 계층: TCP, UDP
- 인터넷 계층: IP
- 네트워크 인터페이스 계층

* TCP / IP 패킷 정보
- 패킷: 패키지(package)와 버킷(bucket)의 합성어
- TCP(전송 제어 프로토콜, Transmission Control Protocol) 특징
  - 연결 지향 - TCP 3 way handshake (가상 연결)
  - 데이터 전달 보증
  - 순서 보장
  - 신뢰할 수 있는 프로토콜
  - 현재는 대부분 TCP 사용
- UDP(사용자 데이터그램 프로토콜, User Datagram Protocol) 특징
  - 하얀 도화지에 비유(기능이 거의 없음)
  - 연결지향 - TCP 3 way handshake X
  - 데이터 전달 보증 X
  - 순서 보장 X
  - 데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠름
  - 정리
    - IP와 거의 같다. + PORT + 체크섬 정도만 추가
      * PORT: 하나의 IP에서 여러 애플리케이션을 동작시키는 상황에서 애플리케이션별 패킷을 구분할 수 있게 해줌
        - 단어 뜻은 항구(Port)에서 유래
      * 체크섬: 메시지가 맞는지 검증해주는 역할
    - 애플리케이션에서 추가 작업 필요

- PORT
  - 같은 IP 내에서 프로세스 구분
  - IP를 아파트라고 치면, PORT는 몇 동 몇 호에 해당
  - 0 ~ 65535 할당 가능
  - 0 ~ 1023: 잘 알려진 포트, 사용하지 않는 것이 좋음
    - FTP: 20, 21
    - TELNET: 23
    - HTTP: 80
    - HTTPS: 443

- DNS(도메인 네임 시스템, Domain Name System)
  - IP는 기억하기 어렵다
  - IP는 변경될 수 있다(과거 IP, 신규 IP)
  - DNS는 일종의 전화번호부다
  - 도메인 명을 IP 주소로 변환해준다

- 인터넷 네트워크 정리
  - 인터넷 통신
  - IP(Internet Protocol)
  - TCP, UPD
  - PORT
  - DNS


### 3. URI와 웹 브라우저 요청 흐름
- URI(Uniform Resource Identifier)
  - URI, URL, URN
  - URI는 로케이터(Locator), 이름(Name) 또는 둘 다 추가로 분류될 수 있다.
  - URI 안에 URL(Uniform Resource Locator), URN(Uniform Resource Name)이 포함된다.
  - URN은 거의 안 쓰고 URL을 많이 쓴다고 생각하면 된다
  - URI 단어 뜻
    - Uniform: 리소스 식별하는 통일된 방식
    - Resource: 자원, URI로 식별할 수 있는 모든 것(제한 없음)
    - Identifier: 다른 항목과 구분하는데 필요한 정보

  - URL, URN 단어 뜻
    - URL: Locator - 리소스가 있는 위치를 지정
    - URN: Name - 리소스에 이름을 부여
    - 위치는 변할 수 있지만, 이름은 변하지 않는다.
    - urn:isbrn:8960777331 (어떤 책의 isbn URN)
    - URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음
    - 앞으로 URI를 URL과 같은 의미로 이야기 하겠음

  - URL 전체 문법
    - scheme://[userinfo@]host[:port][/path][?query][#fragment]
    - https://www.google.com:443/search?q=hello&hl=ko
    - 프로토콜(https)
    - 호스트명(www.google.com)
    - 포트 번호(443)
    - 패스(/search)
    - 쿼리 파라미터(q=hello&hl=ko)

  - scheme에 대한 설명(위 예시에서 https)
    - 주로 프로토콜 사용
    - 프로토콜: 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙(예: http, https, htp 등등)
    - http는 80 포트, https는 443 포트를 주로 사용, 포트는 생략 가능
    - https는 http에 보안 추가 (HTTP Secure)

  - userinfo에 대한 설명(위 예시에는 userinfo에 대한 설명 없음)
    - URL에 사용자정보를 포함해서 인증
    - 거의 사용하지 않음

  - host에 대한 설명(위 예시에서 www.google.com에 해당)
    - 호스트명
    - 도메인명 또는 IP 주소를 직접 사용가능

  - PORT에 대한 설명(위 예시에서 :443에 해당)
    - 포트(PORT)
    - 접속 포트
    - 일반적으로 생략, 생략시 http는 80, https는 443

  - path에 대한 설명(위 예시에서 search에 해당)
    - 리소스 경로(path), 계층적 구조
    - 예)
      - /home/file1.jpg
      - /members
      - /members/100
      - /items/iphone12

  - query에 대한 설명(위 예시에서 ?q=hello&hl=ko에 해당)
    - key=value 형태
    - ?로 시작, &로 추가 가능 -> ?keyA=valueA&keyB=valueB
    - query parameter, query string 등으로 불림, 웹서버에 제공하는 파라미터, 문자 형태

  - fragment에 대한 설명(위 예시에는 fragment 없음)
    - scheme://[userinfo@]host[:port][/path][?query][#fragment]
    - https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started.html#getting-started-introducing-spring-boot
    - 위 예시에서 #getting-started-introducing-spring-boot에 해당
    - html 내부 북마크 등에 사용
    - 서버에 전송하는 정보는 아님

- 웹 브라우저 요청 흐름
  - HTTP 요청 메시지 예시: GET /search?q=hello&hl=ko HTTP/1.1 Host: www.google.com
  - HTTP 응답 메시지 예시:
    HTTP/1.1 200 OK
    Content-Type: text/html;charset=UTF-8
    Content-Length: 3423
    <html>
      <body>...</body>
    </html>
  - HTTP 메시지 전송 순서
    1. 웹 브라우저가 HTTP 메시지 생성
    2. SOCKET 라이브러리를 통해 전달
      - A: TCP/IP 연결(IP, PORT)
      - B: 데이터 전달
    3. TCP/IP 패킷 생성, HTTP 메시지 포함


### 5. HTTP 기본 
- 모든 것이 HTTP
  - HTTP(HyperText Transfer Protocol)
    - HTTP 메시지에 모든 것을 전송
      - HTML, TEXT
      - IMAGE, 음성, 영상, 파일
      - JSON, XML(API)
      - 거의 모든 형태의 데이터 전송 가능
      - 서버간에 데이터를 주고 받을 때도 대부분 HTTP 사용
      - 지금은 HTTP 시대!

  - HTTP 역사
    - HTTP/0.9 - 1991년: GET 메서드만 지원, HTTP 헤더 X
    - HTTP/1.0 - 1996년: 메서드, 헤더 추가
    - HTTP/1.1 - 1997년: 가장 많이 사용, 우리에게 가장 중요한 버전
      - RFC2068 (1997년) -> RFC2616 (1999년) -> RFC7230~7235 (2014년)
    - HTTP/2 - 2015년: 성능 개선
    - HTTP/3 - 진행중: TCP 대신에 UDP 사용, 성능 개선

  - 기반 프로토콜
    - TCP: HTTP/1.1, HTTP/2
    - UDP: HTTP/3
    - 현재 HTTP/1.1 주로 사용
      - HTTP/2, HTTP/3도 점점 증가

  - HTTP 특징
    - 클라이언트 서버 구조
    - 무상태 프로토콜(스테이스리스), 비연결성
    - HTTP 메시지
    - 단순함, 확장 가능


- 클라이언트 서버 구조
  - Request Response 구조
  - 클라이언트는 서버에 요청을 보내고, 응답을 대기
  - 서버가 요청에 대한 결과를 만들어서 응답


- Stateful, Stateless
  - 무상태 프로토콜(스테이스리스, Stateless)
    - 서버가 클라이언트의 상태를 보존하지 않음
    - 장점: 서버 확장성 높음(스케일 아웃)
    - 단점: 클라이언트가 추가 데이터 전송

  - Stateful, Stateless 차이
    - 상태 유지(Stateful)
      - 고객: 이 노트북 얼마인가요?
      - 점원: 100만원 입니다. (노트북 상태 유지)
      - 고객: 2개 구매하겠습니다.
      - 점원: 200만원입니다. 신용카드, 현금중에 어떤 걸로 구매하시겠어요? (노트북, 2개 상태 유지)
      - 고객: 신용카드로 구매하겠습니다.
      - 점원: 200만원 결제 완료되었습니다. (노트북, 2개, 신용카드 상태 유지)
      
    - 무상태(Stateless)
      - 고객: 이 노트북 얼마인가요?
      - 점원: 100만원 입니다.
      - 고객: 노트북 2개 구매하겠습니다.
      - 점원: 노트북 2개는 200만원입니다. 신용카드, 현금중에 어떤 걸로 구매하시겠어요?
      - 고객: 노트북 2개를 신용카드로 구매하겠습니다.
      - 점원: 200만원 결제 완료되었습니다.

  - Stateful, Stateless 차이 정리
    - 상태 유지(Stateful): 중간에 다른 점원으로 바뀌면 안된다
      (중간에 다른 점원으로 바뀔 때 상태 정보를 다른 점원에게 미리 알려줘야 한다)
      - 항상 같은 서버가 유지되어야 한다.
      
    - 무상태(Stateless): 중간에 다른 점원으로 바뀌어도 된다.  
      - 갑자기 고객이 증가해도 점원을 대거 투입할 수 있다.
      - 갑자기 클라이언트 요청이 증가해도 서버를 대거 투입할 수 있다.
      - 아무 서버나 호출해도 된다.
    - 무상태는 응답 서버를 쉽게 바꿀 수 있다. -> 무한한 서버 증설 가능(스케일 아웃, 수평 확장)

  - Stateless의 실무적 한계
    - 모든 것을 무상태로 설계할 수 있는 것은 아니다 -> 경우에 따라 무상태로 설계할 수 없는 경우도 있음
    - 무상태
      - 예) 로그인이 필요 없는 단순한 서비스 소개 화면
    - 상태 유지
      - 예) 로그인
    - 로그인한 사용자의 경우 로그인 했다는 상태를 서버에 유지
    - 일반적으로 브라우저 쿠키와 서버 세션등을 사용해서 상태 유지
    - 상태 유지는 최소한만 사용

- 비 연결성(connectionless)
  - 연결을 유지하는 모델
    - 서버는 연결을 계속 유지해야 하므로 서버 자원 소모

  - 연결을 유지하지 않는 모델
    - 서버는 연결을 유지하지 않음. 최소한의 자원 유지

  - 비 연결성
    - HTTP는 기본적으로 연결을 유지하지 않는 모델
    - 일반적으로 초 단위 이하의 빠른 속도로 응답
    - 1시간 동안 수천명이 서비스를 사용해도 실제 서버에서 동시에 처리하는 요청은 수십개 이하로 매우 작음
      - 예) 웹 브라우저에서 계속 연속해서 검색 버튼을 누르지는 않는다.
    - 서버 자원을 매우 효율적으로 사용할 수 있음

  - 비 연결성의 한계와 극복
    - TCP/IP 연결을 새로 맺어야 함 -> 3 way handshake 시간 추가
    - 웹 브라우저로 사이트를 요청하면 HTML 뿐만 아니라 자바스크립트, css, 추가 이미지 등 수 많은 자원이 함께 다운로드
    - 지금은 HTTP 지속 연결(Persistent Connections)로 문제 해결
    - HTTP/2, HTTP/3에서 더 많은 최적화

  - HTTP 초기 - 연결, 종료 낭비
    클라이언트 <-> 서버
    - 연결 0.1초
    - 요청/HTML 응답 0.1초
    - 종료 0.1초

    - 다른 연결 0.1초
    - 다른 요청/HTML 응답 0.1초
    - 다른 종료 0.1초

    - 또 다른 연결 0.1초
    - 또 다른 요청/HTML 응답 0.1초
    - 또 다른 종료 0.1초
    -> 합 0.9초

  - HTTP 지속 연결(Persistent Connections)
    클라이언트 <-> 서버
    - 연결 0.1초
    - 요청 / HTML 응답 0.1초
    - 요청 / 자바스크립트 응답 0.1초
    - 요청 / 이미지 응답 0.1초
    - 종료 0.1초
    -> 합 0.5초
    
  - 스테이트리스를 기억하자
    - 서버 개발자들이 어려워하는 업무
    - 정말 같은 시간에 딱 맞추어 발생하는 대용량 트래픽
    - 예) 선착순 이벤트, 명절 KTX 예약, 학과 수업 등록
    - 예) 저녁 6:00 선착순 1000명 치킨 할인 이벤트 -> 수만명 동시 요청


- HTTP 메시지
  - HTTP 요청 메시지 예시
    GET /search?q=hello&hl=ko HTTP/1.1 
    Host: www.google.com
    
  - HTTP 응답 메시지 예시
    HTTP/1.1 200 OK
    Content-Type: text/html;charset=UTF-8
    Content-Length: 3423
    <html>
      <body>...</body>
    </html>

  - HTTP 메시지 구조
    start-line 시작 라인
      - 요청의 'GET /search?q=hello&hl=ko HTTP/1.1', 응답의 'HTTP/1.1 200 OK'에 해당
    header 헤더
      - 요청의 'Host: www.google.com', 응답의 'Content-Type: text/html;charset=UTF-8, Content-Length: 3423'에 해당
    empty line 공백 라인 (CRLF)
      - 요청과 응답의 헤더 아래
    message body
      - 응답에서 '<html> <body> ... </body> </html>'에 해당, 요청 메시지도 message body를 가질 수 있음

  - 시작 라인(요청 메시지)
    GET /search?q=hello&hl=ko HTTP/1.1
    Host: www.google.com
    
    - start-line = request-line과 status-line으로 구성
    - request-line = method SP(공백) request-target SP HTTP-version CRLF(엔터)
    - HTTP 메서드 (GET: 조회)
    - 요청 대상(/search?q=hello&hl=ko)
    - HTTP Version

    - 요청 메시지 - HTTP 메서드(위 예시에서 'GET'에 해당)
      - 종류: GET, POST, PUT, DELETE
      - 서버가 수행해야 할 동작 지정
        - GET: 리소스 조회
        - POST: 요청 내역 처리

    - 요청 메시지 - 요청 대상(위 예시에서 '/search?q=hello&hl=ko'에 해당)
      - absolute-path[?query] (절대경로[?쿼리])
      - 절대경로: "/"로 시작하는 경로
      - 참고: *, http://...?x=y와 같이 다른 유형의 경로지정 방법도 있다.

    - 요청 메시지 - HTTP 버전(위 예시에서 'HTTP/1.1'에 해당)
      - HTTP Version

    - 응답 메시지 (위 예시에서 'HTTP/1.1 200 OK'에 해당)
      - start-line = request-line과 status-line으로 구성
      - status-line = HTTP-version SP(공백) status-code SP(공백) reason-phrase CRLF
      - HTTP 버전
      - HTTP 상태 코드: 요청 성공, 실패를 나타냄
        - 200: 성공
        - 400: 클라이언트 요청 오류
        - 500: 서버 내부 오류
      - 이유 문구(위 예시에서 'OK'에 해당, reason-phrase): 사람이 이해할 수 있는 짧은 상태 코드 설명 글

    - HTTP 헤더 (위 예시에서 'Content-Type: text/html;charset=UTF-8, Content-Length:3423'에 해당)
      - header-field = field-name ":" OWS field-value OWS 
        * OWS: 띄어쓰기 허용
      - field-name은 대소문자 구분 없음
      - 용도
        - HTTP 전송에 필요한 모든 부가정보
          - 예: 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트(브라우저) 정보, 서버 애플리케이션 정보, 캐시 관리 정보 등
        - 표준 헤더가 너무 많음 (https://en.wikipedia.org/wiki/List of HTTP header fields)
        - 필요시 임의의 헤더 추가 가능
          - 예: helloworld: hihi

    - HTTP 메시지 바디 (위 예시에서 '<html> <body>...</body> </html>'에 해당)
      - 용도
        - 실제 전송할 데이터
        - HTML 문서, 이미지, 영상 JSON 등등 byte로 표현할 수 있는 모든 데이터 전송 가능

  - 단순함 확장 가능
    - HTTP는 단순하다. 스펙도 읽어볼만...
    - HTTP 메시지도 매우 단순
    - 크게 성공하는 표준 기술은 단순하지만 확장 가능한 기술
      
      

### 7. HTTP 메서드


### 9. HTTP 메서드 활용
### 10. HTTP 상태코드
### 11. HTTP 헤더1 - 일반 헤더
### 12. HTTP 헤더2 - 캐시와 조건부 요청



