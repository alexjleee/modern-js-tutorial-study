# 브라우저 환경과 다양한 명세서

## 호스트 환경

- 자바스크립트는 본래 웹 브라우저에서 사용하기 위해 만들어졌으나 현재는 웹 브라우저뿐만 아니라 서버를 비롯한 다양한 호스트 환경(host environment)에서 사용할 수 있다.

- 각각의 호스트 환경은 랭귀지 코어(ECMAScript)에 더해 플랫폼에 특정된 객체와 함수를 제공한다.

  - 웹 브라우저 : 웹 페이지 제어 기능 제공
  
  - Node.js : 서버 사이드 기능 제공

## 브라우저 환경

![window objects](/images/part2_0101.png)

- `window` : 회상단 루트 객체

  - 자바스크립트 코드의 전역 객체

  - 브라우저 창(browser window)을 대변하며 이를 제어할 수 있는 메서드 제공

```javascript
function greet() {
  alert('Hello World');
}
window.greet(); // window가 전역 객체로 사용됨

alert(window.innerHeight); // window가 브라우저 창을 대변
```

## 문서 객체 모델 (DOM)

- 문서 객체 모델(Document Object Model, DOM)은 웹 페이지 내 모든 콘텐츠를 객체로 나타내며 이 객체는 수정 가능하다.

- `document` : 체이지의 기본 진입점, 이 객체를 이용해 페이지 내 모든 것을 수정/생성 할 수 있음

```javascript
document.body.style.backgroundColor = 'red';
// 페이지의 body 배경을 red로 변경
```

- cf. DOM은 브라우저가 아닌 곳에서도 사용되기도 한다. 예를 들어 HTML 페이지를 다운로드하고 이를 가공하는 서버 사이드에서도 DOM을 사용한다.

- cf. CSSOM : CSS 규칙과 스타일시트를 객체로 나타내고 이를 어떻게 읽고 쓸 지에 대한 명세서. 문서 스타일을 수정할 때 DOM과 함께 쓰인다. 드물지만 자바스크립트에서 CSS 규칙을 추가/제거해야 할 경우에도 사용된다.

## 브라우저 객체 모델 (BOM)

- 브라우저 객체 모델(Browser Object Model, BOM)은 문서 외의 모든 것을 제어하기 위해 브라우저가 제공하는 추가 객체를 말한다.

- HTML 명세서의 일부로 tag, attribute 같은 HTML 뿐만 아니라 다양한 객체, 메서드, 브라우저에서만 사용되는 DOM 확장을 다룬다.

- 예시

  - `navigator` : 브라우저와 운영체제에 대한 정보 제공. 가장 잘 알려진 프로퍼티로 현재 사용 중인 브라우저 정보를 알려주는 `navigator.userAgent`, 브라우저가 실행 중인 운영체제 정보를 알려주는 `navigator.platform`이 있다.

  - `location` : 현재 URL을 읽거나 새로운 URL로 변경할 수 있게 해 준다.

  - `alert`, `confirm`, `prompt` : 문서와 직접 연결되어 있지 않지만 사용자와 브라우저 사이의 소통을 도와주는 메서드