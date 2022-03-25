# 논리 연산자

- 논리 연산자의 종류 : OR(`||`), AND(`&&`), NOT(`!`) 

- 논리 연산자는 피연산자로 모든 자료형의 값을 받을 수 있고 연산 결과 역시 모든 타입이 될 수 있다.

## OR (||)

- `operand1 || operand2`

- 피연산자가 둘 다 `false`가 아닌 이상 결과는 `true`

- 피연산자가 불린형이 아닐 경우 불린형으로 변환하여 평가

### if문과 OR 연산자

```javascript
if (hour < 10 || hour > 18) {
  alert('영업시간이 아닙니다');
}
```

### 첫 번째 truthy를 찾는 OR 연산자

- 자바스크립트에서 제공하는 OR 연산자의 추가 기능

- OR 연산자와 피연산자가 여러 개인 경우 :

  1. 가장 왼쪽 피연산자부터 차례로 피연산자를 평가

  2. 각 피연산자를 불린형으로 변환하여 그 값이 `true`이면 연산을 멈추고 해당 피연산자의 변환 전 값을 반환

  3. 피연산자가 모두 `false`로 평가되는 경우에는 마지막 피연산자를 반환

#### 변수 또는 표현식으로 구성된 목록에서 첫 번째 truthy 얻기

```javascript
let name = '';
let nickname = '';

alert(name || nickname || '익명'); // 익명
// name이 없는 경우 nickname이, nickname도 없는 경우 '익명'이 표시됨
```

#### 단락 평가 (Short Circuit Evaluation)

- 단락 평가 : `truthy` 값을 만나면 그 이후로는 평가하지 않는 OR 연산자의 특징을 이용하여 첫 번째 값의 결과가 확실할 때 두 번째 값은 평가하자 않는 방법

  - 단락 평가는 연산자 왼쪽 조건이 `falsy`일 때만 명령어를 실행하고자 할 때 자주 쓰인다.

```javascript
let printMessage = '';
printMessage || alert('no message to print');
// printMessage가 falsy인 빈문자열이기 때문에 alert가 실행된다
```

## AND (&&)

- `operand1 || operand2`

- 피연산자가 둘 다 `true`일 때만 `true`를 반환하며 그 외의 경우는 `false`를 반환

- 피연산자가 불린형이 아닐 경우 불린형으로 변환하여 평가

### if문과 AND 연산자

```javascript
if (hour >= 10 && hour <= 18) {
  alert('영업시간입니다');
}
```

### 첫 번째 falsy를 찾는 AND 연산자

- OR 연산자와 반대로 AND 연산자와 피연산자가 여러 개인 경우 첫 번째 falsy를 반환한다. 피연산자에 falsy가 없다면 마지막 값을 반환한다.

- AND 연산자가 OR 연산자보다 우선순위가 높다. 즉, `a || b && c`는 `a || (b && c)`와 동일하게 동작한다.

- if를 짧게 줄이기 위한 용도로 AND 연산자나 OR 연산자를 사용하지 말아야 한다. 조건문이 필요할 때는 if문을 사용하는 것이 코드에서 무엇을 구현하고자 하는지 더 명백하게 보여줄 수 있습니다.

```javascript
// (1)
(x > 0) && alert('x는 0보다 크다');

// (2)
if (x > 0) alert('x는 0보다 크다');

// (1)과 (2)의 실행 결과는 같지만 이 경우 if문을 사용하는 것이 적절하다
```

## NOT (!)

- `!operand`

- NOT 연산자는 하나의 인수만 받고 다음 순서로 연산을 수행한다 :

  1. 피연산자를 불린형으로 변환

  2. 1에서 변환된 값의 역을 반환

- `!true === false`

- NOT을 연달아 두 개 사용하면 값을 불린형으로 형변환할 수 있다.

  - `!!'not an empty string' === Boolean('not an empty string')`

- NOT 연산자의 우선순위는 모든 논리 연산자 중에서 가장 높다.