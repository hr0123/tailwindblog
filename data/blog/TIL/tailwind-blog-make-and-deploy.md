---
title: 'Tailwind 블로그 & TailwindCSS'
date: '2022-09-13'
tags: ['tailwind', 'clone', 'git', 'deploy', 'Vercel']
draft: false
summary: 'Tailwind 블로그 생성 / git clone 후 첫 push(오류 해결) / TailwindCSS 장단점 / inline style과의 차별점'
---

# Tailwind 블로그 생성

## 1. 내 계정에 repository 생성 후 clone

① https://github.com/timlrx/tailwind-nextjs-starter-blog -> 'Use this template' -> `git clone URL`  
② `README.md` 보면서 커스텀 [참고](https://cheesepaninim.vercel.app/blog/develop/blog/init-03)

## 2. clone 후 첫 push

```
git add .
git commit -m "feat(layout): 블로그 생성"
git push origin master
```

했더니, 아래 내용의 error가 떴다

  <div className="my-1 px-2 w-full overflow-hidden xl:my-1 xl:px-2 xl:w-1/2">
    ![Maple](/static/images/git-first-push-error.png)
  </div>

### 원인

clone을 https로 해서, remote가 https이기 때문

### 해결방법

① ssh를 복사해서

  <div className="my-1 px-2 w-full overflow-hidden xl:my-1 xl:px-2 xl:w-1/2">
    ![Maple](/static/images/git-ssh.png)
  </div>
② github 설정 가서, 붙여넣기
  <div className="my-1 px-2 w-full overflow-hidden xl:my-1 xl:px-2 xl:w-1/2">
    ![Maple](/static/images/git-ssh-github.png)
  </div>
③ https로 되어있는 origin을 지우고 ➜ GitHub에서 SSH 복사해, `remote add origin 붙여넣기` ➜ `push`
  <div className="my-1 px-2 w-full overflow-hidden xl:my-1 xl:px-2 xl:w-1/2">
    ![Maple](/static/images/git-clone-ssh.png)
  </div>
  <div className="my-1 px-2 w-full overflow-hidden xl:my-1 xl:px-2 xl:w-1/2">
    ![Maple](/static/images/git-fix.png)
  </div>

## 3. 배포

https://vercel.com/ -> login(GitHub) -> 이름 설정  
➜ [배포 완료](https://vercel.com/hr0123/haeri-blog)(도메인 : https://haeri-blog.vercel.app/)

---

# TailwindCSS 장점

#### 1. Utility-First(미리 세팅된 유틸리티 클래스를 활용하여 HTML 코드 내에서 스타일링)이어서, 쉽고 빠르게 원하는 디자인을 개발 가능

- 스타일 코드도 HTML 코드 안에 있기 때문에 HTML와 CSS 파일을 별도로 관리할 필요가 없다
- 원하는 태그의 스타일을 변경하기 위해 클래스명을 검색해가며 일일이 필요한 CSS 코드를 찾을 수고도 사라진다
- 랩핑 태그의 클래스명을 사용할 일이 거의 없으므로 `container`, `wrapper`, `inner-wrapper`와 같은 클래스명을 고민하지 않아도 된다

#### 2. 모든 곳에서 동일한 색상이나 사이즈, 간격 등의 유틸리티 클래스를 사용

- 일관된 스타일로 구현하기가 수월

#### 3. 다른 프레임워크들에 비해 기본 스타일 값을 디테일한 부분까지 쉽게 커스텀이 가능

- 기본 스타일 값을 수정하는 방식이기에 디자인 일관성도 해치지 않는다
- 덕분에 디자인 시스템이나 다크 모드 구현도 간편

#### 4. 로우 레벨의 스타일 제공

- 각 CSS 요소 수준의 유틸리티 클래스를 제공하기 때문에 세밀하게 원하는 디자인을 구현할 수 있다
- 거의 모든 스타일의 유틸리티 클래스를 학습해야 한다는 의미와 같다. 이러한 불편을 해소하기 위해 [Intelli Sense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss) 플러그인을 제공 : 미리보기, 자동완성, 신택스 하이라이팅, 린팅을 지원하기 때문에 조금만 익숙해지면 금방 문서 없이 개발할 수 있다

#### 5. JavaScript 코드와 완전히 분리되어 있다

- 프로젝트 진행 도중 JavaScript 프레임워크를 변경하여도 큰 추가 작업 없이 기존의 HTML 코드를 그대로 쓸 수 있다

---

# TailwindCSS 단점

#### 1. 초반에는 각 스타일의 클래스명을 익히느라 개발하는 내내 문서를 참고해야 하는 번거로움

그래도 대부분의 클래스명이 기존 CSS 속성이나 속성값과 비슷한 경우가 많고 자동완성을 지원하는 Intelli Sense 플러그인이 있어서 금방 익숙해지기는 한다

#### 2. JavaScript 코드 사용 불가

클래스명을 분기 처리하여 동적으로 스타일링을 설정할 수는 있지만 styled-components와 같이 JavaScript 변수 값에 따라 가로 길이를 설정하는 등의 구현은 가능하기는 하지만 무척 번거로운 설정이 필요(그러나, 이렇게 특정 변수값을 활용하여 스타일링을 하면 일관된 디자인을 해치는 경우가 많음)

#### 3. HTML와 CSS 코드 혼재

HTML와 CSS의 관심사 분리가 이루어지지 않았다

---

# inline style과의 차별점

#### 1. Designing with constraints

사전 정의된 스타일들 중에 선택해 사용하므로, 시각적으로 일관된 UI 구축에 용이하다.

> Using inline styles, every value is a magic number. With utilities, you’re choosing styles from a predefined [design system](https://tailwindcss.com/docs/theme), which makes it much easier to build visually consistent UIs.

#### 2. Responsive design

반응형 쉽게 구현 가능

> You can’t use media queries in inline styles, but you can use Tailwind’s [responsive utilities](https://tailwindcss.com/docs/responsive-design) to build fully responsive interfaces easily.

#### 3. Hover, focus, and other states

마우스 호버, 포커스 등 쉽게 구현 가능

> Inline styles can’t target states like hover or focus, but Tailwind’s [state variants](https://tailwindcss.com/docs/hover-focus-and-other-states) make it easy to style those states with utility classes.
