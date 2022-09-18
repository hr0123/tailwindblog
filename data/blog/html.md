---
title: 'HTML'
date: '2022-09-16'
lastmod: '2022-09-18'
tags:
  [
    'HTML',
    'W3C',
    'Page Stucture',
    'Element',
    'Attribute',
    'HTML Tags',
    'Semantic Tag',
    'SEO',
    'Accessibility',
  ]
draft: false
summary: 'HTML 필수 기본'
---

# HTML [🔗](https://developer.mozilla.org/ko/docs/Web/HTML)

<Image src="/static/images/htmltag.png" width="400" height="250" />
브라우저에서 실행 가능한 가장 기본적인 파일로,  
마크업 언어로 구조적으로 태그들을 이용해서 보여지며,  
상위태그로 `<head>`, `<body>`가 있는데,  
`<head>`는 상세 설명(페이지에 표시되는 [meta data](https://developer.mozilla.org/ko/docs/Learn/HTML/Introduction_to_HTML/The_head_metadata_in_HTML)),  
`<body>`는 사용자에게 보여지는 태그들로 되어있다

- `charset="utf-8"` : 현존하는 모든 사람들이 쓰는 언어를 지원(기본)
- title : 브라우저 검색하거나 북마크 설정 시 보여지는 제목

### Hyper Text Markup Language

- Hyper Text : 웹 페이지를 다른 페이지로 연결하는 링크(웹의 근본 속성)(ex. 자료 업로드)
- Markup Language : (프로그래밍 언어는 아니고) 웹페이지 구조화가 어떻게 되어있는지를 브라우저에게 알려주는 마크업 언어

### W3C(World Wide Web Consortium)

- 여러 교육기관과 Microsoft사와 같은 다양한 기업들이 모여 웹의 표준화를 추진
- chrome, Safari 등 모든 브라우저들이 표준에 맞게 브라우저를 구현해야하기 때문

### vlidation

- validator website 가서 확인 가능
- 오류가 있어도 브라우저가 알아서 처리하기 때문에 걱정 안해도됨

---

# Page structure [🔗](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Document_and_website_structure)

#### 박스모델로 생각하기(React 사용에 필수)

<Image src="/static/images/htmlstructure1.png" width="300" height="170"/>
<Image src="/static/images/htmlstructure2.png" width="300" height="170"/>
<Image src="/static/images/htmlstructure3.png" width="300" height="170"/>

---

# HTML Tag 구성

## 1. Element(=node)

`<태그이름></태그이름>` : HTML을 구성하는 마크업 도구, JavaScript DOM에 삽입되고 구성이 이뤄짐
<Image src="/static/images/htmlelement.png" width="300" height="90"/>

#### Empty element : 닫는 태그 불필요

```html
<img src="" />
```

## 2. Attribute

`< ... 속성이름="속성내용" >` : 작은따옴표, 큰따옴표 모두 가능
<Image src="/static/images/htmlattribute.png" width="400" height="50"/>

#### Boolean Attribute

```html
<input type="text" disabled="disabled" />
```

```html
<input type="text" disabled />
```

➜ 결과 : <input type="text" disabled />

---

# HTML Tag 종류 [🔗](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)

## 1. BOX : 구조를 나누는 tag들

`<header>`, `<footer>`, `<nav>`, `<section>`, `<article>`(반복되는, 재사용 가능한 것들을 묶어놓은 것) 등

## 2. ITEM(Semantic Tags) : 사용자에게 보여지는 / 목적, 역할, 효과를 갖는 tag들

`<a>`, `<button>`, `<input>`, `<label>`, `<table>` 등

<Image src="/static/images/htmlboxvsitem.png" width="500" height="300" />

---

### Inline VS Block element

<Image src="/static/images/htmlinlinevsblock.png" width="500" height="230" />

- `<span>` : Inline element
- `<div>` : Block element -> 한 줄 차지(한 줄에 하나)

### (link)a

<Image src="/static/images/htmla.png" width="500" height="230" />

- `href` : url
- `target` : \_blanck로 하면 새 탭에서 열림(생략하면 현재 탭에서)
- `title` : 마우스 hover했을 때 뜨는 내용

### ol / ul / li

<Image src="/static/images/htmlolul.png" width="500" height="320" />

### input & label

<Image src="/static/images/htmlinput.png" width="560" height="200" />

---

# SEO

[🔗](https://www.notion.so/hrcodelog/React-Next-js-001f52da15ac4e409d6da15b450912ef#37213a4df4364b9383ad010f51b2ab6f)

---

# Accessibility 높이려면 어떻게 해야하는지
