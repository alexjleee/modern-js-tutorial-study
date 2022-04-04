# 객체 복사

## 참조에 의한 객체 복사 (단순 복사)

- 원시값은 값 그대로 저장/복사되는 반면 객체는 참조에 의해 저장/복사된다.

- 객체의 경우 객체가 할당된 변수의 메모리 주소를 통해 메모리 공간에 접근하면 참조 값(reference value)에 접근하게 된다.

- 객체가 할당된 변수를 복사하면 객체가 복사되는 것이 아니라 참조 값이 복사된다.

- 원시값과 다르게 객체의 경우 여러 개의 식별자가 하나의 객체를 공유할 수 있다.

```javascript
let user = { name: 'Alex' };
let admin = user;
// user와 admin은 같은 객체를 참조
admin.name = 'Lewis';
user.name; // 'Lewis';
```

## 얕은 복사 (Shallow Copy) & 깊은 복사 (Deep Copy)

- 두 변수가 하나의 객체를 참고하는 것이 아닌 형태가 동일하지만 별개의 객체를 참조하게 하려면, 즉 객체의 복사본을 만들려면 얕은 복사를 하거나 깊은 복사를 해야 한다.

### 얕은 복사 (Shallow Copy)

- 한 단계만 복사. 객체에 중첩된 객체는 복사하지 못함.

```javascript
let user = {
  name: 'Alex',
  age: 30,
  nationality: 'South Korea'
}
```

#### for...in

```javascript
let clone = {}; // user의 프로퍼티를 복사할 빈 객체 생성

for (let key in user) {
  clone[key] = user[key];
} // 반복문으로 user의 프로퍼티를 순회하여 clone에 똑같은 프로퍼티를 만들어줌
```

#### Object.assign

```javascript
let clone = Object.assign({}, user); 
// Object.assign(dest, [src1, src2, ...]) :
// dest에 src1, src2, ...의 프로퍼티들을 복사한 후 dest 반환
```

#### 펼침 연산자(spread operator)

```javascript
let clone = {...user};
```

### 깊은 복사 (Deep Copy)

- 중첩 객체까지 복사하기 위해서는 객체의 각 프로퍼티 값을 검사하며 값이 객체일 경우 그 객체의 구조도 복사해주는 반복문을 사용해야 한다.

- 이전에는 자바스크립트에서 깊은 복사를 지원하지 않았고 `JSON.parse(JSON.stringify(obj))`로 깊은 복사를 하곤 했다. 이 패턴은 빠르지만 재귀 데이터 구조, 내장 함수(`Map`, `Set`, `Date`, `RegEs` 등), 함수의 경우 복사할 수 없었다.

- 2018년 `structuredClone()` 메소드가 추가되었다. 하지만 여전히 한계가 있다. 함수를 복사할 수 없으며 Error와 DOM 노드도 복사할 수 없다. 또, `structuredClone()`가 클래스 인스턴스를 복사한다면 반환 값은 일반 객체가 된다.

- [Lodash](https://lodash.com/)의 `cloneDeep(obj)`또는 `Ramda`의 `clone` 등을 사용하면 보다 정확한 복사를 할 수 있다.

