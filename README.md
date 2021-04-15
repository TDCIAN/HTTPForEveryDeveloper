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

- 비 연결성(connectionless)
- HTTP 메시지


### 7. HTTP 메서드


### 9. HTTP 메서드 활용
### 10. HTTP 상태코드
### 11. HTTP 헤더1 - 일반 헤더
### 12. HTTP 헤더2 - 캐시와 조건부 요청



