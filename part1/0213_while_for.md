# while과 for 반복문

## 반복문

- 반복문은 조건식의 결과가 참인 경우 반복하여 코드 블록을 실행하며 이는 조건식이 거짓일 때까지 반복된다.

## while 반복문

```javascript
while (condition) {
  // 반복문 본문: condition이 truthy일 때 실행되는 코드
}
```

- 반복문의 조건식은 평가 후 불린값으로 변경된다. 조건식 평가 결과가 거짓이 될 때까지 본문을 반복 실행한다.

- `while`문은 반복 횟수가 불명확할 때 주로 사용한다.

- `while`의 조건식에 `true`를 넣으면 무한 반복문이 된다.

## do...while 반복문

```javascript
do {
  // 반복문 본문
} while (condition);
```

- `while`문과 달리 본문이 먼저 실행된 후 조건을 확인한다.

- `do...while`문은 조건의 참 거짓 여부와 상관 없이 본문을 최소 한 번은 실행해야 할 때만 사용하며 그 외 대부분의 경우는 `while`문이 더 적합하다.

## for 반복문

```javascript
for (initialization; condition; step) {
  // 반복문 본문
}
```

- initialization: 식 또는 변수 선언. 반복문에 진입할 때 단 한 번 실행된다. 주로 카운터 변수를 초기화할 때 사용한다.

- condition: 매 반복마다 평가되는 조건식으로 결과가 참이면 본문을 실행하며 거짓이 되면 반복문을 멈춘다.

- step: 각 반복의 본문이 실행된 이후 실행된다.

### 인라인 변수 선언

- 카운터 변수를 반복문 안에서 `let`으로 선언하면 해당 변수는 반복문 안에서만 접근할 수 있다.

```javascript
for (let i = 0; i < 3; i++) {
  alert(i);
}
alert(i); // ReferenceError
```

```javascript
for (var i = 0; i < 3; i++) {
  alert(i);
}
alert(i); // 3
```

### 구성 요소 생략

- `for`문의 구성 요소는 필요에 따라 생략 가능하다.

```javascript
let i = 0;
for (; i < 3; i++) {
  alert(i);
}
// initialization이 필요하지 않으므로 생략
```

- 모든 구성 요소를 생략할 수도 있으나 이 경우 무한 반복문이 된다.

- `for`문의 구성 요소를 생략할 때 세미콜론(`;`) 두 개는 절대 생략해서는 안 된다. 하나라도 없으면 문법 에러가 발생한다.

## break

- 특별 지시자인 `break`를 사용하면 언제든 원하는 때에 반복문을 빠져나올 수 있다.

- 반복문의 시작/끝 지점에서 조건을 확인하는 것이 아니라 본문 가운데 또는 여러 곳에서 조건을 확인해야 하는 경우 무한 반복문과 함께 `break`를 사용하면 좋다.

```javascript
let sum = 0;

while (true) {
  // condition이 true이므로 무한 반복문이다
  // 계속해서 prompt로 value 값을 입력받아 sum에 더한다
  let value = +prompt('Enter a number', '');
  if (!value) break; // 단, value값이 입력되지 않을 경우 break하여 반복문을 빠져나온다
  sum += value;
}

alert('Sum: ' + sum);
```

## continue

- `continue`는 전체 반복문이 아닌 현재 진행 중인 이터레이션만 멈추고 다음 이터레이션을 실행한다.

```javascript
for (let i = 1; i < 10; i++) {
  if (i % 2 === 0) continue; // i가 짝수일 때는 이후 본문이 실행되지 않는다
  alert(i); // i가 홀수일 때만 실행됨
}
```

- 삼항 연산자와 함께 사용할 수 없다. 삼항 연산자는 표현식만 피연산자로 받기 때문이다. 따라서 `continue`나 `break`와 같은 지시자는 삼항 연산자에 사용할 수 없다.

## break/continue와 레이블

- 여러 개의 중첩 반복문을 한 번에 빠져나와야 할 경우, `break` 지시자만으로는 안쪽에 있는 반복문만 빠져나올 수 있다. 외부 반복문까지 한꺼번에 빠져 나와야 할 때, 레이블을 사용할 수 있다.

- 레이블(label)은 반복문 앞에 콜론과 함께 쓰이는 식별자다. 반복문 안에서 `break <labelName>`문을 사용하면 레이블에 해당하는 반복문을 빠져나갈 수 있다.

```javascript
outer:
for (let i = 0; i < 3; i++) {
  // inner
  for (let j = 0; j < 3; j++) {
    let input = prompt(`(${i}, ${j}의 값)`, '');
    if (!input) break outer;
    // 사용자가 값을 입력하지 않거나 Cancel 버튼을 누르면 inner와 outer반복문 모두를 빠져나온다
  }
}
```

- `continue` 지시자도 레이블과 함께 사용할 수 있으며 이 경우 레이블이 붙은 반복문의 다음 이터레이션을 실행한다.

- `break`와 `continue`는 반복문 안에서만 사용 가능하며 레이블은 반드시 `break`나 `continue` 지시자 위에 있어야 한다.