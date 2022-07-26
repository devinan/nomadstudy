# 에러 코드를 읽고 문제 해결방법

에러의 종류

- **syntax error**
- **logic error**

## Syntax ERROR 란?


아래의 예제는 자주 보이는 에러를 위주로 작성했습니다.

- SyntaxError: "x" is a reserved identifier

```js
// 예약어를 nameing 하는것은 좋지 않습니다. 특히 enum 예약어는 엄격모드를 하지 않아도 에러를 냅니다.
const enum = "nico";
// SyntaxError: enum is a reserved identifier
```

---
- SyntaxError: Unexpected '#' used outside of class body
> 주로 dom을 다룰때 많이 나타는 에러입니다.

```js
document.querySelector(.clock-title);
// Uncaught SyntaxError: Unexpected token '.'

```

```js
document.querySelector(clock-title);
// Uncaught ReferenceError: clock is not defined
```

```js
document.querySelector(#clock-title);
// Uncaught SyntaxError: Private field '#clock' must be declared in an enclosing class (at index.js:1:23)
```

``` js
class classWithHi {
    #privateField
  
    constructor() {
    }
  }

  this.#privateField = "hello";

// Uncaught SyntaxError: Private field '#privateField' must be declared in an enclosing class (at index.js:8:7)

// ! fix it
class classWithHi {
    #privateField
  
    constructor() {
        this.#privateField = "hello";
    }
  }


```

---

- SyntaxError: Unexpected token
>  syntaxError: expected A , got "x" 주로 x 부분을 찾아보시면 압니다.
``` js

for (let i = 0; i < 5,; ++i) {
  console.log(i);
}

Uncaught SyntaxError: Unexpected token ';' (at index.js:1:23)

```
---

- SyntaxError: function statement requires a name
> function statement vs function expression
```js
function () {
    return 'Hello world';
  }
// SyntaxError: function statement requires a name
```

---

-  SyntaxError: missing X after Y


- SyntaxError: return not in function

```js
const greeting = function (lang) {
  if (lang === "ko")
    return '안녕하세요';
  };
  if (lang === "en") {
    return 'hi';
  }
}
// Uncaught SyntaxError: Illegal return statement (at index.js:6:5)
// return not in function
// Declartion or statement expected.

```

## TypeError: "x" is (not) "y"

- typeError: x is not function
  - A typo in the function name
  - Function called on the wrong object


## ReferenceError

- ReferenceError: "x" is not defined
>  어느 곳에서 존재하지 않은 변수를 호출할때 일어납니다. 그리고 잘못된 스코프를 사용했을때 일어납니다.

``` js
const hours = "2";

minutes.padStart(2, "0");
// Uncaught ReferenceError: minutes is not defined
```

``` js
function add () {
  const num1 = 3, num2 = 5;
  return num1 + num2;
}

console.log(num1);

// Uncaught ReferenceError: num1 is not defined
```

- ReferenceError: assignment to undeclared variable "x"

``` js
function hello() {
  greeting = "hi";
  console.log(greeting);
}

hello();
// 실행하시면 error가 일어나지 않습니다. 하지만 이러한 함수를 작성하는 것은 잘못된 표현입니다.
// 왜냐하면 greeting = "hi"가 마치 전역변수가 greeting이 있는 것 처럼 보입니다.
// 그래서 hello();를 호출 하기전에  console.log(greeting)을 하면 에러가 나옵니다.
```


## Logic ERROR 란?

logic error는 에러메세지가 일어나지 않으며(break 현상이 없습니다.) 프로그램은 정상적으로 작동됩니다.
다만, 프로그래머가 입력한 결과와 달리 의도치 않은 부수효과를 일으킵니다.
이 에러는 보통 비동기적 상황에서 일어나므로 쉽게 찾을 수 없습니다.
