# URI와 Web 브라우저 요청 흐름
## URI란?
- Uniform Resource Identifier<br>
  - Uniform : 리소스 식별하는 통일된 방식<br>
  - Resource : 자원, URI로 식별할 수 있는 모든 것 (제한 없음)<br>
  - Identifier : 다른 항목과 구분하는데 필요한 정보

- 로케이터(Locator), 이름(Name) 또는 둘 다 추가로 분류될 수 있다.
  
- URI(Resource Identifier) = URL(Resource Locator, 리소스가 있는 위치를 저장) + URN(Resource Name, 리소스에 이름을 부여)

- 거의 URL만 사용, URN은 이런게 있구나 정도로만 이해<br>
  (URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음)

- 그래서 사실 URI = URL이라고 봐도 됨

## URL Scheme
- scheme://[userinfo@]host:[port][/path][?query][#fragment]<br>
  https:<span></span>//www.<span></span>google.com:443/serach?q=hello&hl=ko

- Scheme : 주로 프로토콜 사용<br>
  (프로토콜 : 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙)<br>
  (ex http, https, ftp 등)

- userinfo : URL에 사용자정보를 포함해서 인증해야하며 거의 사용하지 않음

- host : host명, 도메인명 또는 IP 주소를 직접 사용가능

- port : 접속 포트 (생략 가능)

- path : 리소스 경로, 계층적 구조<br>
  (ex home/file1.jpg, /members, /members/100, /itmes/iphone12)

- query = key, value 형태<br>
  ?로 시작, &로 추가 가능 ?keyA=valueA&keyB=valueB<br>
  query parameter, query strng 등으로 불림, 웹서버에 제공하는 파라미터, 문자 형태

- fragment : html 내부 북마크 등에 사용 (잘 사용하지 않음, 서버에 전송하는 정보 아님)

- https = http secure<br>
  (지금은 대부분의 웹사이트들이 https로 동작중)

## Web 브라우저 요청 흐름
1. DNS 조회 (www.<span></span>google.com:443 → IP : 200.200.200.2 + HTTPS port 생략, 443)

1. HTTP 요청 메세지 생성 (GET /serach?q=hello&hl=ko HTTP/1.1 Host:www.<span></span>google.com)

1. HTTP 메세지 전송
   1. Web 브라우저가 HTTP 메세지 생성
   1. Socket 라이브러리를 통해 전달
      - A : TCP/IP 연결 (IP, PORT)
      - B : 데이터 전달

1. TCP/IP 패킷 생성 (HTTP 메세지 포함)

1. 네트워크 인터페이스(LAN 장비 등)을 통하여 인터넷으로 전달하여 서버로 전달

1. 서버에서 TCP/IP 패킷을 받아서 까서 HTTP 메세지 확인

1. HTTP 응답 메세지를 웹 브라우저로 전달

1. Web 브라우저가 HTTP 응답 메세지를 까서 HTML 렌더링
