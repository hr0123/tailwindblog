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
summary: 'HTML ํ์ ๊ธฐ๋ณธ'
---

# HTML [๐](https://developer.mozilla.org/ko/docs/Web/HTML)

<Image src="/static/images/htmltag.png" width="400" height="250" />
๋ธ๋ผ์ฐ์ ์์ ์คํ ๊ฐ๋ฅํ ๊ฐ์ฅ ๊ธฐ๋ณธ์ ์ธ ํ์ผ๋ก,  
๋งํฌ์ ์ธ์ด๋ก ๊ตฌ์กฐ์ ์ผ๋ก ํ๊ทธ๋ค์ ์ด์ฉํด์ ๋ณด์ฌ์ง๋ฉฐ,  
์์ํ๊ทธ๋ก `<head>`, `<body>`๊ฐ ์๋๋ฐ,  
`<head>`๋ ์์ธ ์ค๋ช(ํ์ด์ง์ ํ์๋๋ [meta data](https://developer.mozilla.org/ko/docs/Learn/HTML/Introduction_to_HTML/The_head_metadata_in_HTML)),  
`<body>`๋ ์ฌ์ฉ์์๊ฒ ๋ณด์ฌ์ง๋ ํ๊ทธ๋ค๋ก ๋์ด์๋ค

- `charset="utf-8"` : ํ์กดํ๋ ๋ชจ๋  ์ฌ๋๋ค์ด ์ฐ๋ ์ธ์ด๋ฅผ ์ง์(๊ธฐ๋ณธ)
- title : ๋ธ๋ผ์ฐ์  ๊ฒ์ํ๊ฑฐ๋ ๋ถ๋งํฌ ์ค์  ์ ๋ณด์ฌ์ง๋ ์ ๋ชฉ

### Hyper Text Markup Language

- Hyper Text : ์น ํ์ด์ง๋ฅผ ๋ค๋ฅธ ํ์ด์ง๋ก ์ฐ๊ฒฐํ๋ ๋งํฌ(์น์ ๊ทผ๋ณธ ์์ฑ)(ex. ์๋ฃ ์๋ก๋)
- Markup Language : (ํ๋ก๊ทธ๋๋ฐ ์ธ์ด๋ ์๋๊ณ ) ์นํ์ด์ง ๊ตฌ์กฐํ๊ฐ ์ด๋ป๊ฒ ๋์ด์๋์ง๋ฅผ ๋ธ๋ผ์ฐ์ ์๊ฒ ์๋ ค์ฃผ๋ ๋งํฌ์ ์ธ์ด

### W3C(World Wide Web Consortium)

- ์ฌ๋ฌ ๊ต์ก๊ธฐ๊ด๊ณผ Microsoft์ฌ์ ๊ฐ์ ๋ค์ํ ๊ธฐ์๋ค์ด ๋ชจ์ฌ ์น์ ํ์คํ๋ฅผ ์ถ์ง
- chrome, Safari ๋ฑ ๋ชจ๋  ๋ธ๋ผ์ฐ์ ๋ค์ด ํ์ค์ ๋ง๊ฒ ๋ธ๋ผ์ฐ์ ๋ฅผ ๊ตฌํํด์ผํ๊ธฐ ๋๋ฌธ

### vlidation

- validator website ๊ฐ์ ํ์ธ ๊ฐ๋ฅ
- ์ค๋ฅ๊ฐ ์์ด๋ ๋ธ๋ผ์ฐ์ ๊ฐ ์์์ ์ฒ๋ฆฌํ๊ธฐ ๋๋ฌธ์ ๊ฑฑ์  ์ํด๋๋จ

---

# Page structure [๐](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Document_and_website_structure)

#### ๋ฐ์ค๋ชจ๋ธ๋ก ์๊ฐํ๊ธฐ(React ์ฌ์ฉ์ ํ์)

<Image src="/static/images/htmlstructure1.png" width="300" height="170"/>
<Image src="/static/images/htmlstructure2.png" width="300" height="170"/>
<Image src="/static/images/htmlstructure3.png" width="300" height="170"/>

---

# HTML Tag ๊ตฌ์ฑ

## 1. Element(=node)

`<ํ๊ทธ์ด๋ฆ></ํ๊ทธ์ด๋ฆ>` : HTML์ ๊ตฌ์ฑํ๋ ๋งํฌ์ ๋๊ตฌ, JavaScript DOM์ ์ฝ์๋๊ณ  ๊ตฌ์ฑ์ด ์ด๋ค์ง
<Image src="/static/images/htmlelement.png" width="300" height="90"/>

#### Empty element : ๋ซ๋ ํ๊ทธ ๋ถํ์

```html
<img src="" />
```

## 2. Attribute

`< ... ์์ฑ์ด๋ฆ="์์ฑ๋ด์ฉ" >` : ์์๋ฐ์ดํ, ํฐ๋ฐ์ดํ ๋ชจ๋ ๊ฐ๋ฅ
<Image src="/static/images/htmlattribute.png" width="400" height="50"/>

#### Boolean Attribute

```html
<input type="text" disabled="disabled" />
```

```html
<input type="text" disabled />
```

โ ๊ฒฐ๊ณผ : <input type="text" disabled />

---

# HTML Tag ์ข๋ฅ [๐](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)

## 1. BOX : ๊ตฌ์กฐ๋ฅผ ๋๋๋ tag๋ค

`<header>`, `<footer>`, `<nav>`, `<section>`, `<article>`(๋ฐ๋ณต๋๋, ์ฌ์ฌ์ฉ ๊ฐ๋ฅํ ๊ฒ๋ค์ ๋ฌถ์ด๋์ ๊ฒ) ๋ฑ

## 2. ITEM(Semantic Tags) : ์ฌ์ฉ์์๊ฒ ๋ณด์ฌ์ง๋ / ๋ชฉ์ , ์ญํ , ํจ๊ณผ๋ฅผ ๊ฐ๋ tag๋ค

`<a>`, `<button>`, `<input>`, `<label>`, `<table>` ๋ฑ

<Image src="/static/images/htmlboxvsitem.png" width="500" height="300" />

---

### Inline VS Block element

<Image src="/static/images/htmlinlinevsblock.png" width="500" height="230" />

- `<span>` : Inline element
- `<div>` : Block element -> ํ ์ค ์ฐจ์ง(ํ ์ค์ ํ๋)

### (link)a

<Image src="/static/images/htmla.png" width="500" height="230" />

- `href` : url
- `target` : \_blanck๋ก ํ๋ฉด ์ ํญ์์ ์ด๋ฆผ(์๋ตํ๋ฉด ํ์ฌ ํญ์์)
- `title` : ๋ง์ฐ์ค hoverํ์ ๋ ๋จ๋ ๋ด์ฉ

### ol / ul / li

<Image src="/static/images/htmlolul.png" width="500" height="320" />

### input & label

<Image src="/static/images/htmlinput.png" width="560" height="200" />

---

# SEO

[๐](https://www.notion.so/hrcodelog/React-Next-js-001f52da15ac4e409d6da15b450912ef#37213a4df4364b9383ad010f51b2ab6f)

---

# Accessibility ๋์ด๋ ค๋ฉด ์ด๋ป๊ฒ ํด์ผํ๋์ง
