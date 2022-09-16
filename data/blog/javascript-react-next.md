---
title: 'JavaScript, React, NextJS 사용 이유'
date: '2022-09-15'
tags: ['JavaScript', 'React', 'NextJS']
draft: false
---

## JavaScript 사용 이유

HTML 문서에, 웹사이트상에서 동적 상호작용성(ex. 게임, 버튼이 눌리거나 폼에 자료가 입력될 때 반응, 동적인 스타일링과 애니메이션 등)을 더해주기 위해

## React 사용 이유(JavaScript 라이브러리)

#### JavaScript의 한계 1 : 실시간으로 많은 유저의 인터랙션이 일어나는 서비스들이 생겨나면서 ⇒ 화면 깜빡임 없고 부드럽게 잘 동작하는 웹사이트 개발이 필요해짐

-> React : SPA(Single Page Application)의 CSR(Client Side Rendering)

- SPA :
- CSR :

#### JavaScript의 한계 2 : 한 페이지에 해당하는 용량이 커져 ⇒ 기존 방식으로 매번 새로운 페이지를 전달하는게 버거워짐

-> React : 초반에 표시되는 index.html 파일 외에 HTML 문서는 없고, index.html 파일의 내용을 JS를 이용해 재렌더링 해주는 방식으로 페이지를 구성하므로,
페이지 별로 파일을 구성하는게 아닌, 표시해줄 내용 각각을 컴포넌트 형식으로 구성

## NextJS 사용 이유(React기반 JavaScript 프레임워크)

#### React의 한계 : CSR은 첫 로딩 속도 느림, SEO 어려움

-> NextJS : 처음 페이지 접속 등 초기 렌더링 시에는 SSR + 이후 페이지 이동 시에는 CSR

- SSR :
- SSG :
