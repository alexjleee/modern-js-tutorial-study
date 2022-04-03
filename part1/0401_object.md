# 객체

## 객체란?

- 객체는 키(key)와 값(value)으로 구성된 프로퍼티(property)들의 집합이다.

  - 키에는 문자형/심볼, 값에는 모든 자료형이 허용된다.

  - `key: value`

  - 키는 프로퍼티 이름 또는 식별자라고도 불린다.

  - 프로퍼티의 값이 함수일 경우 일반 함수와 구분하기 위해 메서드(method)라고 부른다.

- 자바스크립트는 객체 기반의 프로그래밍 언어이며 원시 자료형을 제외한 자바스크립트를 구성하는 거의 모든 것(함수, 배열, 정규표현식 등)이 객체이다.

- 원시형과 달리 객체형은 다양한 데이터를 담을 수 있다. 또, 원시형은 값을 변경할 수 없지만(immutable) 객체형은 값을 변경할 수 있다(mutable).

  - 객체는 `const`로 선언되어도 내부 프로퍼티는 수정될 수 있다. 

## 객체 리터럴

- 자바스크립트가 지원하는 다양한 객체 생성 방법 중 객체 리터럴(object literal)이 주로 사용된다.

- 객체 리터럴은 중괄호(`{...}`)를 사용해 객체를 선언한다. 중괄호 안에 0개 이상의 프로퍼티를 정의하며 만약 중괄호 내에 프로퍼티를 정의하지 않으면 빈 객체가 생성된다.

```javascript
const user = {
  name: 'Alex', //키: 'name', 값: 'Alex'
  age: 30 // 키: 'age', 값: 30,
};
```

## 프로퍼티

- 객체는 프로퍼티의 집합이며 프로퍼티는 `key: value` 형태다.

- 프로퍼티를 나열할 때는 쉼표(`,`)로 구분한다.

  - 마지막 프로퍼티 끝에 붙는 쉼표는 trailing/hanging comma라고 부르며 생략 가능하다. 마지막 프로퍼티 끝에 쉼표를 붙이면 후에 프로퍼티를 추가/삭제/이동하기 쉬워진다.

### 프로퍼티 이름

- 변수 이름과 달리 객체 프로퍼티에는 예약어도 사용할 수 있다. 

- 프로퍼티 이름은 식별자 이름 규칙을 따르지 않을 수도 있으나 이 경우 반드시 이름을 따옴표로 묵어야 한다. (예: `firstName`의 경우 그냥 사용할 수 있지만 `'first-name'`, `'first name'`의 경우 반드시 따옴표로 묶어야 한다.)

- 프로퍼티 이름에는 문자형, 심볼형이 사용될 수 있다. 그 외의 값은 문자형으로 자동 변환된다. (예를 들어 숫자 `0`을 키로 사용하면 자동으로 문자열 `'0'`으로 변환된다.)

### 프로퍼티 접근

- 대괄호 표기법(bracket notation): 대괄호 표기법으로 프로퍼티에 접근할 때는 반드시 문자열을 따옴표로 묶어 주어야 한다. 대괄호 표기법을 사용하면 문자열뿐 아니라 모든 표현식의 평가 결과를 프로퍼티로 사용할 수 있다. => 다양한 경우에 사용 가능!

- 마침표 표기법(dot notation): 프로퍼티 이름이 식별자 이름 규칙을 따를 경우에만 마침표 표기법으로 프로퍼티에 접근할 수 있다. => 사용 범위에 제약이 있지만 단순!

```javascript
const user = {
  'first-name': 'Alex',
  age: 30
}
const key = 'first-name';

user.first-name; // error!
user[first-name]; // error!
user['first-name']; // 'Alex'

user.key; // error!
user[key]; // 'Alex'

user.age; // 30
user[age]; // error!
user['age']; // OK
```

#### 계산된 프로퍼티

- 계산된 프로퍼티(computed property): 객체 리터럴 안에서 대괄호로 묶인 프로퍼티 키

```javascript
let fruit = prompt('Which fruit do you want to buy?', '');

const cart = {
  [fruit]: 1, // 해당 프로퍼티의 이름은 변수 fruit의 값을 동적으로 받아온다
};
```

#### 단축 프로퍼티 (ES6)

- 프로퍼티 값을 기존 변수에서 받아와 사용할 때, 프로퍼티 이름과 값이 변수의 이름과 같을 때 프로퍼티 값 단축 구문(property value shorthand)을 사용할 수 있다.

```javascript
function makeUser(name, age) {
  return {
    name, // name: name과 같음
    age, // age: age와 같음
    createdAt: new Date().toLocalString()
  }
}
```

### 프로퍼티 동적 생성

- 존재하지 않는 프로퍼티에 값을 할당하면 프로퍼티가 동적으로 생성된다.

```javascript
const user = {
  name: 'Alex',
  age: 30
}
user.nationality = 'Republic of Korea';
user; // {name: 'Alex', age: 30, nationality: 'Republic of Korea'}
```

### 프로퍼티 값 갱신

- 이미 존재하는 프로퍼티에 값을 할당하면 해당 프로퍼티 값이 갱신된다.

```javascript
const user = {
  name: 'Alex',
  age: 29
}
user.age = 30;
user; // {name: 'Alex', age: 30}
```

### 프로퍼티 삭제

- `delete` 연산자는 객체의 프로퍼티를 삭제한다. 존재하지 않는 프로퍼티를 삭제하려 할 경우 에러가 발생하지 않고 무시된다.

```javascript
const user = {
  name: 'Alex',
  age: 30
}

delete user.age; // true
user; // {name: 'Alex'}

delete user.nationality; // true
user; // {name: 'Alex'}
```

### in 연산자로 프로퍼티 존재 여부 확인

- 자바스크립트에서는 존재하지 않는 프로퍼티에 접근해도 에러가 발생하지 않고 `undefined`가 반환된다. 이를 이용하면 프로퍼티의 존재 여부를 쉽게 확인할 수 있다.

```javascript
const user = {
  name: 'Alex'
}
if (user.age === undefined) {
  alert('There is no age property');
} // user 객체 안에 age라는 프로퍼티는 없으므로 alert창이 뜨게 된다
```

- `in` 연산자를 사용하여 프로퍼티의 존재 여부를 확인할 수도 있다. 프로퍼티가 존재하는데 값이 `undefined`여서 위의 방법으로 확인이 불가능 할 때 정확한 판별을 위해 `in` 연산자를 사용할 수 있다.

```javascript
const user = {
  name: 'Alex',
  age: 30
}
if ('age' in user) {
  alert('There is age property');
} // user 객체 안에 age라는 프로퍼티가 존재하므로 alert창이 뜨게 된다
```

### for...in 반복문

- `for...in` 반복문을 사용하면 객체의 모든 키를 순회할 수 있다.

```javascript
const user = {
  name: 'Alex',
  age: 30,
  nationality: 'Republic of Korea'
}

for (let key in user) {
  alert(key + ' : ' + user[key]);
}
// 'name : Alex'
// 'age : 30'
// 'nationality : Republic of Korea'
```

### 객체의 프로퍼티 정렬 방식

- 정수 프로퍼티는 자동으로 정렬되며 그 외 프로퍼티는 객체에 추가된 순서대로 정렬된다. 

  - 정수 프로퍼티(integer property): 정수로 변환하였다 다시 문자열로 바꿨을 때 값이 변하지 않는 문자열 (예: `12`는 정수 프로퍼티지만 `$12`, `1.2` 등은 정수 프로퍼티가 아니다.) 