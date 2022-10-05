---
title: 'Scroll interaction 라이브러리'
date: '2022-09-27'
tags: ['fade effect', 'aos']
draft: false
summary: 'AOS 사용해, fade effect 주기'
---

랜딩페이지 작업하면서 스크롤 인터랙션 잘 주고 싶었는데, 찾아보다가 생각했던 것보다 간단하게 구현 가능한 방법을 찾아서 적용했다.  
다른 방법도 있을 수 있지만, 다양한 인터랙션을 손쉽게 구현 가능해 다음에도 참고할 수 있도록 기록한다.

[🔗출처: 예시 및 설명](https://michalsnik.github.io/aos/)

---

# 1. 설치

```
yarn add aos
```

---

# 2. 코드

## 최상위 Container

- 설치한 AOS를 import
- useEffect 사용해, 얼마의 시간동안 일어나게 할건지 지속시간 설정

```js
import React, { useEffect } from 'react'
import AOS from 'aos'
import 'aos/dist/aos.css'

const Home: NextPage = () => {
  useEffect(() => {
    AOS.init({
      duration: 1000,
    })
  })

  return (
    <>
      <HeroContainer />
      <ProblemContainer />
      <SolutionContainer />
      <StrengthContainer />
      <MeritContainer />
      <ClientListContainer />
      <EndingContainer />
    </>
  )
}

export default Home
```

## 각 컴포넌트의 Presenter

- 원하는 방식의 인터랙션을([예시](https://michalsnik.github.io/aos/) 참고) 가장 바깥 태그에 속성으로 설정

```js
import { Wrapper } from './Styles'

export const Problem = () => {
  return <Wrapper data-aos="fade-up">... </Wrapper>
}
```
