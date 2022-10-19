---
title: '방향키 상하 이동 이벤트 | Array.prototype | nextSibling'
date: '2022-10-15'
tags: ['Vanilla JS', 'arrow event', 'array', 'Array.prototype', next Sibling, active Element]
draft: false
summary: 'Notion Clone 프로젝트 작업 : 방향키 눌렀을때 커서가 상하 요소로 이동하는 이벤트'
---

# 구상한 방법 1. wrapper id 배열

1. wrapper가 Enter event로 새로 생성될 때마다, 각 wrapper의 id를 `배열`에 담아
2. 현재 커서가 위치한 wrapper의 id를 받아온 후, 그 id가 `wrapper id 배열`에서 몇번째 인덱스인지 확인해
3. Arrow Down event 함수에서는 그 바로 다음 인덱스의 요소(id)를, Arrow Up event 함수에서는 그 바로 전 인덱스의 요소(id)를 받아와서
4. 해당 id를 갖는 wrapper를 찾아, 거기에 focus(커서 생기게) 하기

## 사용하려는 개념 : array.push()

```js
const newArr = new Array()
//undefined
newArr
//[]
newArr.push('123')
//1
newArr
//['123']
newArr.push('44')
//2
newArr
//['123', '44']
```

## 오류 상황

idArr라는 새 빈 배열을 생성해, 새 wrapper가 생길때마다 inputId를 push하려고 했으나  
➜ 문제 : console에서 확인해보면, idArr안에 inputId들이 누적되지 않고, 계속해서 새 inputId 하나만 담긴다

```js
const inputId = String(Math.floor(Math.random() * 1000000000))
wrapper.setAttribute('id', inputId)
// let idArr = [];   //new Array()와 .push를 쓰지않고, 빈 배열 []을 만든 후 push해도 마찬가지로 안됨
const idArr = new Array()
idArr.push(inputId)
console.log(idArr)
```

```js
textContainer.addEventListener('keydown', (e: any) => {
  // if (idArr.length <= 1) return;
  if ((e as KeyboardEvent).key === 'ArrowDown') {
    const currentFocusedId = e.path[1].id;
    const nextId = idArr.find((el) => idArr.indexOf(el) === idArr.indexOf(currentFocusedId) + 1);
    shadow.getElementById(nextId)?.focus(); //WebComponent로 작업한거라, document.getElementById가 아니고 shadow.getElementById로 해야 가져와짐
  }
  if ((e as KeyboardEvent).key === 'ArrowUp') {
  }
});
```

## 해결

new Array() 또는 []이 아닌, `Array.prototype`에 `push()`해야 작동함

```js
const inputId = String(Math.floor(Math.random() * 1000000000))
wrapper.setAttribute('id', inputId)
Array.prototype.push(inputId)
const idArr = Array.prototype
console.log(idArr)
```

---

# 구상한 방법 2. nextSibling, activeElement

`idArr.push()`가 안되고 있어서 이런 저런 시도하다가 nextSibling API 발견  
🔎 [nextSibling VS nextElementSibling 차이](https://aljjabaegi.tistory.com/548)

### +) 현재 Focus 찾는 `document.activeElement`

`shadow.activeElement`를 사용해, 현재 Focus 위치한 wrapper를 받아오려고 했으나  
➜ 문제 : 최상위 태그인 WebComponent Element `<text-input>`를 받아와서 사용 불가  
➜ 해결 :  
`console.log(e)`로 e에 어떤 데이터들 담겨오는지 확인해 ⇨ `e.path[1].id`로 현재 Focus돼있는 wrppaer의 id 받아온 후 ⇨ `shadow.getElementById(currentFocusedId)`로 해당 id를 가진 wrapper를 변수에 담아 사용

## 오류 상황

[써치한 방법](https://newspatrak.com/javascript/property-focus-does-not-exist-on-element/) 대로 `as HTMLElement` 타입 설정 했는데도  
➜ nextElementSibling로 focus(커서 이동) 안됨

```js
textContainer.addEventListener('keydown', (e: Event) => {
  const currentFocusedId = (<any>e).path[1].id;
  const currentFocused = shadow.getElementById(currentFocusedId);
  if ((e as KeyboardEvent).key === 'ArrowDown') {
    const next = currentFocused.nextElementSibling as HTMLElement;
    next.focus(); //안됨
  }
  if ((e as KeyboardEvent).key === 'ArrowUp') {
    const prev = currentFocused.previousElementSibling as HTMLElement;
    prev.focus(); //안됨
  }
});
```

## 해결

`currentFocused.nextElementSibling`는 *wrapper*태그  
➜ `currentFocused.nextElementSibling.children[0].children[1]`로 *text*태그에까지 들어가 접근해야 Focus 줄 수 있음

```js
textContainer.addEventListener('keydown', (e: Event) => {
  // const currentFocused = shadow.activeElement.parentElement
  const currentFocusedId = (<any>e).path[1].id;
  const currentFocused = shadow.getElementById(currentFocusedId);
  if ((e as KeyboardEvent).key === 'ArrowDown') {
    (currentFocused.nextElementSibling.children[0].children[1] as HTMLElement).focus();
  }
  if ((e as KeyboardEvent).key === 'ArrowUp') {
    (currentFocused.previousElementSibling.children[0].children[1] as HTMLElement).focus();
  }
});
```

## 완성

맨 아래/위 wrapper인 경우 처리 추가

```js
textContainer.addEventListener('keydown', (e: Event) => {
  const currentFocusedId = (<any>e).path[1].id;
  const currentFocused = shadow.getElementById(currentFocusedId) as HTMLElement;
  if ((e as KeyboardEvent).key === 'ArrowDown') {
    if (!currentFocused.nextElementSibling) return;
    (currentFocused.nextElementSibling.children[0].children[1] as HTMLElement).focus();
  }
  if ((e as KeyboardEvent).key === 'ArrowUp') {
    if (!currentFocused.previousElementSibling.children[0]) return;
    (currentFocused.previousElementSibling.children[0].children[1] as HTMLElement).focus();
  }
});
```

---

# 추가)

## drag and drop 작업 하면서 wrapper에 id를 없게 조정하면서, 수정한 arrow event 최종 코드

이제 wrapper에는 id값이 없고 textContainer에 id값이 있기 때문에, `shadow.getElementById((<any>e).path[1].id)` 하면 textContainer를 받아오므로  
➜ wrapper를 받아오기 위해 `.parentElement`를 추가해, focusedWrapper에 저장해 사용

```js
const inputId = String(Math.floor(Math.random() * 1000000000));
// wrapper.setAttribute("id", inputId);
// ...(중략)
textContainer.addEventListener("keydown", (e: Event) => {
  const focusedWrapper = shadow.getElementById((<any>e).path[1].id).parentElement as HTMLElement;

  if ((e as KeyboardEvent).key === "ArrowDown") {
    if (!focusedWrapper.nextElementSibling) return;
    (focusedWrapper.nextElementSibling.children[0].children[1] as HTMLElement).focus();
  }

  if ((e as KeyboardEvent).key === "ArrowUp") {
    if (!focusedWrapper.previousElementSibling.children[0]) return;
    (focusedWrapper.previousElementSibling.children[0].children[1] as HTMLElement).focus();
  }

  shadow.activeElement.setAttribute("placeholder", 'Type "/" for commands');
  if (text !== shadow.activeElement) {
    text.removeAttribute("placeholder");
  }
});
```
