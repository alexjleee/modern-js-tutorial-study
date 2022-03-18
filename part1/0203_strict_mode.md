# 엄격 모드

## 엄격 모드 (Strict Mode)

- ES5에서 추가된 엄격 모드를 사용하면 자바스크립트 문법을 좀 더 엄격하게 적용하여 오류를 발생시킬 가능성이 높은 코드에 대해 명시적 에러를 발생시킨다.

- `'use strict'`(또는 `"use strict"`)라는 특별한 지시자를 사용해 엄격 모드를 활성화 할 수 있다.

- ES6에서 추가된 클래스나 모듈을 사용하면 `use strict`가 자동으로 적용되기 때문에 `'use strict'` 지시자를 사용할 필요가 없다.

- `'use strict'` 지시자는 스크립트의 최상단 또는 함수 본문의 최상단에 위치할 수 있다. 스크립틔의 최상단에 위치할 경우 전체 스크립트가, 함수 본문 최상단에 위치할 경우 해당 함수만 엄격 모드로 실행된다.

  - 최상단에 위치하지 않으면 엄격 모드가 활성화되지 않을 수 있으므로 반드시 최상단에 와야 한다.

  - 일단 엄격 모드가 활성화되면 비활성화 할 수 없다.

```javascript
// sloppy mode
function returnX() {
  x = 10;
  return x;
}
returnX();
// 엄격 모드가 아닐 때, 선언하지 않은 변수를 참조하면 암묵적으로 전역 객체에 해당 프로퍼티를 동적으로 생성한다.
```

```javascript
// strict mode
'use strict';
function returnX() {
  x = 10; // ReferenceError: x is not defined
  return x;
}
returnX();
```

## 엄격 모드가 발생시키는 에러

- 선언하지 않은 변수 참조시 ReferenceError 발생

- `delete` 연산자로 변수, 함수, 매개변수를 삭제하면 SyntaxError 발생

- 중복된 매개변수 이름 사용시 SyntaxError 발생
