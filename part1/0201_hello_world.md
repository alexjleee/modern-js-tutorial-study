# Hello, world!

## script 태그

- `<script>` 태그는 HTML 문서의 `<head>` 또는 `<body>`에 위치할 수 있다.

### 내부 스크립트

- `<script>` 태그 안에 자바스크립트 코드를 입력한다.

```html
<!DOCTYPE HTML>
<html>
  <body>
    <script>
      alert('Hello, world!');
    </script>
  <body>
</html>
```

### 외부 스크립트

- 자바스크립트 코드를 JS 파일에 저장한 뒤 `<script>` 태그의 `src` 속성을 사용해 HTML에 삽입할 수 있다.

  - `src` 속성이 있으면 내부 코드는 무시된다.

  - `src` 속성의 값으로는 파일이 위치한 절대 경로, 상대 경로, 또는 URL이 들어갈 수 있으며 복수의 스크립트 파일을 삽입하고 싶다면 `<script>` 태그를 여러 개 사용하면 된다.

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.11/lodash.js"></script>
<script src="script.js"></script>
```

- 내부 스크립트는 코드가 아주 간단할 때만 사용한다. 코드가 길어지면 별도의 파일로 만드는 것이 좋다. 외부 스크립트의 경우 캐시에 저장되며 여러 페이지에서 동일 스크립트를 사용하는 경우 페이지가 바뀌어도 스크립트를 새로 다운받지 않고 캐시에서 스크립트를 가져와 사용하기 때문에 성능상 이점이 있다.

### 속성

- `type`

  - HTML4에선 `type="text/javascript"와 같이 스크립트 타입을 명시하는 것이 필수였으나 HTML5부터는 필수가 아니다. HTML5에서는 자바스크립트 모듈에 사용되고 있다.

- `async`, `defer`

  - 브라우저가 구문 분석을 진행하다가 내부 스크립트 또는 `async`, `defer`, `type="module"` 속성이 없는 스크립트를 만나면 해당 스크립트를 실행하기 전까지 분석을 중단한다.

  - `async`와 `defer`를 사용하면 스크립트가 백그라운드에서 다운로드되는 동안 HTML 분석이 멈추지 않는다. `async` 속성을 가진 스크립트는 다운로드가 완료된 즉시 실행되는반면 `defer` 속성을 가진 스크립트는 HTML 분석이 끝난 후에 실행된다.
