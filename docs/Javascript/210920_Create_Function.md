# 함수 만들기
### 1. 함수 선언
- 함수 선언 또는 정의는 function 키워드 사용, 그 뒤에 함수 이름이 옴
``` javascript
    fucntion logCompliment() {
        consloe.log("잘했어요!");
    }
```

### 2. 함수 표현식 (Function Expression)
- 이름이 없는 함수를 만들며, 변수에 값을 대입할 수 있음<br>
  (무명 메서드 느낌?)
``` javascript
    const logCompliment = function() {
        console.log("잘했어요");
    }
    logCompliment();
```

- 그렇다면 함수 선언과 함수 표현식 중 어떤쪽을 사용해야하는가?<br>
  → 함수 선언은 호이스팅되지만 함수 표현식은 그렇지 않음<br>
  → 따라서 함수 선언을 작성하기 전에 함수를 호출해도 됨, 하지만 함수 표현식은 함수 표현식이 실행되기 전에는 호출 불가능
``` javascript
// 선언하기 전에 함수를 호출한다.
hey();
// 함수 선언
function hey() {
    alert("hey!"); // ** TypeError: hey is not a function **
}
```
- 프로젝트에서 함수나 파일을 import 할 때도 TypeError가 발생하곤 함<br>
  이런 오류를 본다면 항상 함수 선언으로 Refactoring필요

#### 인수 넘기기
