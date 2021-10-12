# HTTP API 설계 예시

### HTTP API :: 컬렉션
- POST 기반 등록 (ex. 회원 관리 API 제공)
``` 
회원 목록 /members → GET
회원 등록 /members → POST
회원 조회 /members/{id} → GET
회원 수정 /members/{id} → PATCH, PUT, POST
회원 삭제 /members/{id} → DELETE
``` 
- 클라이언트는 등록될 Resource의 URI를 모른다.<br>
  . 회원 등록 /members → POST<br>
  . POST /memebers

- 서버가 새로 등록된 Resource URI를 생성해준다.<br>
``` 
HTTP/1.1 201 Created
Location: /members/100
```

- 컬렉션(Collection)<br>
  . 서버가 관리하는 Resource 디렉토리<br>
  . 서버가 Resource의 URI를 생성하고 관리<br>
  . 여기서 컬렉션은 /members

### HTTP API :: 스토어
- PUT 기반 등록 (ex. 정적 컨텐츠 관리, 원격 파일 관리)
``` 
파일 목록 /files → GET
파일 조회 /files/{filename} → GET
파일 등록 /files/{filename} → PUT
파일 삭제 /files/{filename} → DELETE
파일 대량 등록 /files → POST
``` 
- 클라이언트가 Resource URI를 알고 있어야 한다.<br>
  . 파일 등록 /files/{filename} → PUT<br>
  . PUT /files/star.jpg

- 클라이언트가 직접 Resource의 URI를 지정한다.

- 스토어(Store)<br>
  . 클라이언트가 관리하는 Resource 저장소<br>
  . 클라이언트가 Resource의 URI를 알고 관리<br>
  . 여기서 스토어는 /files

- 실제 사용빈도 매우 낮음, 대부분 POST 기반의 컬렉션을 사용 

### HTML FORM 사용
- HTML FORM은 **GET, POST만 지원**

- AJAX 같은 기술을 사용해서 해결 가능 → 회원 API 참고

- 여기서 순수 HTML, HTML FORM 이야기

- GET, POST만 지원하므로 제약이 있음
``` 
회원 목록 /members → GET
회원 등록 폼 /members/new → GET
회원 등록 /members/new, /members → POST
회원 조회 /members/{id} → GET
회원 수정 폼 /members/{id}/edit → GET
회원 수정 /members/{id} → POST
회원 삭제 /members/{id}/delete → POST
``` 
- **컨트롤 URI**<br>
  . GET, POST만 지원하므로 제약이 있음<br>
  . 이런 제약을 해결하기 위해 동사로 된 Resource 경로 사용<br>
  . POST의 /new, /edit, /delete가 컨트롤 URI<br>
  . HTTP 메서드로 해결하기 애매한 경우 사용(HTTP API 포함)<br>
  . 실제로 실무에서는 되게 많이 사용(어쩔 수 없이)

### 참고하면 좋은 URI 설계 개념
- https://resfulapi.net/resource-naming

#### 문서(document)
- 단일 개념(파일 하나, 객체 인스턴스, 데이터베이스 row)

- 예) /members/100, file/star.jpg

#### 컬렉션(collection)
- 서버과 관리하는 Resource 디렉터리

- 서버과 Resource의 URI를 생성하고 관리

- 예) /members

#### 스토어(store)
- 클라이언트가 관리하는 Resource 저장소

- 클라이언트가 Resource의 URI를 알고 관리

- 예) /files

#### 컨트롤러(controller), 컨트롤 URI
- 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행

- 동사를 직접 사용

- 예) /members/{id}/delete