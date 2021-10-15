# React 프로젝트 시작하기
- 초기 단계에서는 아래의 도구들을 직접 건드릴 일이 없음

- 그냥 아래의 도구들이 사용되고 있다 정도로만 이해하면 됨

- codesandbox에서 이것 저것 테스트 해보면 좋음

#### Webpack
- 코드들을 의존하는 순서대로 잘 합쳐서 하나 또는 여러개의 파일로 결과물을 만들어냄

- 웹 프로젝트를 만들때, 전체적으로 파일들을 관리해주는 도구 정도로 이해하면 됨

#### Babel
- Javascript 변환 도구

- 최신 버전의 Javascipt 문법을 Browser에 대중적인 이전 버전의 문법으로 변환 시켜줌

#### React 프로젝트 기초
``` javascript
// React모듈이 설치되어 있는데, 그걸 불러와서 사용하겠다는 의미
// React를 사용할때는 꼭 import React로 불러와줘야함
import React, { Component } from 'react'; 

// Component를 만드는 방법은 2가지가 있는데, 그 중 첫번째 방법이 class
// 다른 방법은 function을 통해서 생성
class App extends Component {
  // render 메서드는 꼭 JSX 형태의 코드를 return 해야함
  render() {
    return (
      <div>
        <h1>안녕하세요 리액트</h1>
      </div>
    );
  }
}

export default App;
```