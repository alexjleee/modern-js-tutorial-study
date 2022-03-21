# 형 변환

## 원시형의 형 변환

- 형 변환(type conversion): 함수와 연산자에 전달되는 값이 적절한 자료형으로 자동 변환되는 것

  - 예: `alert` 함수가 전달받은 값을 자동으로 문자열로 변환하여 보여주는 것이나 수학 연산자가 전달받은 값을 숫자로 변환하는 경우

  - 전달받은 값을 의도적으로 원하는 타입으로 명시적으로 변환해 주는 경우도 형 변환

## 문자형으로 변환

- 문자형의 값이 필요할 때 일어난다.

- 예를 들어 `alert` 함수는 매개변수로 문자형을 받기 때문에 다른 형의 값을 전달받으면 자동으로 문자형으로 변환된다.

- `String` 함수를 호출해 전달받은 값을 명시적으로 문자열로 변환할 수 있다.

```javascript
let boolValue = true;
console.log(typeof boolValue); // 'boolean'
let stringValue = String(boolValue);
console.log(stringValue); // 'true'
console.log(typeof stringValue); // 'string'
```

## 숫자형으로 변환

- 수학과 관련딘 함수와 표현식에서 자동으로 일어난다.

- 예를 들어 `'6' / '2'` 처럼 숫자가 아닌 값에 나누기를 적용한 경우 문자열이 숫자형으로 자동 변환된 후 연산이 수행된다. 위 연산의 결과는 `6 / 2`와 같다.

- `Number` 함수를 호출해 전달받은 값을 명시적으로 숫자형으로 변환할 수 있다.

```javascript
let stringValue = '123';
console.log(typeof stringValue); // 'string'
let numberValue = Number(stringValue);
console.log(numberValue); // 123
console.log(typeof numberValue); // 'number'
```

- 단, 숫자 외 글자가 들어간 문자열을 숫자형으로 변환하려고 하면 그 결과는 `NaN`이 된다.

  - 문자열의 앞뒤 공백을 제거한 후 남은 문자열이 없다면 `0`, 문자열에서 숫자를 읽을 수 있다면 숫자형으로 변환, 실패하면 `NaN`이 된다.

```javascript
let price = Number('1500원');
console.log(price); // NaN
```

- 숫자형 변환 규칙

  - `undefined` => `NaN`

  - `null` => `0`

  - `true`/`false` => `1`/`0`

## 불린형으로 변환

- 논리 연산을 수행할 때 발생한다.

- `Boolean` 함수를 호출해 전달받은 값을 명시적으로 불린형으로 변환할 수 있다.

- 불린형 변환 규칙

  - `0`, `''`, `null`, `undefined`, `NaN` => `false`
  - 그 외의 값은 `true`

```javascript
console.log(Boolean(0)); // false
console.log(Boolean('0')); // true <= 비어있지 않은 문자열은 모두 true가 된다
```
