---
title: 'Redux'
date: '2022-09-19'
lastmod: '2022-09-19'
tags: ['Redux']
draft: true
summary: 'Redux 세미나 준비'
---

# without Redux VS with Redux : Redux 사용 이유

### 1. Store 한 곳에만 상태 저장해 각 컴포넌트가 가져다 쓰므로, props drilling 방지

### 2. 상태 수정 API들을 Store 한 곳에 모두 만들어놓으므로, 버그 발생 시 원인 추적 용이함

---

# React 프로젝트 생성해, Redux 구현해보기

[Redux](https://ko.redux.js.org/tutorials/quick-start)

```js
npx create-react-app redux-seminar
cd redux-seminar
// Add the Redux Toolkit and React-Redux packages to your project:
npm install @reduxjs/toolkit react-redux
```

```js
// src/app/store.js
import { configureStore } from '@reduxjs/toolkit'

export default configureStore({
  reducer: {},
})
// This creates a Redux store, and also automatically configure the Redux DevTools extension
// so that you can inspect the store while developing.
```

---
