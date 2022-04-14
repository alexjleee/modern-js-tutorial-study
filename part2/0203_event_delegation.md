# 이벤트 위임

## 이벤트 위임은 언제 사용할까

- 비슷한 방식으로 여러 요소를 다루어야 할 때

- 이벤트 위임을 사용하면 각 요소마다 핸들러를 다는 대신, 공통 조상 요소에 하나의 이벤트 핸들러를 달아 여러 요소를 한꺼번에 다룰 수 있다.

  - 공통 조상의 핸들러는 `event.target`을 통해 실제 이벤트가 발생한 요소를 특정할 수 있다.

- 이렇게 구현하면 핸들러가 각각의 요소에 달리는 것이 아니기 때문에 그 개수에 상관없이 빠르고 효율적으로 구현할 수 있다.

## 이벤트가 원하는 요소의 자식 요소에서 일어날 경우

```html
<table>
  <tr>
    <td class="nw"><strong>Northwest</strong></td>
    <td class="n"><strong>North</strong></td>
    <td class="ne">...</td>
  </tr>
  <tr>
    ...
  </tr>
  <tr>
    ...
  </tr>
</table>
```

```javascript
table.onClick = function (event) {
  let td = event.target.closest('td');
  // elem.closest(selector) : elem의 상위 요소 중 selector와 일치하는 가장 근접한 조성 요소 반환
  if (!td) return; // 선택된 td가 없다면 즉시 리턴
  if (!table.contains(td)) return; // 선택된 td가 table 밖에 있다면 즉시 리턴
  // do something with td
};
```

## 이벤트 위임 활용

- 여러 기능을 하는 버튼을 담은 메뉴를 만들어야할 때, 각 버튼의 기능과 관련된 메서드를 담은 객체는 구현되어 있는 상태에서, 어떻게 버튼과 메서드를 연결해야 할까?

  - Option 1. 각 버튼에 독립적인 핸들러를 할당한다.

  - Option 2. 버튼들을 담은 메뉴에 하나의 핸들러를 할당한 뒤, 각 버튼의 `data-action` 속성에 호출할 메서드를 할당해 준다.

- 이벤트 위임을 활용하면 버튼마다 일일이 핸들러를 할당하는 코드를 작성할 필요가 없고, 언제든지 버튼을 추가/제거할 수 있어 HTML 구조가 유연해진다.

- 핸들러의 개수가 줄어들기 때문에 초기화가 단순해지고 메모리가 절약된다.

```html
<div id="menu">
  <button data-action="save">저장하기</button>
  <button data-action="load">불러오기</button>
  <button data-action="search">검색하기</button>
</div>
```

```javascript
class Menu {
  constructor(elem) {
    this._elem = elem;
    elem.onClick = this.onClick.bind(this);
    // cf. this.onClick을 this에 바인딩 (이렇게 하지 않으면 this는 Menu 객체가 아닌 이벤트를 호출한 DOM 요소를 참조하게 됨)

    save() {
      // 저장하기 관련 코드
    }

    load() {
      // 불러오기 관련 코드
    }

    search() {
      // 검색하기 관련 코드
    }

    onClick(event) {
      let action = event.target.dataset.action;
      if (action) {
        this[action]();
      }
    }
  }
}

new Menu(menu);
```

## '행동' 패턴

- 이벤트 위임은 요소에 *선언적*으로 행동(behavior)을 추가할 때 사용할 수도 있다.

1. 요소의 행동을 설명하는 커스텀 속성을 요소에 추가한다.

2. 문서 전체에 할당된 핸들러가 이벤트를 추적하여 1에서 추가한 속성이 있는 요소에서 이벤트가 발생하면 작업을 수행한다.

- 주의! 문서 레벨의 핸들러를 만들 때는 항상 `addEventListener`를 사용한다. `document.onClick`은 충돌을 일으킬 가능성이 있다. (새로운 핸들러가 이전 핸들러를 덮어쓸 수 있음)

- 예: 토글러

```html
<button data-toggle-id="toggle-div">
  아래의 div를 토글
</button>

<div id="toggle-div" hidden>
  버튼을 누르면 보이게 됩니다
</form>

<script>
  document.addEventListener('click', function(event) {
    let id = event.target.dataset.toggleId;
    if (!id) return;
    let elem = document.getElementById(id);
    elem.hidden = !elem.hidden;
  });
</script>
```

- 이제 태그에 `data-toggle-id` 속성만 추가하면 속성값을 id로 가진 요소를 토글할 수 있게 된다.

## 이벤트 위임의 단점

- 이벤트 위임을 사용하기 위해서는 반드시 이벤트 버블링이 일어나야 한다. 하지만 몇몇 이벤트는 버블링 되지 않는다.

- 낮은 레벨에 할당한 핸들러에 `event.stopPropagation()`을 쓸 수 없다.

- 공통 부모 요소에 할당된 핸들러가 응답할 필요가 있든 없든 모든 하위 요소의 이벤트에 응답해야 하므로 CPU 작업 부하가 늘어날 수 있다. (하지만 이는 무시할만한 수준이다.)
