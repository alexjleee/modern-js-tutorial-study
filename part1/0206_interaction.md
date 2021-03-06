# alert, prompt, confirm을 이용한 상호작용

## alert, propmt, confirm

- 브라우저는 사용자와 상호작용할 수 있는 함수(`alert`, `prompt`, `confirm`)를 제공한다. 세 함수 모두 모달(modal)로 사용자와 상호작용하며 이 모달이 닫힐 때까지 사용자는 웹 페이지의 다른 부분과 상호작용할 수 없다.

  - 모달 창의 위치는 각 브라우저가 결정하며, 대개 브라우저 중앙에 위치한다.

  - 모달 창의 모양은 브라우저마다 다르며 개발자가 임의로 수정할 수 없다.

### alert

- 사용자가 '확인(OK)' 버튼을 누를 때까지 메시지를 보여주는 경고 모달 창을 띄운다.

- `alert([message])`

### prompt

- 사용자가 텍스트를 입력할 수 있는 입력 필드, 확인(OK) 및 취소(Cancel) 버튼이 있는 대화 모달 창을 띄운다.

- `prompt([message, default])`

- 두 번째 매개변수로 입력 필드의 초깃값을 지정해줄 수 있다. 이 매개변수는 선택사항이지만 IE에서는 이 매개변수가 없는 경우 `undefined`를 입력 필드에 명시한다.

- 사용자가 입력 필드에 입력한 문자열 또는 사용자가 입력을 취소한 경우 `null`을 반환하다.

- 예: `let age = prompt('나이를 입력하세요', 18)`;

### confirm

- 질문과 확인(OK) 및 취소(Cancel) 버튼을 가진 대화 모달 창을 띄운다.

- `confirm([question])`

- 사용자가 확인 버튼을 누르면 `true`, 그 외의 경우에는 `false`를 반환한다.

- 예: `let isAdult = confirm('만 18세 이상이십니까?')`
