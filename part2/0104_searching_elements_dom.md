# getElement*, querySelector*로 요소 검색하기

## document.getElementById 또는 id로 요소 검색하기

- `document.getElementById(id)` : 요소에 `id` 속성이 있는 경우 이를 이용해 요소에 접근할 수 있다.

  - `getElementById`는 `document` 객체를 대상으로만 호출할 수 있다.

- `id` 속성값과 똑같은 이름의 전역 변수로도 접근할 수 있다.

  - `id` 속성값이 변수 이름 규칙에서 어긋나는 경우 대괄호를 사용해 `window['id-name']`으로 접근할 수 있다.

  - `id` 속성값을 따서 자동으로 선언된 전역 변수는 스크립트 내에서 같은 이름을 가진 변수가 선언되면 더 이상 사용할 수 없다.

  - 이름 충돌 가능성이 있고, HTML 파일을 참조하지 않는 이상 코드만 보고 변수의 출처를 알기 힘들다는 단점이 있으므로 실무에선 `document.getElementById`를 사용하자.

  - 문서 내 `id` 속성 값은 중복되어선 안 된다.

```html
<div id="selectme"></div>
<div id="select-me"></div>
<script>
  let selectedElement = document.getElementById('selectme'); // === selectme
  let selectedElement = document.getElementById('select-me'); // === window['select-me']

  let selectme = 'now, this is new select me variable'; // selectme !== selectedElement
</script>
```

## getElementBy\*

- `getElementBy*` 메서드를 사용해 태그나 클래스 등을 이용해 원하는 노드를 찾을 수 있다.

  - `element.getElementByTagName(tag)` : 주어진 태그에 해당하는 모든 요소를 담은 컬렉션을 반환한다. (`tag`에 `'*'`이 들어가면 모든 태그가 검색된다.)

  - `element.getElementsByClassName(className)` : 주어진 값을 `class` 속성값으로 가지는 모든 요소를 담은 컬렉션을 반환한다.

  - `document.getElementByName(name)` : 문서 전체에서 주어진 값을 `name` 속성값으로 가지는 모든 요소를 담은 컬렉션을 반환한다. (아주 드물게 쓰인다.)

- `getElementsBy*` 메서드는 _살아있는_ 컬렉션을 반환한다. 문서에 변경이 있을 때마다 컬렉션은 자동으로 갱신된다.

## querySelectorAll

- CSS 선택자를 사용하여 다양한 방법으로 요소 선택 가능

  - `id`, `class` 속성값뿐만 아니라 `p`, `ul > li`, `li:first-child`, `:hover`와 같이 다양한 CSS 선택자를 사용해 선택할 수 있다.

  - 주어진 CSS 선택자에 대응하는 모든 요소를 탐은 컬렉션이 반환되며 DOM 트리 순서를 따른다.

```html
<ul>
  <li>green</li>
  <li>green</li>
  <li>green</li>
</ul>
<script>
  let liElements = document.querySelectorAll('li');
  for (let elem of liElements) {
    elem.style.color = 'green';
  }
</script>
```

## querySelector

- 주어진 CSS 선택자에 대응하는 요소들 중 첫 번째 요소를 반환한다.

- `element.querySelector(css)`는 `element.querySelectorAll(css)[0]`와 결과는 동일하지만 첫 번째 요소를 찾은 뒤 검색을 멈추기 때문에 더 빠르다.

## matches

- `element.matches(css)`는 요소 `element`가 주어진 CSS 선택자와 일치하면 `true`, 아니면 `false`를 반환한다.

- 요소가 담겨 있는 배열을 순회하며 특정 요소만 걸러내고자 할 때 유용하다.

## closest

- `element.closest(css)`는 `element` 자기 자신을 포함하여 CSS 선택자와 일치하는 가장 가까운 조상 요소를 반환한다. 가장 먼저 일치하는 요소를 반환하고 검색을 중단한다.
