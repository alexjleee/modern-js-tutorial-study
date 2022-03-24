# if와 ?를 사용한 조건 처리

## if

```javascript
if (조건식1) {
  // 조건식1의 평가 결과가 true일 때 실행되는 코드 블록
} else if (조건식2) {
  // optional
  // 조건식1의 평가 결과가 false이고 조건식2의 평과 결과는 true일 때 실행되는 코드 블록
} else {
  // optional
  // 조건식1, 조건식2의 평가 결과가 모두 false일 때 실행되는 코드 블록
}
```

- `if`문을 쓸 때 조건이 참일 때 실행되는 구문이 짧더라도 가독성을 위해 중괄호(`{}`)로 감싸는 것을 권장한다.

- `falsy`값 : 불린형으로 변환 시 `false`가 되는 값.

  - `0`, `''`, `null`, `undefined`, `NaN`

- `truthy`값 : `falsy`값 외의 값. 불린형으로 변환시 `truthy`가 된다.

## 조건부 연산자 ?

```javascript
let result = condition ? value1 : value2;
// condition이 true면 value1이, false면 value2가 result에 할당된다
```

- 삼항(ternary) 연산자라고도 부른다

- 조건에 따라 다른 값을 변수에 할당해야 할 때, 조건부 연산자를 사용하면 `if...else`문보다 짧고 간결하게 표현할 수 있다.

```javascript
// if...else
let height = prompt('Enter your height in meter', '');
let weight = propmt('Enter your weight in kg', '');
let bmi = weight / (height * height);

let isNormalWeight;
if (bmi > 18.5 && bmi < 25) {
  isNormalWeight = true;
} else {
  isNormalWeight = false;
}
```

```javascript
// ?
let height = prompt('Enter your height in meter', '');
let weight = propmt('Enter your weight in kg', '');
let bmi = weight / (height * height);

let isNormalWeight = bmi > 18.5 && bmi < 25 ? true : false;
// cf. 조건에 따라 할당해야 할 값이 true/false라면 비교 연산 자체가 true/false를 반환하기 때문에 굳이 조건부 연산자를 사용하지 않아도 된다.
// let isNormalWeight = bmi > 18.5 && bmi < 25;
```

- 조건식을 괄호 안에 쓰지 않아도 상관없지만 가독성을 위해 사용할 것을 권장한다.

### 다중 ?

- 조건부 연산자를 여러 개 연결하여 복수의 조건을 처리할 수 있다.

```javascript
let bmi = prompt('Enter your BMI', '');
let category = (bmi <= 18.5) ? 'Underweight' : 
  (bmi < 25) ? 'Normal' : 
  (bmi < 30) ? 'Overweight' :
  'Obese';
```

```javascript
// 위의 예시를 if...else문으로 작성할 경우
let bmi = prompt('Enter your BMI', '');
let category;
if (bmi <= 18.5) {
  category = 'Underweight';
} else if (bmi < 25) {
  category = 'Normal';
} else if (bmi < 30) {
  category = 'Overweight';
} else {
  category = 'Obese';
}
```
### 부적절한 ?

- `?` 연산자를 사용하면 `if`문보다 짧게 작성할 수 있지만 모든 경우에 적절한 것은 아니다.

- 조건에 따라 반환 값을 달리해야 할 때는 `?` 연산자를, 분기를 만들어 처리해야 할 때는 `if`문을 사용하는 것이 적절하다.

```javascript
// 부적절한 ? 연산자 사용 예시
(bmi > 18.5 && bmi < 25) ? 
  alert('BMI가 정상체중 범위 안에 있습니다.') : alert('BMI가 정상체중 범위 밖에 있습니다.');
```