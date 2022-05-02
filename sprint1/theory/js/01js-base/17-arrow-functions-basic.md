# 화살표 함수 기본

<https://ko.javascript.info/arrow-functions-basics>

화살표 함수라는 이름은 문법의 생김새를 차용해 지어졌습니다.

```js
let func = (arg1, arg2, ...argN) => expression
```

아래 함수의 축약 버전이라고 할 수 있죠.

```js
let func = function(arg1, arg2, ...argN) {
  return expression;
};
```

```js
let sum = (a, b) => a + b;

/* 위 화살표 함수는 아래 함수의 축약 버전입니다.

let sum = function(a, b) {
  return a + b;
};
*/

alert( sum(1, 2) ); // 3
```

보시는 바와 같이 (a, b) => a + b는 인수 a와 b를 받는 함수입니다. (a, b) => a + b는 실행되는 순간 표현식 a + b를 평가하고 그 결과를 반환합니다.

* 인수가 하나밖에 없다면 인수를 감싸는 괄호를 생략할 수 있습니다. 괄호를 생략하면 코드 길이를 더 줄일 수 있습니다.

```js
let double = n => n * 2;
// let double = function(n) { return n * 2 }과 거의 동일합니다.

alert( double(3) ); // 6
```

* 인수가 하나도 없을 땐 괄호를 비워놓으면 됩니다. 다만, 이 때 괄호는 생략할 수 없습니다.

```js
let double = n => n * 2;
// let double = function(n) { return n * 2 }과 거의 동일합니다.

alert( double(3) ); // 6
```

아래 예시와 같이 함수를 동적으로 만들 수 있습니다.

```js
let age = prompt("나이를 알려주세요.", 18);

let welcome = (age < 18) ?
  () => alert('안녕') :
  () => alert("안녕하세요!");

welcome();
```

## 본문이 여러 줄인 화살표 함수

그런데 평가해야 할 표현식이나 구문이 여러 개인 함수가 있을 수도 있습니다. 이 경우 역시 화살표 함수 문법을 사용해 함수를 만들 수 있습니다. 다만, 이때는 중괄호 안에 평가해야 할 코드를 넣어주어야 합니다. 그리고 return 지시자를 사용해 명시적으로 결괏값을 반환해 주어야 합니다.

```js
let sum = (a, b) => {  // 중괄호는 본문 여러 줄로 구성되어 있음을 알려줍니다.
  let result = a + b;
  return result; // 중괄호를 사용했다면, return 지시자로 결괏값을 반환해주어야 합니다.
};

alert( sum(1, 2) ); // 3
```

## 요약

화살표 함수는 본문이 한 줄인 함수를 작성할 때 유용합니다. 본문이 한 줄이 아니라면 다른 방법으로 화살표 함수를 작성해야 합니다.

* 중괄호 없이 작성: `(...args) => expression` – 화살표 오른쪽에 표현식을 둡니다. 함수는 이 표현식을 평가하고, 평가 결과를 반환합니다.
* 중괄호와 함께 작성: `(...args) => { body }` – 본문이 여러 줄로 구성되었다면 중괄호를 사용해야 합니다. 다만, 이 경우는 반드시 `return` 지시자를 사용해 반환 값을 명기해 주어야 합니다.
