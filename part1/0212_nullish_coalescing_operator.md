# nullish 병합 연산자 ??

- `operand1 ?? operand2`

- 왼쪽 피연산자가 `null` 또는 `undefined`인 경우 오른쪽의 피연산자를 반환하고 아닐 경우 왼쪽 피연산자를 반환한다.

- `??` 연산자를 사용하면 피연산자들 중 값이 정의된 변수를 빠르게 찾을 수 있다.

- 변수에 기본값을 설정할 때 유용하게 쓸 수 있다.

- ES11에서 도입된 최신 문법으로 구식 브라우저는 폴리필이 필요하다.

```javascript
let name = null;
let nickname = null;

alert(name ?? nickname ?? '익명'); // 익명
// name이 없는 경우 nickname이, nickname도 없는 경우 '익명'이 표시됨
```

## ??와 ||의 차이

- `||`는 첫 번째 truthy 값을 반환

- `??`는 첫 번째 정의된(defined) 값을 반환

  - `null`, `undefined`와 falsy 값(예: `0`, `''` 등)을 구분해야 할 때는 `??`를 써야 한다.

```javascript
let height = 0;
alert(hegith || 100); // 100
// => ||는 0을 falsy값으로 취급하여 null이나 undefined를 할당한 것과 동일하게 처리
alert(height && 100); // 0
// => ??는 height가 정확하게 null이나 undefined일 경우에만 100을 반환
```

## 연산자 우선순위

- `??` 연산자의 우선순위는 5로 낮은 편이다.

  - 대다수 연산자보다 낮고 `?`, `=`보다는 높음

- 복잡한 표현식에서 `??`를 사용할 경우 괄호를 추가하는 것이 좋다.

```javascript
let area = (height ?? 100) * (width ?? 50);
// 여기서 괄호를 사용하지 않으면 *가 ??보다 우선순위가 높아 먼저 실행됨
```

- 안정성 관련 이슈 때문에 `??`를 `&&`나 `||`와 함께 사용할 수 없다. 함께 사용할 경우 문법 에러가 발생한다. 제약을 피하려면 괄호를 사용하면 된다.

```javascript
let x;
x = 1 && 2 ?? 3; // SyntaxError
x = (1 && 2) ?? 3; // 2
```