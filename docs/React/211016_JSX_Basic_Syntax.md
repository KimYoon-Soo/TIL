# JSX 기본 문법
#### JSX
- HTML처럼 보이지만 Javascript로 변환됨

- 지켜할 규칙이 몇가지 있음
**1. 태그는 꼭 닫혀 있어야 함**<br>
  . Self-Closing 태그도 반드시 닫아야함 (ex. ``<input/>, <br/>`` 등)
``` javascript
class App extends Component {
  render() {
    return (
      <div>
        <input type="text"> // 에러 발생
      </div>
    );
  }
}
```

**2. 감싸져 있는 엘리먼트**<br>
  . 2개 이상의 엘리먼트는 무조건 하나의 엘리먼트로 감싸져있어야 함
``` javascript
class App extends Component {
  render() {
    return (
      // 이렇게 2개 이상의 엘리먼트를 다른 엘리먼트로 감싸두지 않으면 에러 발생
      <div>Hello</div>
      <div>Bye</div>
    );
  }
}
```
  . ``Fragment``라는 것이 새로 도입되어서 사용하면 됨<br>
    (상단에 Fragment import 추가)
``` javascript
class App extends Component {
  render() {
    return (
      <Fragment>
        <div>Hello</div>
        <div>Bye</div>
      </Fragment>
    );
  }
}
```

**3. JSX 안에서 Javascript 값 사용하기**
``` javascript
class App extends Component {
  render() {
    const name = 'react';
    return <div>hello {name}!</div>; // 이런식으로 사용하면 됨
  }
}
```

**4. 조건부 렌더링**
- 삼항연산자 사용
``` javascript
class App extends Component {
  render() {
    return <div>{1 + 1 === 2 ? <div>맞아요!</div> : <div>틀려요!</div>}</div>;
  }
}
```
- && 연산자 사용<br>
  . Javascript에서 ```true && expression```은 항상 ```expression```으로 평가되고 ```false && expression```은 항상 ```false```로 평가됨
``` javascript
class App extends Component {
  render() {
    const name = 'velopert';
    return name === 'velopert' && <div>벨로퍼트다!</div>;
  }
}
```
- function 사용 (IIFE)
``` javascript
class App extends Component {
  render() {
    const value = 1;
    return (
      <div>
        {
          (function () {
            if (value === 1) return <div>1이다!</div>;
            if (value === 2) return <div>2이다!</div>;
            if (value === 3) return <div>3이다!</div>;
            return <div>없다!</div>;
          })()
        }
      </div>
    );
  }
}
```
``` javascript
class App extends Component {
  render() {
    const value = 1;
    return (
      <div>
        // 화살표 함수를 사용하면 좀 더 깔끔해짐
        // 화살표 함수는 this, argument, super 이런 개념이 없음
        {(() => {
          if (value === 1) return <div>1이다!</div>;
          if (value === 2) return <div>2이다!</div>;
          if (value === 3) return <div>3이다!</div>;
          return <div>없다!</div>;
        })()}
      </div>
    );
  }
}
```

#### JSX에서 스타일 사용하기
- HTML에서는 스타일을 문자열로 넣었지만 React에서는 객체형태로 넣어줌
``` javascript
class App extends Component {
  render() {
    const style = {
      backgroundColor: 'black', // background-color 였던게 카멜 케이스로 바뀜
      padding: '16px',
      color: 'white',
      fontSize: '36px'
      //fontSize: 5 + 10 + 'px' // 이런식으로 Javascript를 사용할 수도 있음
    };

    return <div style={style}>안녕하세요!</div>;
  }
}
```

- 스타일의 class 사용하기
``` javascript
return (
      // class가 아니라 className으로 해야함
      // class로도 작동은 하지만 className이 올바른 Convention임
      <div className="App"> 
        안녕하세요!
      </div>
    );
```

--- JSX 주석 작성하기
``` javascript
class App extends Component {
  render() {
    // 일반적인 javascript 주석 방법
    return (
      <div>
        // 하지만 JSX 상에서는 그냥 랜더링이 되어버림 
        /* 
          멀티라인도 예외가 아니다!
        */
        {/* 
          이런식으로 멀티라인 주석에서 { }을 한번 감싸줘야함
        */}
        <h1 
          something="어쩌구저쩌구" // 태그 사이 주석은 이런식으로!!
        >
          리액트
        </h1>
      </div>
    );
  }
}
```

#### Javascript 문법
**1. let**
- 아래 예시와 같이 scope({})가 함수 단위여서 문제가 발생

- let과 const는 scope가 블록 단위

- 그렇기에 let을 사용하는 것을 권장

``` javascript
function foo() {
    var a = 'hello';
    if (true) {
        var a = 'bye';
        console.log(a); // bye
    }
    console.log(a); // bye
}
```

``` javascript
function foo() {
    let a = 'hello';
    if (true) {
        let a = 'bye';
        console.log(a); // bye
    }
    console.log(a); // hello
}
```

**2. var vs const vs let**
- var는 더 이상 사용 X

- const : 한번 선언 후 고정적인 값

- let : 유동적인 값
