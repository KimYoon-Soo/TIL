# React는 무엇인가?
### 프론트엔드 라이브러리
- 3대장 (React, Angular, Vue)...

- 뭐가 가장 좋다 이런 개념은 없다.<br>
  개발자 자신이 가장 잘하고 좋은걸로 하면 된다.

- 각 라이브러리나 Framework들을 기초 수준이라도 한번씩은 사용해보는 것을 권장

- 각 도구들의 철학과 추구하고자 하는 방향이 다름

#### Angular
- 다양한 기능이 이미 내장<br>
  즉, 이거 하나만으로 많은 것들을 만들 수 있다.

- Framework 차원에서는 매우 성숙

- 인지도 측면에서는 아직 성장중<br>
  Main으로 사용하는 개발자가 적음

- TypeScript 사용이 기본

#### React
- Component라는 개념에 집중이 되어있는 라이브러리

- Framework가 아님

- 공식 라이브러리 이런 개념이 딱히 없음

- 생태계가 굉장히 넓고 뜨겁다.

- 많은 기업에서 사용중

#### Vue
- 입문자가 사용하기에 쉬움

- 그냥 CDN으로 불러와서도 자주 사용

- 공식 Router와 공식 상태 관리 라이브러리가 존재

- Angular와 React에서 좋은 것들은 몇가지씩 가져와서 짬뽕해둔 느낌

### React의 Virtual DOM
- '우리는 지속해서 데이터가 변화하는 대규모 어플리케이션을 구축하기 위해 React를 만들었습니다.'

- 다양한 패턴들의 공통점 : Model<br>
  양방향 Binding (View ↔ Model)

- 변화 (Mutation)<br>
  그냥 Mutation을 하지 말자!!<br>
  그 대신에, 데이터가 바뀌면 그냥 View를 날려버리고 새로 만들면 어떨까?<br>
  하지만 그때 그때 View를 만들면 너무 성능 저하가 발생

- 그래서 필요한 것이 Virtual DOM

- 즉, 변화가 발생하면 Virtual DOM에 먼저 Rendering하고 그 다음에 진짜 DOM과 비교하여 변화가 필요한 곳만 Update

### React를 특별하게 만드는 점
- React에서만 Virtual DOM을 사용하는가?<br>
  아니다. Vue, Marko, Maquette 등등 여러 라이브러리에서 사용중

- 그렇다면 무엇이 React를 특별하게 만드는가?

1. 어마어마한 생태계 (JQuery 등장 초반과 유사, 2018년 기준)

1. 사용하는 곳이 많다.<br>

1. 한번 사용하면 좋아하게 된다.