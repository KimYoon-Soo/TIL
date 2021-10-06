# HTTP 메서드
## 좋은 URI 설계란?
- 예시<br>
 . 회원 목록 조회 /read-member-list<br>
 . 회원 조회 /read-member-by-id<br>
 . 회원 등록 /create-member<br>
 . 회원 수정 /update-member<br>
 . 회원 삭제 /delete-member

- 가장 중요한 것은 **Resource 식별**

- Resource란?
 . 회원을 등록하고 수정하고 조회하는게 리소스가 아니다!<br>
 . 예) 미네랄을 캐라 → 미네랄이 Resource<br>
 . 회원이라는 개념 자체가 바로 Resource

- Resource를 어떻게 식별하는게 좋을까?
 . 회원을 등록하고 수정하고 조회하는 것을 모두 배제<br>
 . 회원이라는 Resource만 식별하면 됨 → 회원 Resource를 URI에 매핑

- 위 예시를 Resource에 포커싱하면?
 . **회원** 목록 조회 /members<br>
 . **회원** 조회 /members/{id}<br>
 . **회원** 등록 /members/{id}<br>
 . **회원** 수정 /members/{id}<br>
 . **회원** 삭제 /members/{id}<br>
 . 참고 : 계층 구조상 상위를 컬렉션으로 보고 복수단어 사용 권장 (member → members)<br>
 . 그렇다면 조회, 등록, 수정, 삭제는 **어떻게 구분하지??**

- Resource와 행위를 분리
 . **가장 중요한 것은 리소스를 식별하는 것**<br>
 . URI는 Resource만 식별!<br>
 . Resource와 해당 Resource를 대상으로 하는 행위를 분리<br>
   . Resource : 회원<br>
   . 행위 : 조회, 등록, 삭제, 변경<br>
 . Resource는 명사, 행위는 동사 (미네랄을 캐라)

## HTTP 메서드 종류
- GET : Resource 조회
 
- POST : 요청 데이터 처리, 주로 등록에 사용
 
- PUT : Resource를 대체, 해당 Resource가 없으면 생성
 
- PATCH : Resource 부분 변경
 
- DELETE : Resource 삭제
 
- HEAD : GET과 동일하지만 메세지 부분을 제외하고, 상태 줄과 헤더만 반환

- OPTIONS : 대상 Resource에 대한 통신 가능 옵션(메서드)을 설명 (주로 CORS에서 사용, 이런게 있구나 정도로 참고)

- 그 외에 CONNECT, TRACE 등이 더 있는데, 거의 사용하지 않음

## GET
- GET /search?q=hello&hl=ko HTTP/1.1<br>
  Host: www.<span></span>google.com

- Resource 조회

- 서버에 전달하고 싶은 데이터는 query를 통해서 전달

- 메세지 바디를 사용해서 데이터를 전달할 수 있지만, 지원하지 않는 곳이 많아서 권장하지 않음

## POST
- POST /members HTTP/1.1<br>
  Content-Type: application/json<br>
  {<br>
    "username": "hello",<br>
    "age": 20<br>
  }

- 요청 데이터 처리

- **메세지 바디를 통해 서버로 요청 데이터 전달**

- 서버는 요청 데이터를 **처리**
 . 메세지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행

- 주로 전달된 데이터로 신규 Resource 등록, 프로세스 처리에 사용

#### POST는 요청 데이터를 어떻게 처리한다는 뜻일까?
- POST 메서드는 **대상 Resource가 Resource의 고유한 의미 체계에 따라 요청에 포함된 표현을 처리하도록 요청**

- 예시)<br>
 . HTML 양식에 입력된 필드와 같은 데이터 블록을 데이터 처리 프로세스에 제공<br>
   (HTML FORM에 입력한 정보로 회원 가입, 주문 등에서 사용)<br>
 . 게시판, 뉴스 그룹, 메일링 리스트, 블로그 또는 유사한 기사 그룹에 메세지 게시<br>
   (게시판 글쓰기, 댓글 달기)<br>
 . 서버가 아직 식별하지 않은 새 Resource 생성<br>
   (신규 주문 생성)<br>
 . 기존 자원에 데이터 추가<br>
   (한 문서 긑에 내용 추가하기)

- **정리 : 이 Resource URI에 POST 요청이 오면 요청 데이터를 어떻게 처리할지 Resource마다 따로 정해야함**
 . 정해진 것이 없다.

#### POST 정리
1. 새 Resource 생성(등록)
 . 서버가 아직 식별하지 않은 새 Resource 생성

1. 요청 데이터 처리<br>
 . 단순히 데이터를 생성하거나, 변경하는 것을 넘어서 프로세스를 처리해야 하는 경우<br>
 . 예) 주문에서 결제 완료 → 배달 시작 → 배달 완료 처럼 단순히 값 변경을 넘어 프로세스의 상태가 변경되는 경우<br>
 . POST의 결과로 새로운 Resource가 생성되지 않을 수도 있음<br>
 . 예) POST /ordes/{orderId}/start-delivery **(컨트롤 URI)**

1. 다른 메서드로 처리하기 애매한 경우
 . 예) JSON으로 조회 데이터를 넘겨야 하는데, GET 메서드를 사용하기 어려운 경우<br>
 . 애매하면 POST

## PUT
- PUT /members/100 HTTP/1.1<br>
  Content-Type: application/json<br>
  {<br>
    "username": "hello",<br>
    "age": 20<br>
  }

- Resource를 대체<br>
 . Resource가 있으면 대체<br>
 . Resource가 없으면 생성<br>
 . 쉽게 이야기해서 덮어버림

- **클라이언트가 Resource를 식별**<br>
 . 클라이언트가 Resource 위치를 알고 URI 지정<br>
 . POST와 차이점

- **주의 - Resource를 완전히 대체**

## PATCH
- PATCH /members/100 HTTP/1.1<br>
  Content-Type: application/json<br>
  {<br>
    "age":50<br>
  }

 - Resource 부분 변경

## DELETE
- PATCH /members/100 HTTP/1.1<br>
  Host: localhost:8080

- Resource 제거

## HTTP 메서드의 속성
- 안전 (Safe Methods)

- 멱등 (Idempotent Methods)

- 캐시 가능 (Cacheable Methods)

#### 안전 (Safe)
- 호출해도 Resource를 변경하지 않는다.

- Q. 그래도 계속 호출해서, 로그 같은게 쌓여서 장애가 발생하면요?

- A. 안전은 해당 Resource만 고려한다. 그런 부분까지는 고려하지 않는다.

#### 멱등 (Idempotent)
- f(f(x)) = f(x)

- 한 번 호출하든 두 번 호출하든 100번 호출하든 결과가 똑같다.

- 멱등 메서드
 . GET : 한번 조회하든, 두번 조회하든 같은 결과가 조회<br>
 . PUT : 결과를 대체, 따라서 같은 요청을 여러번 해도 최종 결과는 동일<br>
 . DELETE : 결과를 삭제, 같은 요청을 여러번 해도 삭제된 결과는 동일<br>
 . POST : **멱등이 아님**, 두번 호출하면 같은 결제가 중복 발생

- 활용
 . 자동 복구 메커니즘<br>
 . 서버가 TIMEOUT 등으로 정상 응답을 못주었을 떄, 클라이언트가 같은 요청을 다시 해도 되는가? 판단의 근거

- Q. 재요청 중간에 다른 곳에서 Resource를 변경해버리면?<br>
 . 사용자1: GET → username: A, age: 20<br>
 . 사용자2: PUT → username: A, age: 30<br>
 . 사용자1: GET → username: A, age: 30 → 사용자2의 영향으로 바뀐 데이터 조회

- A. 멱등은 외부 요인으로 중간에 Resource가 변경되는 것까지는 고려하지 않음

#### 캐시 가능 (Cacheable)
- 응답 결과 Resource를 캐시해서 사용해도 되는가?

- GET, HEAD, POST, PATCH 캐시가능

- 실제로는 GET, HEAD 정도만 캐시로 사용<br>
 . POST, PATCH는 본문 내용까지 캐시 키로 고려해야 하는데, 구현이 쉽지 않음
