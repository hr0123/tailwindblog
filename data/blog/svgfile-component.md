---
title: 'svg파일 컴포넌트 생성해 사용하기'
date: '2022-09-22'
lastmod: '2022-09-22'
tags: ['svg', 'figma', 'svgr', 'svgr playground']
draft: false
# summary: ''
---

## 1. Figma : 원하는 이미지를 Example에서 svg형식으로 파일 저장

<Image src="/static/images/save-svgfile-on-figma.png" width="800" height="380"/>

## 2. [SVGR Playground](https://react-svgr.com/playground/) : svg파일을 TypeScript로 추출

1. 좌측에 TypeScript 체크박스 체크
2. Fimga에서 저장해온 svg파일을 'SVG INPUT' 부분에 drag&drop
3. 'SVG OUTPUT'에 뜬 컴포넌트 로직 전체 복사

## 3. VScode : 컴포넌트 생성

.tsx 파일 생성해 ➜ 복사해온 로직 붙여넣기
