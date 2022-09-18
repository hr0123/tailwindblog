---
title: 'CSS'
date: '2022-09-18'
lastmod: '2022-09-18'
tags: ['css', 'css property', 'selector', 'display', 'position', 'flexbox']
draft: false
summary: 'CSS 필수 기본'
---

# Cascading Styling Sheet

- cascade : 위에서 아래로 계속해서 떨어지는 폭포

- 웹사이트 스타일링 세가지  
  : 브라우저 상에 기본적으로 작성된 styling을 정의한 기본 sheet이 있으면 그것을 쓰고 -> 없으면 다음 기본으로 지정된 것으로 넘어감

  ① Author style (=제공하는 CSS 파일)  
   ➜ ② User style(사용자가 지정한 브라우저 스타일)  
   ➜ ③ Browser : 브라우저 상에서 기본적으로 설정한 스타일

- `important` : cascade 무시하고 최우선으로 설정되도록 하는 것(되도록 사용않는게 좋음)

## CSS property

🔗 [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)  
🔗 [CanIuse](https://caniuse.com/) : 속성값의 브라우저별 지원 여부, 사용량

---

# Selector(선택자)

🔗 [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors) | [연습](https://flukeout.github.io/)

커다란 `<body>` 안에  
여러 섹션들을 나누고  
각 섹션 안에 박스들을 나눠 구조화하는 데 있어서,  
labeling을 잘 해야 CSS 할때 쉬움 -> selector

<Image src="/static/images/cssselector.png" width="750" height="400"/>

- `*` : Universal Selector
- `tag이름` : Type Selector
- `#id이름`
- `.class이름`
- `:state내용`
- `[attribute내용]`

---

# Display

🔗 [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/display)

Block`<div>` VS Inline`<span>`
<Image src="/static/images/cssdisplay.png" width="750" height="250"/>

---

# Position

🔗 [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/position)

- static
- relative
- absolute
- fixed

<Image src="/static/images/cssposition.png" width="750" height="300"/>

---

# Flex box (Layouts)

🔗 [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox) | [연습](https://flexboxfroggy.com/) | [+](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

\*[Float](https://developer.mozilla.org/en-US/docs/Web/CSS/float) : text와 image 간 배치 설정

## Container에 부여하는 속성값

- display
- flex-direction
- flex-wrap
- flex-flow
- justify-content
- align-items
- align-content

<Image src="/static/images/csscontainerdisplay.png" width="750" height="600"/>

## Item에 부여하는 속성값

- order
- flex-grow
- flex-shrink
- flex
- align-self

<Image src="/static/images/cssitemorder.png" width="750" height="400"/>
<Image src="/static/images/cssitemflexshrink1.png" width="750" height="280"/>
<Image src="/static/images/cssitemflexshrink2.png" width="750" height="280"/>
<Image src="/static/images/cssitemflexbasis.png" width="750" height="280"/>
<Image src="/static/images/cssflexandalignself.png" width="750" height="280"/>

---

# Responsive Design

---

# Animation
