# react-tictactoe-tutorial

리액트 튜토리얼 따라하기 : [공홈의 튜토리얼](https://ko.reactjs.org/tutorial/tutorial.html)을 따라가면서 배우 내용을 정리합니다.

* 완성본 : https://codepen.io/gaearon/pen/gWWZgR
* 스켈레톤 : https://codepen.io/gaearon/pen/oWWQNa


## Step 1 : [사용자와 상호작용하는 컴포넌트 만들기](https://ko.reactjs.org/tutorial/tutorial.html#making-an-interactive-component)

* Square 클래스(컴포넌트)에 생성자를 만들고 속성(state)을 추가했다.
* Square 컴포넌트에 onClick 이벤트를 연결했다.

> 변경된 코드 [#1](https://github.com/samsee/react-tictactoe-tutorial/pull/1)

## Step 2 : [순서 만들기](https://ko.reactjs.org/tutorial/tutorial.html#completing-the-game)

* 상태를 Square 컴포넌트에서 Board 컴포넌트로 관리하도록 변경했다.
* Board의 상태와 이벤트 핸들러를 Square 컴포넌트로 전달했다.
* Square 컴포넌트를 함수 컴포넌트로 리팩토링했다.

> 변경된 코드 #2

## *Step 3*



## *Step 4*


## *Step n*



# 배운 것들

* React란? 선언적이고 효율적이며 유연한 JS 라이브러리
* React 컴포넌트란? 작고 고립된 코드의 파편. `React.Component` 클래스를 상속받는다.
* 데이터가 변경될 때 React는 컴포넌트를 효율적으로 업데이트하고 다시 렌더링합니다
* 컴포넌트를 정의할 때 [JSX](https://ko.reactjs.org/docs/introducing-jsx.html)라는 표현식을 사용할 수 있다. 현재로서는 html을 확장한 표현식 같아 보인다.
* Javascript에서는 constructor 함수로 생성자를 정의할 수 있다. 항상 super를 해야 한다고..
* 컴포넌트의 state로 상태를 저장할 수 있다.
* 다른 컴포넌트로 상태와 함수를 전달할 수 있다.
* 

# 현재 모르는 것들/궁금한 것들

- [ ] Javascript : [이걸](https://developer.mozilla.org/ko/docs/web/javascript/a_re-introduction_to_javascript) 보란다. 
  - [ ] 클래스와 상속
  - [ ] let, const
  - [ ] 화살표 함수(=>) : 람다 관련인 것 같은데..
  - [ ] constructor
  - [ ] 세미콜론과 괄호, 중괄호 : 옛날에도 헷갈려는데 더 헷갈려진 것 같아..
  - [ ] Object, assign, 객체 spread?? : 이거 언제 생겼데
  - [ ] 이 코드 뭐지 : `if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c])`
  - [ ] 조건문에서 false로 평가되는 경우 : false, null(흠..), 또 뭐 있지?
- [ ] 리액트
  - [ ] 스코프 : 소스 뒤쪽에서 정의한 함수도 참조가 된다. 원래 이게 됐었나? 예전엔 순차적으로 했던 것 같은데..
  - [ ] 배열, 이터레이터의 key property : 이건 전에 Vue 쪽에서 봤는데.. 같은건가?