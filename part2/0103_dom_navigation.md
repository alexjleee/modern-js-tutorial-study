# DOM 탐색하기

- DOM을 이용해 특정 요소를 조작하기 위해서는 조작하고자 하는 DOM 객체에 먼저 접근해야 한다.

- DOM 진입은 `document` 객체에서 시작한다.

## DOM 트리 상단의 노드

- DOM 트리 상단의 노드들은 `document`의 프로퍼티를 통해 접근할 수 있다.

  - `<html>` : `document.documentElement`

  - `<body>` : `document.body`

  - `<head>` : `document.head`

- 주의! 스크립트를 읽는 도중에 아직 존재하지 않는 요소(`null`)는 스크립트가 접근할 수 없다. (예: 만약 스크립트가 `<head>` 안에 위치한다면 해당 스크립트에서는 `document.body`에 접근할 수 없다. 해당 스크립트를 읽는 시점에서는 아직 `<body>` 노드가 생성되지 않았기 때문이다.)

## 자식 노드 탐색

- 자식 노드(child node, children) : 바로 아래의 하위 요소. (예: `<head>`와 `<body>`는 `<html>`의 자식 요소)

- 후손 노드(descendants) : 하위의 모든 요소. 자식 노드뿐만 아니라 자식의 자식 등 모든 하위 노드.

### 자식 노드에 접근하는 데 사용할 수 있는 프로퍼티

- `childNodes` : 텍스트 노드를 포함한 모든 자식 노드

- `firstChild` : 첫 번째 자식 노드. `el.childNodes[0]`과 같다.

- `lastChild` : 마지막 자식 노드. `el.childNodes[el.childNodes.length - 1]`과 같다.

### DOM 컬렉션

- 컬렉션(collection) : _읽기 전용_ 프로퍼티로 마치 배열처럼 반복 가능한(iterable) 유사 배열 객체. (예: `childNodes`)

#### 컬렉션의 특징

- `for...of` 사용 가능 (컬렉션은 이터러블로, `Symbol.iterator`가 구현되어 있기 때문)

  - `for...in`은 사용하지 말 것. (컬렉션에 사용되는 추가 프로퍼티까지 순회 대상에 포함되기 때문)

- 배열이 아니기 때문에 `filter`, `map`과 같은 배열 메서드는 사용할 수 없다.

  - 배열 메서드를 사용하고 싶다면 `Array.from`을 사용하여 우선 배열로 만들어야 한다.

- DOM 컬렉션은 DOM의 현재 상태를 반영하기 때문에 컬렉션을 참조하고 있는 도중 DOM에 새로운 노드가 추가/삭제되는 것을 자동으로 반영한다.

## 형제 노드 & 부모 노드

- 형제 노드(sibling) : 부모가 같은 노드

  -예를 들어, `<head>`는 `<body>`의 이전(previous)/좌측(left) 형제 노드, `<body>`는 `<head>`의 다음(next)/우측(right) 형제 노드이다.

  - 다음 형제 노드는 `nextSibling`, 이전 형제 노드는 `previousSibling` 프로퍼티로 접근할 수 있다.

- 부모 노드(parent node) : 바로 위 상위 요소.

  - 부모 노드에 대한 정보는 `parentNode` 프로퍼티 참조

## 요소 간 이동

- 실무에서 주요하게 다루는 요소 노드(element)를 탐색하는 프로퍼티

  - `children` : 해당 요소의 자식 노드 중 요소 노드만

  - `firstElementChild`/`lastElementChild` : 해당 요소의 첫 번째/마지막 자식 요소 노드

  - `previousElementSibling`/`nextElementSibling` : 해당 요소의 이전/다음 형제 요소 노드

  - `parentElement` : 해당 요소의 부모 요소 노드

    - 해당 요소의 부모가 요소가 아닐 때 `null` 반환

    - `document.documentElement.parentNode === document`

    - `document.documentElement.parentElement !== document` : `document`는 요소 노드가 아님

## 테이블 탐색

- 일부 DOM 요소 노드는 편의를 위해 추가적인 프로퍼티를 지원하는데, 테이블이 가장 대표적이다.

### table

- `table.rows` : `<tr>` 요소를 담은 컬렉션 참조

- `table.caption/tHead/tFoot` : `<caption>/<thead>/<tfoot>` 요소를 참조

- `table.tBodies` : `<tbody>` 요소를 담은 컬렉션 참조. 테이블 내에 `<tbody>`가 최소 한 개 이상 존재해야 하므로 문서에 `<tbody>`가 없을 경우 해당 노드를 DOM에 자동으로 추가한다.

### thead, tfoot, tbody

- `rows` : 내부 `<tr>` 요소 컬렉션 참조

### tr

- `tr.cells` : 해당 `<tr>` 내부 모든 `<td>`, `<th>`를 담은 컬렉션 반환

- `tr.sectionRowIndex` : 해당 `<tr>`이 `<thead>/<tbody>/<tfoot>` 내에서 몇 번째 줄에 위치하는지 인덱스를 반환

- `tr.rowIndex` : 해당 `<tr>`이 `<table>` 내에서 몇 번째 줄인지 나타내는 인덱스를 반환

### td, th

- `td/th.cellIndex` : `<td>/<th>`가 속한 `<tr>` 내에서 해당 셀이 몇 번째인지 나타내는 인덱스를 반환

---

## 과제

### 모든 대각선 셀 선택하기

다음 테이블의 모든 대각선 셀을 빨간색으로 칠하는 코드를 작성하시오. (1:1, 2:2, 3:3, 4:4, 5:5가 있는 셀이 빨간색)

```html
<table id="table">
  <tbody>
    <tr>
      <td>1:1</td>
      <td>2:1</td>
      <td>3:1</td>
      <td>4:1</td>
      <td>5:1</td>
    </tr>
    <tr>
      <td>1:2</td>
      <td>2:2</td>
      <td>3:2</td>
      <td>4:2</td>
      <td>5:2</td>
    </tr>
    <tr>
      <td>1:3</td>
      <td>2:3</td>
      <td>3:3</td>
      <td>4:3</td>
      <td>5:3</td>
    </tr>
    <tr>
      <td>1:4</td>
      <td>2:4</td>
      <td>3:4</td>
      <td>4:4</td>
      <td>5:4</td>
    </tr>
    <tr>
      <td>1:5</td>
      <td>2:5</td>
      <td>3:5</td>
      <td>4:5</td>
      <td>5:5</td>
    </tr>
  </tbody>
</table>
```

```javascript
const table = document.getElementById('table');
for (let i = 0, n = table.rows.length; i < n; i++) {
  table.rows[i].cells[i].style.backgroundColor = 'red';
}
```
