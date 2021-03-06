# 비교 연산자

## 비교 연산자

- 미만 `... < ...` / 초과 `... > ...`

- 이하 `... <= ...` / 이상 `... >= ...`

- 동등 `... == ...` / 부등 `... != ...`

- 일치 `... === ...` / 불일치 `... !== ...`

## 불린형 반환

- 비교 연산자는 불린형을 반환하며 반환된 값은 변수에 할당할 수 있다.

## 문자열 비교

- 문자열간에는 사전순(정확히는 유니코드순)으로 비교하며 사전상 뒤에 오는 문자열은 앞에 오는 문자열보다 크다고 판단된다. (예: `'a' < 'b'`)

  - 두 문자열의 첫 글자부터 비교하여 글자가 같으면 그다음 글자를 비교하고, 다르면 해당 글자가 더 큰 값을 가진 문자열이 더 크다고 판단한다. (예: `'appear' < 'apply'`)

  - 글자 간 비교가 끝날 때까지 반복하며 비교가 종료되었을 때 두 문자열의 길이가 같다면 두 문자열은 동일하다고 판단하고, 다르면 둘 중 길이가 더 긴 문자열이 더 크다고 판단한다. (예: `'bee' > 'be'`)

  - 같은 글자일 경우 소문자가 대문자보다 크다. (예: `'a' > 'A'`)

## 다른 형을 가진 값 간의 비교

- 비교하려는 값의 자료형이 다르면 숫자형으로 바꾸어 비교한다.

  - 문자열의 경우 숫자와 비교될 때 빈 문자열이면 `0`으로, 숫자가 아닌 글자가 포함된 문자열이면 `NaN`로, 숫자만 포함된 문자열일 경우 해당 숫자로 변환한 후 비교한다. (예: `'01' < 2`)

  - 비교하려는 값이 둘 다 문자열일 경우 숫자로만 이루어져 있더라도 변환하지 않는다. (예: `'2' > '12'`)

  - 불린형의 경우 `true`는 `1`, `false`는 `0`으로 변환된 후 비교한다.

## 일치 연산자

- 동등 연산자(`==`)는 형이 다른 피연산자를 비교할 때 이를 숫자형으로 바꾼다. `''`와 `false`는 숫자형으로 변환하면 `0`이 되기 때문에 `0 == false`, `'' === false`가 성립하게 된다.

- 일치 연산자(`===`)는 자료형의 동등 여부까지 검사하기 때문에 보다 명확하게 비교할 수 있다.

## null이나 undefined와 비교

- 일치 연산자를 사용하면 두 값의 자료형이 다르기 때문에 `false`가 반환된다. (`null !== undefined`)

- 동등 연산자를 사용하면 두 값이 동등하다고 판단하여 `true`를 반환한다. (`null == undefined`)

- 산술 연산자나 기타 비교 연산자(`<`, `>`, `<=`, `>=`)를 사용하여 둘을 비교하면 각각 숫자형으로 변환되어 `null`은 `0`, `undefined`는 `NaN`이 된다.

### null vs 0

```javascript
null == 0; // false -> 동등 연산자
null >= 0; // true -> 기타 비교 연산자: null이 0으로 변환됨
null > 0; // false -> 기타 비교 연산자: null이 0으로 변환됨
```

- 동등 연산자(`==`)와 기타 비교 연산자(`<`, `>`, `<=`, `>=`)는 동작 방식이 다르다.
  - 동등 연산자의 경우 피연산자가 `undefined` 또는 `null`일 때 형 변환을 하지 않는다.
  - 기타 비교 연산자의 경우 피연산자 `null`을 숫자형인 `0`으로 변환하여 비교한다.

### undefined

- `undefined`는 다른 값과 비교해서는 안 된다.

```javascript
undefined > 0; // false -> undefined는 NaN으로 변환됨
undefined < 0; // false -> undefined는 NaN으로 변환됨
undefined == 0; // false -> undefined는 undefined나 null 외의 값과는 동등하지 않음
```

### 함정 피하기

- 일치 연산자(`===`) 외의 비교 연산자의 피연산자에 `null`이나 `undefined`가 오지 않도록 주의한다.

  - `null`이나 `undefined`가 될 가능성이 있는 변수가 기타 비교 연산자(`<`, `>`, `<=`, `>=`)의 피연산자가 될 경우 이를 따로 처리하는 코드를 추가한다.
