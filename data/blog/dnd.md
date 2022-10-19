---
title: 'Drag and Drop 개발'
date: '2022-10-19'
tags: [web component, drag and drop, dnd]
draft: false
summary: 'Notion Clone project(WebComponent) : Drag and Drop으로 행 상하 이동 및 CSS'
---

📌 [Web Component](https://developer.mozilla.org/ko/docs/Web/Web_Components)로 제작함([참고](https://www.webcomponents.org/introduction))

🔗 [MDN) drag and drop API](https://developer.mozilla.org/ko/docs/Web/API/HTML_Drag_and_Drop_API#%EC%96%B4%EB%96%A4_%EA%B2%83%EC%9D%B4_draggable%EC%9D%B8%EC%A7%80_%ED%99%95%EC%9D%B8%ED%95%98%EA%B8%B0)

---

<Image src="/static/images/dnd.gif" width="500" height="200" />

---

## [1️단계] drag와 drop 할 요소(textContainer)에

- draggable 속성 값을 true로 설정
- dragstart, dragover, drop, dragend 함수를 연결

```js
const inputId = String(Math.floor(Math.random() * 1000000000))
const textContainer = document.createElement('div')
textContainer.setAttribute('id', inputId)
textContainer.setAttribute('draggable', 'true')
const dragHandler = document.createElement('img')
dragHandler.setAttribute('draggable', 'true')
const text = document.createElement('div')
text.setAttribute('contenteditable', 'true')
textContainer.appendChild(dragHandler)
textContainer.appendChild(text)

textContainer.ondragstart = handleDragStart
textContainer.ondragover = handleDragOver
textContainer.ondrop = handleDrop
textContainer.ondragend = handleDragEnd
```

⇧ textContainer의 자식요소로 dragHandler와 text가 있는 구조로, dragHandler를 잡아 끌어서 drag와 drop하는 방식

---

## [2단계] dragstart함수 : event target(=drag중인 dragHandler)의 textContainer의 id를 저장

- 🎨Style : dragend된 text는 배경색 ❌ 되도록, 모든 text들 배경색 ❌

```js
function handleDragStart(e: DragEvent) {
  e.dataTransfer.setData(
    "text/plain",
    (e.target as HTMLElement).parentElement.id
  );
  e.dataTransfer.dropEffect = "move";
  //🎨Style
  shadow.querySelectorAll(".text").forEach(
    (el) => ((el as HTMLElement).style.backgroundColor = "white")
  );
}
```

---

## [3단계] dragover함수 : event target = over한 위치에 있는 textContainer

- 🎨Style : over 되어있을 때는 아래 테두리 ⭕️ ➜ 지나가서 over상태 아니면 아래 테두리 ❌

```js
function handleDragOver(e: DragEvent) {
  e.preventDefault();
  e.dataTransfer.dropEffect = "move";
  let overText = (e.target as HTMLElement).children[1] as HTMLElement;
  //🎨Style
  if (overText === undefined) return;
  overText.style.borderBottom = "4px solid rgb(228, 238, 251)";
  //🎨Style
  shadow.querySelectorAll(".text").forEach(
    (el) => el !== overText && ((el as HTMLElement).style.borderBottom = "none")
  );
}
```

---

## [4단계] drop함수 : event target = drop한 위치에 있는 textContainer

- 🎨Style : 아래 테두리 ❌ + 배경색 ❌

```js
function handleDrop(e: DragEvent) {
  e.preventDefault();

  //📌 전체textContainer들의 배열 안에서 drag와 drop의 인덱스 전후 순서 비교해 Style 주기
  //1️⃣ 전체textContainer들의 배열 만들기
  const allTextContainers = shadow.querySelectorAll(".text-container");

  //2️⃣ textContainer들은 각각 고유의 id값(inputId)을 갖고있다(1단계 코드 참고)
  //handleDragStart함수에서 저장한, drag해온 textContainer의 id를
  const data = e.dataTransfer.getData("text/plain");
  //id값으로 갖는 textContainer가 전체textContainer들 배열 안에서 몇번째 인덱스인지 저장
  const dragIndex = Array.from(allTextContainers).indexOf(shadow.getElementById(data));

  //3️⃣ drop한 위치의 textContainer가
  const dropTextContainer = e.target as HTMLElement;
  //전체textContainer들 배열 안에서 몇번째 인덱스인지 저장
  const dropIndex = Array.from(allTextContainers).indexOf(dropTextContainer);

  //4️⃣ drag해온 textContainer가 (1)textContainer들 중 맨 마지막에 위치했었거나 or (2)drop한 위치의 textContainer보다 뒤에 위치할 경우
  //➜ 즉 뒤에서 앞으로 이동하는 경우이므로, insertBefore(위치시킬 요소, 어느 요소의 바로앞에 위치시킬건지)
  if (dragIndex === -1 || dragIndex > dropIndex) {
    dropTextContainer.parentElement.insertBefore(
      shadow.getElementById(data), dropTextContainer
    );
  //drag해온 textContainer가 drop한 위치의 textContainer보다 앞에 위치할 경우
  //➜즉 앞에서 뒤로 이동하는 경우이므로, appendChild(위치시킬 요소)로 맨끝에 위치시킴
  } else if (dragIndex < dropIndex) {
    dropTextContainer.parentElement.appendChild(
      shadow.getElementById(data)
    );
  }

  //🎨Style
  (dropTextContainer.children[1] as HTMLElement).style.borderBottom = "none";
  (dropTextContainer.children[1] as HTMLElement).style.backgroundColor = "white";
}
```

---

## [5단계] dragend함수 : event target = drag해오다가 drop까지 완료한 dragHandler

- 🎨Style : 배경색 ⭕️

```js
function handleDragEnd(e: DragEvent) {
  //🎨Style
  ((e.target as HTMLElement).nextElementSibling as HTMLElement).style.backgroundColor
  = "rgb(228, 238, 251)";
}
```
