# switch문

- 복수의 `if` 조건문은 `switch`문으로 바꿀 수 있다.

- `if...else`문은 논리적 참/거짓으로 실행할 코드 블록을 결정하고, `switch`문은 표현식을 평가한 다양한 값에 따라 실행할 코드 블록을 결정한다.

## 문법

```javascript
switch(x) {
  case value1:
    // x가 value1과 일치할 때 실행될 구문
    [break]; // break는 선택사항
  case value2:
    // x가 value2와 일치할 때 실행될 구문
    [break];
  default:
    // x와 일치하는 case가 없을 때 실행될 구문
    [break];
}
```

- 위에서부터 차례대로 주어진 변수 `x`를 각 `case`문의 값과 비교하여 일치할 경우 해당 `case`문 아래의 코드를 실행한다.

- `break`문을 만나면 코드 실행을 멈춘다.

- 변수 `x`와 일치하는 `case`문의 값이 없다면, (`default`문이 있을 경우 `default`문 아래의 코드가 실행된다.

- `switch`문과 `case`문은 모든 형태의 표현식을 인수로 받는다.

## 예시

```javascript
let day = 5;

switch (day) {
  case 0:
    alert('Today is Sunday');
    break;
  case 1:
    alert('Today is Monday');
    break;
  case 2:
    alert('Today is Tuesday');
    break;
  case 3:
    alert('Today is Wednesday');
    break;
  case 4:
    alert('Today is Thursday');
    break;
  case 5:
    alert('Today is Friday'); // 실행됨
    break;
  case 6:
    alert('Today is Saturday');
    break;
  default:
    alert('Invalid day');
}
```

- 만약 위의 예제에서 `break`문이 없으면 폴스루(fall through)가 되어 `case 5`가 실행된 후 `switch`문을 탈출하지 않고 연이어 그 아래 코드가 실행되며 `'Today is Friday'`, `'Today is Saturday'`, `'Invalid day'`가 차례로 뜨게 된다.

## 여러 개의 case문 묶기

- 폴스루를 활용해 여러 개의 `case`문을 한데 묶을 수 있다.

```javascript
let month = 3;
let days = 0;

switch (month) {
  case 1: case 3: case 5: case 7: case 8: case 10: case 12:
    days = 31;
    break;
  case 4: case 6: case 9: case 11:
    days = 30;
    break;
  case 2:
    days =28;
    break;
  default:
    days = -1;
}

if (days === -1) {
  alert('Invalid month');
} else {
  alert(`This month has ${days} days.`);
}
```

## 자료형의 중요성

- `switch`문은 일치 비교(`===`)로 조건을 확인하기 때문에 비교하려는 값과 `case`문의 값이 형과 값이 같아야 `case`문이 실행된다.

```javascript
let input = prompt('Enter number between 1 ~ 3');

switch (input) {
  case 1: // => case '1':
    alert('You entered 1');
    break;
  case 2: // => case '2':
    alert('You entered 2');
    break;
  case 3: // => case '3':
    alert('You entered 3');
    break;
  default:
    alert('Wront input');
}
```

- 위의 예시에서 아무리 1 ~ 3 사이의 숫자를 입력해도 `default`문이 실행된다. `prompt`로 받은 값의 자료형은 문자열이기 때문이다. 주석처럼 `case`문의 값을 문자열로 바꿔 주어야 의도대로 실행된다.