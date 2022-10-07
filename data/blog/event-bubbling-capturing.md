---
title: 'Event Bubbling & Capturing | onClick함수 id 이슈 해결'
date: '2022-10-05'
tags: ['event bubbling', 'event capturing', 'propagate up', 'propagate down']
draft: true
# summary: ''
---

[🔗참고](https://youtu.be/7gKtNC3b_S8)

## 이벤트 버블링(propagate down) : default

맨아래html - 그 위body - 그 위div (가시적으로 명확하게 이해하기위해 html, body를 예시로 들었지만 div들끼리도 마찬가지)

- 세 요소 각각 모두 클릭이벤트를 갖고있을 때, 클릭 이벤트의 직접 대상인 div을 클릭할 경우, 이벤트 버블링이 발생해, div의 클릭이벤트 실행된 후 → div의 부모요소인 body의 클릭이벤트가 실행되고 → body의 부모요소인 html의 클릭이벤트가 실행된다
- 현재 클릭한 요소의 클릭이벤트 뿐만 아니라 그 부모, 부모…의 클릭이벤트까지 실행되어버리므로, 이를 막아야 할 경우 `event.currentTarget`을 사용하면 현재 클릭한 요소의 클릭이벤트만 실행된다

## 이벤트 캡쳐링(propagate up)

- html(or body)에 이벤트 캡쳐링 설정 할 경우 : 버블링과 반대 방향으로, div를 클릭했음에도 불구하고, html(or body)의 클릭이벤트가 먼저 실행되고 → 그 다음에 div → body(or html)의 클릭이벤트 순서로 실행된다
- html과 body 모두에 이벤트 캡쳐링 설정할 경우 : div를 클릭했음에도 불구하고, html이 가장 먼저 실행 → 그 다음 body → 그 다음 div가 실행된다

```js
// html
<body>
  <div>CLICK!</div>
</body>
```

```js
// JavaScript
const html = document.documentElement
const body = document.body
const div = document.querySelector('div')

html.addEventListener('click', function () {
  console.log('HTML CLICK EVENT!')
})

body.addEventListener('click', function () {
  console.log('BODY CLICK EVENT!')
})

div.addEventListener('click', function () {
  console.log('DIV CLICK EVENT!')
})
```

⇧ 이대로 하면 출력 순서(이벤트 버블링): div -> body -> html

➜ 이벤트 캡쳐링으로 설정: addEventListner의 세번째 인자로 true를 넣으면, 해당 요소의 클릭이벤트가 클릭한 요소의 이벤트보다 먼저 실행됨

---

# onClick함수 id 이슈

```js
// Container
const onClickMenu = (event: React.MouseEvent<HTMLElement>) => {
  if (event.target instanceof Element) {
    props.setSelectedMenu(event.target.id)
  }
}
```

## 수정 전(오류)

전체를 감싸고

```js
// Presenter
<div>
  <div>
    <div id="menu 1" onClick={onClickMenu}>
      MENU 1
    </div>
    <div>Subtitle</div>
  </div>
</div>
```

## 수정 후(해결)

```js
// Presenter
<div id="menu 1" onClick={onClickMenu}>
  <div id="menu 1">
    <div id="menu 1">MENU 1</div>
    <div id="menu 1">Subtitle</div>
  </div>
</div>
```
