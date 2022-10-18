---
title: 'Life cycle(Class 컴포넌트) & useEffect(함수형 컴포넌트)'
date: '2022-10-18'
tags: [class component, life cycle, functional component, useEffect]
draft: false
summary: 'Class형 컴포넌트의 컴포넌트 생명주기 메서드, 그리고 함수형 컴포넌트의 useEffect'
---

# 컴포넌트의 생명주기(Life Cycle)

## 1. render

: 클래스형 컴포넌트의 render method or 함수형 컴포넌트를 호출해, DOM을 만드는 instruction set을 반환받는 것

## 2. mount

: 최초로 컴포넌트 렌더링해 받은 instructions set을 이용해 실제로 최초로 DOM을 만드는 것

| Class component’s Lifecycle Methods                                                       | Functional conponent |
| ----------------------------------------------------------------------------------------- | -------------------- |
| `constructor()` → `static getDrivedStateFromProps()` → `render()` → `componentDidMount()` | `useEffect( ,[])`    |

## 3. update(re-render)

: mount되어 이미 DOM에 존재하는 컴포넌트의

- props가 변경되거나,
- state가 변경되거나,
- 부모 컴포넌트가 리렌더링되거나,
- this.forceUpdate로 강제 렌더링 트리거 되면

컴포넌트를 호출해 새로운 instructions set을 받아오는것(렌더링 재차 함)

| Class component’s Lifecycle Methods                                                                                                | Functional conponent                                                                                                              |
| ---------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `static getDrivedStateFromProps()` → `shouldComponentUpdate()` → `render()` → `getSnapshotBeforeUpdate()` → `componentDidUpdate()` | `useEffect( , [값])` : 배열 안의 의존성 변수 중 하나라도 변경될 때마다 실행 / `useEffect( ,)` : 컴포넌트가 업데이트될 때마다 실행 |

## 4. unmount

: mount와 반대로, DOM에서 컴포넌트가 제거되는 것

| Class component’s Lifecycle Method | Functional conponent |
| ---------------------------------- | -------------------- |
| `componentWillUnmount()`           | `useEffect( ,[])`    |
