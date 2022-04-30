# Modern Javascript

[MDN의 JavaScript 재입문하기](https://developer.mozilla.org/ko/docs/web/javascript/a_re-introduction_to_javascript)와 [러닝 리액트]() 책 중 JavaScript 부분 정리
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
* false로 평가 = false, 0, 빈 문자열, NaN, null, undefined. falsy, truthy


## 제어

* == 으로 비교하지 말자(타입 강제 변환이 일어남). 값을 비교하려면 삼중 등호 연산자로(===, !==)
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

## 배열

* length 속성은 최대 인덱스 + 1인 값. 중간에 비어 있을수도... 와..몰랐다.
  * `var a = ['dog', 'cat', 'hen']; a[100] = 'fox'; a.length; // 101` // WTH
* forEach : 람다. `['dog', 'cat', 'hen'].forEach(function(currentValue, index, array) { .. }`

## 함수

* return 없으면 undefined가 반환됨.
* param을 전달하지 않으면 해당 param은 undefined가 됨.
* 모든 param은 arguments 배열로 접근할 수 있다.
* vargargs : [나머지 매개변수 문법](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/rest_parameters), `function avg(...args) { .. }`
  * 마지막 param으로만 사용할 수 있다.
* apply, call 메서드 : 오랜만이네..
* [전개 연산자](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Spread_syntax) : iterable한 타입이면 나머지 매개변수 문법에서 매핑되어 들어갈 수 있다.

### 익명함수

* [즉시 실행 함수 표현식(IIFE, Immediately Invoked Function Expressions)](https://developer.mozilla.org/ko/docs/Glossary/IIFE) : 선언과 함께 호출하기.

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

