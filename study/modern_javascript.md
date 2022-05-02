# Modern Javascript

[MDN의 JavaScript 재입문하기](https://developer.mozilla.org/ko/docs/web/javascript/a_re-introduction_to_javascript)와 [러닝 리액트 - LR](http://aladin.kr/p/KP4bH) 책 중 JavaScript 부분 정리
기존 JavaScript에 대한 내용은 생략함.

## JavaScript

* ECMA에서 표준을 관리. JavaScript -> ECMAScript
* 현재는 ES6(2015년, ES2015라고도 부르나봐)이 표준
* 그동안 많이도 바뀜.. 브라우저에서 HTML을 보조하기 위해 사용하다가, 현재는 서버 프로그래밍, NoSQL, Linux 데스크탑 환경에서도 사용됨.
* 최신 JS 스펙에 대한 브라우저의 호환성은 [kangax 호환성 표](https://kangax.github.io/compat-table/)를 참조


## 개요

* 다중 패러다임, 동적 언어
* 프로토타입 기반 객체지향 프로그래밍(ES2015부터 클래스 기반 객체지향)
* let : 블록 스코프를 가진 변수 만들기
* const : 상수
* var : 예전과 같다. let과 const는 제한을 가진 것으로 이해할 수 있다.
  * var 없이 하면 기존 처럼 글로벌로 되는건가?
* 템플릿 문자열 : \`$\{변수명\}, \$\{다른변수명\}, ..\`
  * \`...\` 안에서는 공백(개행문자도) 유지됨.

## 타입

* 내장 오류 타입 : 
* BigInt를 제외하고는 모두 실수(헉 처음 알았어..). 명백한 정수는 사실 암묵적으로 실수 라고 함.
* isNan으로 NaN 검사하지 말기([링크](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/isNaN#%ED%98%BC%EB%9E%80%EC%8A%A4%EB%9F%AC%EC%9A%B4_%ED%8A%B9%EB%B3%84_%EC%BC%80%EC%9D%B4%EC%8A%A4_%ED%96%89%EB%8F%99)). 대신 Number.isNaN() 사용하기.
* false로 평가 = false, 0, 빈 문자열, NaN, null, undefined. 거짓같은(falsy), 참같은(truthy)

## 제어

* == 으로 비교하지 말자(타입 강제 변환이 일어남). 값을 비교하려면 삼중 등호 연산자로(`===`, `!==`)
* for .. of : [iterator](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Iteration_protocols) 관련. 반복 가능한 객체. String 을 넣으면 한 글자씩..
* for .. in : 기존과 같다. 배열의 경우 인덱스를 반복(비어있는건 건너뜀). 

## 객체

* 기본적으로 이름-값 쌍. 이름 = JS 문자열
* 객체 리터럴 구문 : `var obj = {};`
* 참조하기 : 점 표기법, 대괄호 표기법 obj['name']
  * 이런건 주의 : 일부 JS 엔진과 압축기에서 적용할 수 없다.
  * `var user = prompt('Key?'); obj[user] = prompt('Value?');`
* bracket notation : `var userPhone = {}; userPhone[phoneType] = 12345` 대신 `var userPhone = {[phoneType]: 12345}` 이렇게 표현 가능

### 사용자 정의 객체

* 프로토타입 기반 : **함수** 를 클래스로 사용
* this의 참조 방식이 독특함. dot 표기법을 사용하지 않으면 전역 객체를 this로 사용할 수 있음.
* [참고하기](https://developer.mozilla.org/ko/docs/web/javascript/a_re-introduction_to_javascript#%EC%82%AC%EC%9A%A9%EC%9E%90_%EC%A0%95%EC%9D%98_%EA%B0%9D%EC%B2%B4)
* prototype은 모든 인스턴스간에 공유되는 객체.
  * lookup 체인의 일부

### 클래스

* 리액트는 클래스를 멀리하기 시작했고, 함수를 사용해 컴포넌트를 구성한다.
* ES2015 부터 클래스 선언이 추가되었지만 syntatic sugar 일 뿐 여전히 프로토타입 기반 상속으로 동작한다.

### 편의 기능

* [구조 분해 할당(destructuring)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) : LR p.39
* 객체 리터럴 개선 : 구조 분해의 반대, [참고](https://joshua1988.github.io/es6-online-book/enhanced-object-literals.html)


## 배열

* length 속성은 최대 인덱스 + 1인 값. 중간에 비어 있을수도... 와..몰랐다.
  * `var a = ['dog', 'cat', 'hen']; a[100] = 'fox'; a.length; // 101` // WTH
* forEach : 람다. `['dog', 'cat', 'hen'].forEach(function(currentValue, index, array) { .. }`

## 함수

* return 없으면 undefined가 반환됨.
* param을 전달하지 않으면 해당 param은 undefined가 됨.
* 모든 param은 arguments 배열로 접근할 수 있다.
* ES6는 default param 지원
* vargargs : [나머지 매개변수 문법](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/rest_parameters), `function avg(...args) { .. }`
  * 마지막 param으로만 사용할 수 있다.
* apply, call 메서드 : 오랜만이네..
* [전개 연산자, 스프레드 연산자](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Spread_syntax) : iterable한 타입이면 나머지 매개변수 문법에서 매핑되어 들어갈 수 있다.
  * 두 배열 합치기 : `[...arr1, ...arr2]`
  * 첫 번째 원소만 따로 : `const [first] = peaks;`

### 익명함수

* 함수 표현식 : `const someFunc = function() { .. }; someFunc();`
  * const 없어도 됨. 재정의 막으려고 하는건가?
* 함수 선언은 [호이스팅](https://developer.mozilla.org/ko/docs/Glossary/Hoisting)되지만 함수 표현식은 그렇지 않다. 표현식으로 정의한 함수는 꼭 호출 전에 선언해야 한다. 
* [즉시 실행 함수 표현식(IIFE, Immediately Invoked Function Expressions)](https://developer.mozilla.org/ko/docs/Glossary/IIFE) : 선언과 함께 호출하기.

### 화살표 함수

* function 키워드 없이 함수 정의
* 최종 표현식의 값을 return 한다.
* `const add = (a, b) => a + b;`
* 객체 리턴 : `const getUser = () => ({ id: 1, name: 'John' });`, {} 만 쓰면 에러남 괄호로 둘러쌓야.
* 일반 함수와 화살표 함수는 this의 바인딩 방법이 다르다.(LR p.36)

### 내장함수

* 함수 안의 함수
```js
function parentFunc() {
  var a = 1;

  function nestedFunc() {
    var b = 4; // parentFunc은 사용할 수 없는 변수
    return a + b;
  }
  return nestedFunc(); // 5
}
```
* 전역 함수를 늘리지 않는 방법

## 컴파일

* 호환성이 더 높은 코드로 변환하는 것.
* 컴파일 : [babel](https://babeljs.io/)
* 빌드 도구들에 의해 자동으로 처리 : [webpack](https://webpack.js.org/), [parcel](https://parceljs.org/), [rollup](https://rollupjs.org/)

## 비동기

### promise와 fetch

* promise : 비동기적인 동작을 수행하는 객체.
  * 대기중인 프라미스는 데이터가 도착하기 전의 상태를 표현
  * then : callback 함수를 인수로 받고 프라미스가 성공하면 콜백이 한 번만 호출됨.
  * callback 함수가 반환하는 값은 그 다음 then 함수의 callback에 전달되는 인자가 됨. 연쇄적으로 호출할 수 있다.
    * 이렇게 `fetch("https://api.randomuser.me/?nat=US&results=1").then(res => res.json()).then(json => json.results).then(console.log).catch(console.error);`
* promise 만들기

```js
new Promise((resolve, reject) => {
  // 코드
});
```

* promise 사용은 then 으로 연쇄시켜서 처리한다.

### async/await

* promise에 비해 기존의 동기적인 방식의 코드와 비슷함.
* 함수 앞에 `async` 키워드를 붙여줌 -> 함수를 비동기 함수로 만들어준다.
* promise 호출 앞에 await 키워드를 붙이면 프라미스가 완료될 때 까지 기다렸다가 함수가 진행된다.(then과 동일하다)


## ES6 모듈

* namespace 기능
* export 키워드
  * 다른 모듈에서 활용할 수 있도록 이름을 외부에 제공
  * export default : 하나의 이름만 노출하는 모듈
* import  : 가져오기
  * 구조분해 할당 : `import { name, another } from 'module';`
  * as 로 이름 바꾸기
  * \* 로 모두 가져오기

### CommonJS

* Node.js 에서 지원하는 일반적인 모듈 패턴
* module.exports 로 노출시키고 require로 가져온다