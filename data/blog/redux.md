---
title: 'Redux, Redux Toolkit'
date: '2022-09-20'
lastmod: '2022-09-20'
tags: ['Redux', 'Redux Toolkit', 'RTK']
draft: false
summary: 'Redux 사용이유, 흐름, 3가지 원칙 | RTK 사용이유, API | React 프로젝트에 RTK 적용 코드'
---

# Redux 사용 이유

1. Store 한 곳에만 상태 저장해두고 각 컴포넌트가 가져다 쓰므로, props drilling 해결
2. 상태 변경 API(reducer)들을 Store 한 곳에 모두 만들어놓으므로, 버그 발생 시 원인 추적 용이함

<Image src="/static/images/withoutvswithredux.png" width="500" height="380"/>
<Image src="/static/images/rtkflow.png" width="700" height="600"/>

---

# Redux 3가지 원칙

1. Single source of truth  
   : 애플리케이션의 상태는 Store라는 단 하나의 저장소 안에 저장되어 관리됨
2. State is read-only  
   : 상태는 읽기 전용이다. 상태를 변화시키는 방법은 action을 reuducer에 전달(dispatch) 뿐
3. Changes are made with pure functions  
   : reducer는 이전 상태와 액션을 받아 다음 상태를 반환하는 순수함수이며, 이전 상태를 변경하는 것이 아닌 새로운 상태 객체를 반환해야함

---

# Redux Toolkit 사용 이유

1. Redux store 구성 설정 코드 간소화 : action creator와 action type을 따로 생성하지 않아도 됨(`configureStore()`)
2. Redux를 유용하게 사용하려면 많은 패키지들을 추가 설치해야했는데, RTK API에 미리 내장되어있음
3. Redux의 Boilerplate code(중복 코드) 줄여줌

---

# Redux Toolkit API

[MDN tutorial](https://redux-toolkit.js.org/usage/usage-guide)

### `configureStore()` : 기존의 `createStore()`를 개선

- middleware 추가 편리
- `redux-thunk`가 내장되어있어 비동기를 지원
- Redux DevTools Extension 사용 가능

### `createReducer()`

### `createAction()`

### `createSlice()`

### `createAsyncThunk()`

### `createEntityAdapter()`

---

# React 프로젝트에 Redux ToolKit 적용

## React 프로젝트 생성 + Redux Toolkit 설치

```
npx create-react-app redux-rtk-seminar
cd redux-rtk-seminar
yarn
yarn add @reduxjs/toolkit
yarn add redux react-redux
yarn start
```

## 1. Create a Redux Store | 4. Add Slice Reducers to the Store

#### without RTK: `createStore` 미사용 유도(자동으로)

```javascript
// src/app/store.js
import { applyMiddleware, createStore } from '@reduxjs/toolkit'
import { composeWithDevTools } from '@reduxjs/toolkit/dist/devtoolsExtension'
import counterReducer from '../features/counter/counterSlice'
import thunk from 'redux-thunk'

export default createStore(counterReducer, composeWithDevTools(applyMiddleware(thunk)))
```

#### RTK: `configureStore` 사용

```javascript
// src/app/store.js
import { configureStore } from '@reduxjs/toolkit'
import counterReducer from '../features/counter/counterSlice'

export default configureStore({
  reducer: {
    counter: counterReducer,
  },
})
```

## 2. Provide the Redux Store to React

```javascript
// src/index.js
...
import { Provider } from 'react-redux'
import store from './app/store'

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>
)

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals()
```

## 3. Create a Redux State Slice: reducer -> createSlice(RTK)

#### without RTK: action creator + reducer

```javascript
const initialState = {
  value: 0,
}

function counterReducer(state = initialState, action) {
  let { type, payload } = action
  switch (type) {
    case 'INCREMENT': //action은 대문자 표기
      return (state += 1)
    case 'DECREMENT':
      return (state -= 1)
    default:
      return state.value
  }
}
export default counterReducer
```

#### RTK: `createSlice`(slice이름, state초기값, reducer함수로 구성된 객체) -> 자동으로 action creator와 action type 생성됨

```javascript
// src/features/counter/counterSlice.js
import { createSlice } from '@reduxjs/toolkit'

const initialState = {
  value: 0,
}

export const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment(state) {
      state.value += 1
    },
    decrement(state) {
      state.value -= 1
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload
    },
  },
})
export const { increment, decrement, incrementByAmount } = counterSlice.actions
export default counterSlice.reducer
```

## 5. Use Redux State and Action in React Components

```javascript
// src/features/counter/Counter.js
import React from 'react'
import { useSelector, useDispatch } from 'react-redux'
import { decrement, increment } from './counterSlice'

export function Counter() {
  const count = useSelector((state) => state.counter.value)
  const dispatch = useDispatch()

  return (
    <div>
      <button aria-label="Decrement value" onClick={() => dispatch(decrement())}>
        Decrement
      </button>
      <span>{count}</span>
      <button aria-label="Increment value" onClick={() => dispatch(increment())}>
        Increment
      </button>
    </div>
  )
}
```

## 6. App컴포넌트에 Counter컴포넌트(Action 발생시키는)를 import

```javascript
import './App.css'
import { Counter } from './features/counter/Counter'

function App() {
  return <Counter />
}

export default App
```
