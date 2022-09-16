---
title: 'HTML'
date: '2022-09-16'
tags: ['HTML', 'HTML Tag', 'Page Stucture', 'Semantic Tag', 'SEO', 'Accessibility']
draft: false
summary: 'HTML 필수 기본'
---

# [Hyper Text Markup Language](https://developer.mozilla.org/ko/docs/Web/HTML)

- Hyper Text : 웹 페이지를 다른 페이지로 연결하는 링크(웹의 근본 속성)(ex. 자료 업로드)
- Markup Language : (프로그래밍 언어는 아니고) 웹페이지 구조화가 어떻게 되어있는지를 브라우저에게 알려주는 마크업 언어

---

# HTML Tags

1. Element `<태그이름></태그이름>` : HTML을 구성하는 마크업 도구
2. Attribute `< ... 속성이름="속성내용" >` (작은따옴표, 큰따옴표 모두 가능)

## Block element

```html
<p>one</p>
<p>two</p>
<p>three</p>
```

➜ 결과

<p>one</p>
<p>two</p>
<p>three</p>

## Inline element

```html
<em>one</em><em>two</em><em>three</em>
```

➜ 결과  
<em>one</em><em>two</em><em>three</em>

## Empty element(닫는 태그 불필요)

```html
<img src="" />
```

## link

```html
<p>
  A link to
  <a href="https://www.google.co.kr" title="google" target="_blank"> my favorite website </a>.
</p>
```

- href : url
- title : 마우스 hover했을 때 뜨는 내용
- target : \_blanck로 하면 새 탭에서 열림(생략하면 현재 탭에서)

➜ 결과 : <p>A link to <a href="https://www.google.co.kr" title="google" target="_blank">my favorite website</a>.</p>

## Boolean Attribute

```html
<input type="text" disabled="disabled" />
```

```html
<input type="text" disabled />
```

➜ 결과 : <input type="text" disabled />

## Meta Data [🔗](https://developer.mozilla.org/ko/docs/Learn/HTML/Introduction_to_HTML/The_head_metadata_in_HTML)

---

# Page Structure

---

# Semantic Tags

#### 목적, 역할, 효과를 갖는 태그(↔︎ `<div>` `<span>`)

- `<h1>`

---

# SEO

---

# Accessibility 높이려면 어떻게 해야하는지
