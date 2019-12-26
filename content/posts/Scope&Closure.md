---
title: 'Scope and Closure of Javascript'
date: '2019.12.26'
template: 'post'
draft: false
slug: '/posts/scope_and_closure_of_javascript/'
category: 'Javascript'
tags:
  - 'Javascript'
  - 'Scope'
  - 'Closure'
description: 'About Scope and Closure'
socialImage: ''
---

## Scope?

스코프란 말 그대로 기준 위치에서 접근할 수 있는 변수들의 범위를 말한다.

## 전역 스코프

만약 변수가 어떠한 함수 안에도 있지 않고, `{}` 안에도 있지 않을 경우 전역 스코프에 정의된다.
전역 스코프라는 말 그대로 모든 곳에서 사용 가능한 변수가 된다.

```js
const greet = "Hello, Luke"

function sayHello() {
  console.log(greet);
};

console.log(greet); // "Hello, Luke"
sayHello(); // "Hello, Luke"

모든 곳에서 사용이 가능함으로 함수 내에서도 당연히 사용 가능하다.
```

## 지역 스코프

1. 함수 스코프
   만약 변수가 함수 내부에서 선언되어진다면 그 변수는 해당 함수 내에서만 사용할 수 있다.

```js
function sayHello() {
  const greet = "Hello, Luke";
  console.log(greet);
};

console.log(greet) // "Reference Error!"
sayHello() // "Hello, Luke";

greet이라는 변수는 sayHello라는 함수 안에서 선언되었기 때문에 해당 함수의 밖에서는 참조할 수 없다.
```

2. 블록 스코프
   블록 스코프는 {} 내부에서 "`const` 혹은 `let`을 사용해 변수를 선언할 경우(`var`은 제외) 그 변수는 중괄호의 블록 내부에서만 사용이 가능하다.

```js
{
  const greet = "Hello, Luke"
  console.log(greet) // "Hello, Luke"
}

console.log(greet); // "Reference Error!"

{} 내부에서 선언되어진 greet를 {}의 밖에서는 참조할 수 없다.
```

## Scope Chain

```js
const value = 'value1';

function printValue() {
  return value;
}

function printFunc(func) {
  const value = 'value2';
  console.log(func());
}

printFunc(printValue);
```

위의 함수를 처음 봤을 때 조금 헷갈렸다. `printFunc(printValue)`를 호출할 때, `printFunc` 내부에서 `value`를 정의했기 때문에 결과값으로 `"value2"`가 나올 것이라 생각했다.

하지만 각 함수 객체가 처음 생성될 때의 실행 컨텍스트가 무엇인지를 생각해야 정확한 결과값을 알 수 있다. `printValue` 라는 함수 객체가 처음 생성될 때, 전역 객체의 `value`를 참조한다. 따라서 해당 함수가 실행될 때(실행 컨텍스트 상에서), 스코프 체이닝이 발생한다.

## Closure

클로저는 독립적인 변수를 가리키는 함수이다. 또는, 클로저 안에 정의된 함수는 만들어진 환경을 기억한다._(ft. MDN)_

### 은닉화

`Prototype`을 사용하면 객체를 다양한 방법으로 다룰 수 있다. 하지만 이때 Private Variable에 대한 접근 권한이라는 문제가 발생할 여지가 있다.

```js
function hello(name) {
  const _name = name;
  return function() {
    console.log('hello' + _name);
  };
}
```

위와 같은 방식이라면 외부에서 `_name`에 접근할 수 있는 방법은 없기 때문에 Closure의 특성을 이용해서 은닉화도 쉽게 구현할 수 있다.

### 반복문

```js
for (let i = 0; i < 10; i++) {
  setTimeout(function() {
    console.log(i);
  }, 100);
}
```

위의 코드를 실행시킨다면 무슨 결과가 나오게 될까?

정답은 `0 ~ 9` 까지의 정수가 아닌 10개의 `10`이다.
setTimeout의 콜백 함수는 비동기로 수행된다. 따라서 for-loop이 모두 끝나고난 뒤 10이 되어버린 `i`를 10번 출력하게 되는 것이다.

이 경우에도 클로저를 활용하면 `0 ~ 9`까지의 정수를 출력시킬 수 있다.

```js
for (let i = 0; i < 10; i++) {
  (function(j) {
    setTimeout(function() {
      console.log(j);
    }, 100);
  })(i);
}
```

위와 같은 방식으로 즉시 실행 함수(IIFE)를 이용해서 setTimeout의 콜백 함수를 가두고, 인자로 `j`를 넘겨주게 되면 for-loop이 한번 실행될 때마다 IIFE를 실행하게 되면서 안의 콜백 함수에 인자로 `i`를 넘겨줄 수 있게 된다.
