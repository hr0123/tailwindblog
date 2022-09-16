---
name: Lee Haeri
avatar: /static/images/avatar.png
occupation: FrontEnd Developer
company: ChangSoft I&I
email: sallygofl@gmail.com
# twitter: https://twitter.com/Twitter
# linkedin: https://www.linkedin.com
github: https://github.com/hr0123
---

# [STUDY PLAN](https://www.youtube.com/watch?v=TTLHd3IyErM)

📌 개념 내용 알려면 Docs 읽기(남이 정리한거는 읽지말기)  
📌 각각의 개념을, 레파지토리 생성해 프로젝트 제작하는 것을 통해 학습  
📌 copy&paste 절대X! 코드 하나하나 직접 입력해가며!  
📌 프로젝트 제작한 내용을 블로그(tailwind)에 기록  
📌 공부하면서, 하루동안 등등 느낀거, 생각한거, 궁금한거 등등 주절주절 블로그에 기록

### 1. `220916F` HTML(전부 암기 아닌, 전체 흐름 이해 ⇨ 추후 찾아가며 개발)

- HTML Tags 어떤 것들이 있고 어떻게 사용되는지
- Page Structure 어떻게 구성할지
- Semantic Tags 어떤 것들이 있고 어떻게 사용되는지
- SEO 높이려면 어떻게 해야하는지
- Accessibility 높이려면 어떻게 해야하는지

### 2. `220916F` CSS(전부 암기 아닌, 전체 흐름 이해 ⇨ 추후 찾아가며 개발)

- Styling
- Layouts
- Responsive Design
- Animation
- `220921W` JavaScript(아래) 학습 후
  - Architecture : BEM(CSS Framework 사용하게 되면 불필요하지만, 어떻게 Class이름 설정하는지 원리 이해 위해)
  - Preprocessors : Sass, Less, PostCSS
  - CSS Framework : Bootstrap, PostCSS, Tailwind CSS, Material UI, Styled-Components

### 3. `220917A` JavaScript

- **ES6 + Syntax : 문법은 첫번째로 익혀야하는 가장 중요한 것**
  - Basic : let, const / if, for, switch, while / function / object
  - Advanced : Prototype / Hoisting / Scope / Closure
- **Browser APIs**
  - DOM Manipulation
  - Events
  - Fetch API(Async)
  - (Vanilla JavaScript, Window Web API, Document(DOM Web API))

### 4. `220918U` TypeScript

- Types
- OOP(객체지향)

<Image src="/static/images/js-ts-diagram.png" width="300" height="230"/>

### 5. `220919M` JavaScript Framework

- React : 무엇때문에 사용하는지 이해하면, 다른 Framework 이해도 잘 될 것
- Vue
- Angular
- Svelte : 신규

### 6. `220919M` JS+TS+Framework=SPA이므로 발생하는 한계(CSR, SEO) 보완

#### 1) SSG

- Gatsby(React)
- GridSome(Vue)
- 11ty(JS)

#### 2) SSR

- Next.js(React)
- Nuxt.js(Vue)
- Universal(Angular)

### 7. `220922H` Tools

- Version Control System : Git
  - GitHub / Bitbucket / GitLab
- Package Manager : **npm** / yarn
- Module Bundler : Webpack / Rollup / Parcel (Framework로 제공받는 기능이지만 원리 숙지 필요)

### 8. Testing : 배포 전 테스트

- Test Pyramid : Jest / Cypress / Enzyme / react-testing-library
- Good Test Principles
- CI / CD

### 9. Publish : 배포(달달 암기 아닌, 실제 배포해보는 경험)

- **Github Pages** / Netlify / Vercel / Heroku / AWS / Azure
