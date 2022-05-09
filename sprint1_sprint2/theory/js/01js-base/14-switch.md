# switch문

## 문법

```js
switch(x) {
  case 'value1':  // if (x === 'value1')
    ...
    [break]

  case 'value2':  // if (x === 'value2')
    ...
    [break]

  default:
    ...
    [break]
}
```

## 예시

```js
let a = 2 + 2;

switch (a) {
  case 3:
    alert( '비교하려는 값보다 작습니다.' );
    break;
  case 4:
    alert( '비교하려는 값과 일치합니다.' );
    break;
  case 5:
    alert( '비교하려는 값보다 큽니다.' );
    break;
  default:
    alert( "어떤 값인지 파악이 되지 않습니다." );
}
```

**case문 안에 break문이 없으면 조건에 부합하는지 여부를 따지지 않고 이어지는 case문을 실행합니다.**

```js
let a = 2 + 2;

switch (a) {
  case 3:
    alert( '비교하려는 값보다 작습니다.' );
  case 4:
    alert( '비교하려는 값과 일치합니다.' );
  case 5:
    alert( '비교하려는 값보다 큽니다.' );
  default:
    alert( "어떤 값인지 파악이 되지 않습니다." );
}
```

위 예시를 실행하면 아래 3개의 alert문이 실행됩니다.

```js
alert( '비교하려는 값과 일치합니다.' );
alert( '비교하려는 값보다 큽니다.' );
alert( "어떤 값인지 파악이 되지 않습니다." );
```

### `switch/case`문의 인수엔 어떤 표현식이든 올 수 있습니다.

`switch`문과 `case`문은 모든 형태의 표현식을 인수로 받습니다.

예시:

```js
let a = "1";
let b = 0;

switch (+a) {
  case b + 1:
    alert("표현식 +a는 1, 표현식 b+1는 1이므로 이 코드가 실행됩니다.");
    break;

  default:
    alert("이 코드는 실행되지 않습니다.");
}
```

executed code

```js
case b + 1:
  alert("표현식 +a는 1, 표현식 b+1는 1이므로 이 코드가 실행됩니다.");
  break;
```

표현식 +a를 평가하면 1이 됩니다. 이 값은 첫 번째 case문의 표현식 b + 1을 평가한 값(1)과 일치하죠. 따라서 첫 번째 case문 아래의 코드가 실행됩니다.

## 여러 개의 "case"문 묶기

```js
let a = 3;

switch (a) {
  case 4:
    alert('계산이 맞습니다!');
    break;

  case 3: // (*) 두 case문을 묶음
  case 5:
    alert('계산이 틀립니다!');
    alert("수학 수업을 다시 들어보는걸 권유 드립니다.");
    break;

  default:
    alert('계산 결과가 이상하네요.');
}
```

case 3과 case 5는 동일한 메시지를 보여줍니다.

switch/case문에서 break문이 없는 경우엔 조건에 상관없이 다음 case문이 실행되는 부작용이 발생합니다. 위 예시에서 case 3이 참인 경우엔 (*)로 표시한 줄 아래의 코드가 실행되는데, 그 아래 줄엔 case 5가 있고 break문도 없기 때문에 12번째 줄의 break문을 만날 때까지 코드는 계속 실행됩니다.

## 자료형의 중요성

switch문은 일치 비교로 조건을 확인합니다. 비교하려는 값과 case문의 값의 형과 값이 같아야 해당 case문이 실행됩니다.

```js
let arg = prompt("값을 입력해주세요.");
switch (arg) {
  case '0':
  case '1':
    alert( '0이나 1을 입력하셨습니다.' );
    break;

  case '2':
    alert( '2를 입력하셨습니다.' );
    break;

  case 3:
    alert( '이 코드는 절대 실행되지 않습니다!' );
    break;
  default:
    alert( '알 수 없는 값을 입력하셨습니다.' );
}
```

1. 0이나 1을 입력한 경우엔 첫 번째 alert문이 실행됩니다.
2. 2를 입력한 경우엔 두 번째 alert문이 실행됩니다.
3. 3을 입력하였더라도 세 번째 alert문은 실행되지 않습니다. 앞서 배운 바와 같이 prompt 함수는 사용자가 입력 필드에 기재한 값을 문자열로 변환해 반환하기 때문에 숫자 3을 입력하더라도 prompt 함수는 문자열 '3'을 반환합니다. 그런데 세 번째 case문에선 사용자가 입력한 값과 숫자형 3을 비교하므로, 형 자체가 다르기 때문에 case 3 아래의 코드는 절대 실행되지 않습니다. 대신 default문이 실행됩니다.

## 과제

### 1. switch to if

```js
switch (browser) {
  case 'Edge':
    alert( "Edge를 사용하고 계시네요!" );
    break;

  case 'Chrome':
  case 'Firefox':
  case 'Safari':
  case 'Opera':
    alert( '저희 서비스가 지원하는 브라우저를 사용하고 계시네요.' );
    break;

  default:
    alert( '현재 페이지가 괜찮아 보이길 바랍니다!' );
}
```

to

```js
if(browser == 'Edge') {
  alert("Edge를 사용하고 계시네요!");
} else if (browser == 'Chrome'
 || browser == 'Firefox'
 || browser == 'Safari'
 || browser == 'Opera') {
  alert( '저희 서비스가 지원하는 브라우저를 사용하고 계시네요.' );
} else {
  alert( '현재 페이지가 괜찮아 보이길 바랍니다!' );
}
```

### 2. "if"문을 "switch"문으로 변환하기

```js
let a = +prompt('a?', '');

if (a == 0) {
  alert( 0 );
}
if (a == 1) {
  alert( 1 );
}

if (a == 2 || a == 3) {
  alert( '2,3' );
}
```

to

```js
let a = +prompt('a?', '');

switch (a) {
  case 0:
    alert( 0 );
    break;

  case 1:
    alert( 1 );
    break;

  case 2:
  case 3:
    alert( '2,3' );
    break;
}
```