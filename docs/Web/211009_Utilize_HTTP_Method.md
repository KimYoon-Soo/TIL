# HTTP 메서드 활용
#### 클라이언트에서 서버로 데이터 전송
<b> 데이터 전달 방식은 크게 2가지 </b>

1. **쿼리 파라미터를 통한 데이터 전송**<br>
 . GET<br>
 . 주로 정렬 필터(검색어)

1. **메세지 바디를 통한 데이터 전송**<br>
 . POST, PUT, PATCH<br>
 . 회원 가입, 상품 주문, Resource 등록, Resource 변경

<b> 4가지 상황 </b>

1. **정적 데이터 조회**<br>
``` 
GET /static/star.jpg HTTP/1.1
Host: localhost:8080
``` 
 . 이미지, 정적 텍스트 문서<br>
 . 조회는 GET 사용<br>
 . 정적 데이터는 일반적으로 쿼리 파라미터 없이 Resource 경로로 단순하게 조회 가능

1. **동적 데이터 조회**
``` 
GET /search?q=hello&hl=ko HTTP/1.1
Host: www.google.com
``` 
 . 주로 검색, 게시판 목록에서 정렬 필터 (검색어)<br>
 . 조회 조건을 줄여주는 필터, 조회 결과를 정렬하는 조건에 주로 사용<br>
 . 조회는 GET 사용<br>
 . GET은 쿼리 파라미터 사용해서 데이터 전달

1. **HTML Form을 통한 데이터 전송**<br>
 . HTML Form submit시 POST전송<br>
 &nbsp;&nbsp;(회원 가입, 상품 주문, 데이터 변경)<br>
 . Content-Type: application/x-www-form-urlencoded 사용<br>
 &nbsp;&nbsp;. form의 내용을 메세지 바디를 통해서 전송(key = value, 쿼리 파라미터 형식)<br>
 &nbsp;&nbsp;. 전송 데이터를 url encoding 처리<br>
 &nbsp;&nbsp;&nbsp;&nbsp;. ex) abc김 → abc%EA%B9%80<br>
 . HTML Form은 GET 전송도 가능<br>
 . Content-Type: multipart/form-data<br>
 &nbsp;&nbsp;. 파일 업로드 같은 바이너리 데이터 전송시 사용<br>
 &nbsp;&nbsp;. 다른 종류의 여러 파일과 폼의 내용 함께 전송 가능(그래서 이름이 multipart)<br>
 . 참고 : HTML Form 전송은 GET, POST만 지원

1. **HTTP API를 통한 데이터 전송**<br>
 . 서버 to 서버<br>
 &nbsp;&nbsp;. 백엔드 시스템 통신<br>
 . 앱 클라이언트<br>
 &nbsp;&nbsp;. 아이폰, 안드로이드<br>
 . 웹 클라이언트<br>
 &nbsp;&nbsp;. HTML에서 Form 전송 대신 Javascript를 통한 통신에 사용(AJAX)<br>
 &nbsp;&nbsp;. ex) React, VueJs 같은 웹 클라이언트와 API 통신<br>
 . POST, PUT, PATCH : 메세지 바디를 통한 데이터 전송<br>
 . GET : 조회, 쿼리 파라미터로 데이터 전달<br>
 . Content-Type : application/json을 주로 사용 (사실상 표준)<br>
 &nbsp;&nbsp;. TEXT, XML, JSON 등등
 