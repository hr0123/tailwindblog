---
title: '[TypeScript] Type 부분 적용하기(children 중복 에러 해결)'
date: '2022-09-30'
tags: ['typescript', 'omit']
draft: false
# summary: ''
---

# 에러 메세지

Navigation bar에 Material UI의 Appbar를 적용하는 과정에서 아래 에러 메세지가 떴다.

```
(alias) const NavBar: (props: Props) => JSX.Element
import NavBar

Property 'children' is missing in type '{}' but required in type 'Props'.ts(2741)

NavBar.tsx(17, 3): 'children' is declared here.
```

---

# 원인

`<HideOnScroll/>`은 이미 children요소`<AppBar>….</AppBar>`를 갖고 있는데, 내려받은 `Props`에도 `children`이 있어 충돌되어 발생한 에러

---

# 해결

`Props`를 prop내려줄 때 `children`은 제외

```js
import AppBar from '@mui/material/AppBar'
import Toolbar from '@mui/material/Toolbar'
import useScrollTrigger from '@mui/material/useScrollTrigger'
import Slide from '@mui/material/Slide'

interface Props {
  window?: () => Window;
  children: React.ReactElement;
}

function HideOnScroll(props: Props) {
  const { children, window } = props
  const trigger = useScrollTrigger({
    target: window ? window() : undefined,
  })

  return (
    <Slide appear={false} direction="down" in={!trigger}>
      {children}
    </Slide>
  )
}

export const NavBar = (props: Omit<Props, 'children'>) => {
  const router = useRouter()

  return (
    <>
      <HideOnScroll {...props}>
        <AppBar>
          <Toolbar>
            <Wrap></Wrap>// AppBar에 넣을 요소
          </Toolbar>
        </AppBar>
      </HideOnScroll>
      <Toolbar />
    </>
  )
}
```
