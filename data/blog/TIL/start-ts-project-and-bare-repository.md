---
title: 'TypeScript 프로젝트와 bare repository 연결'
date: '2022-09-14'
tags: ['typescript', 'git', 'repository', 'bare repository']
draft: false
# summary: 'TypeScript 프로젝트 생성하는 git 절차 | 서버에 bare repository 생성해 프로젝트와 연결'
---

## 1. iTerm2) TypeScript 프로젝트 및 bare repository 생성 후, 연결

```javascript
mkdir 폴더명 //ex) typescript-study
cd typescript-study
git init //git을 먼저 만드는 이유는 repository 연결 위함
cd .git
cat config
```

⇨ 결과: [bare = false](https://git-scm.com/docs/git-config#Documentation/git-config.txt-corebare)

```javascript
//서버에 bare repository 생성
//HOME(/Users) 가서
git init --bare BareRepository이름 //ex) gitbare
```

⇨ 결과: `Initialized empty Git repository in /Users/leehaeri/gitbare/`

```javascript
//프로젝트 생성한거를 bare repository와 연결
cd typescript-study
git remote add origin /Users/leehaeri/gitbare/
git remote -v
```

⇨ 결과:  
`origin /Users/leehaeri/gitbare/ (fetch)`  
`origin /Users/leehaeri/gitbare/ (push)`

```javascript
vi README.md //or code . 후 파일 생성 ➜ 내용 작성
git add .
git commit -m “ ”
git push origin master
```

---

## 2. iTerm2) 서버에 생성된 bare repository 설정

```javascript
// /Users/leehaeri로 가서
cd gitbare
cat config
cat HEAD
```

⇨ 결과: `ref: refs/heads/master`

```javascript
cd refs // /Users/leehaeri/gitbare/refs
cd heads // /Users/leehaeri/gitbare/refs/heads
cat master
```

⇨ 결과: _hash_(= gitbare를 연결해둔 `typescript-study`폴더에서 방금 커밋한 _hash_)

```javascript
// /Users/leehaeri/gitbare/hooks 가서
vi post-receive
```

⇨ 결과: `#!/bin/bash`

```javascript
// HOME(/Users) 가서
which bash
```

⇨ 결과: `/bin/bash` (bash : 리눅스의 커널이 갖고있는 쉘 중 하나)(sh : 리눅스 커널 기본 쉘)

```javascript
sh --version
```

---

## 3. VSCode) TypeScript 프로젝트 설정

```javascript
//폴더 'typescript-study'에서
npm init -y
```

⇨ 결과: package.json파일 생김

```javascript
cat package.json
```

⇨ 결과:
<Image src="/static/images/bareRepo1.png" width={400} height={320}/>

```javascript
//타입스크립트 설치
yarn add -D typescript ts-node ts-node-dev @types/node
cat package.json
```

⇨ 결과:
<Image src="/static/images/bareRepo2.png" width={400} height={500}/>

```javascript
code .
```

⇨ 결과: VSCode에서 'typescript-study'폴더 열림

```javascript
npx gitignore node
```

⇨ 결과: `.gitingore` 파일 생김(`node_modules` 등 Git에 관리 안되게끔)

```javascript
git add .
git commit -m “ ”
```

```javascript
npx tsc --init
```

⇨ 결과: `tsconfig.json` 파일(compile옵션) 생김

```javascript
//package.json파일에서
//scripts: { ...,
    "build": “tsc” //작성
//}
```

```javascript
//src폴더 생성 ➜ 안에 index.ts파일 생성
export {} //작성
```

```javascript
yarn build
```

⇨ 결과: src폴더 안에 index.js파일 생김 ⇨ 삭제

```javascript
//tsconfig.json에서
“ourDir” : “./build” //주석 풀고 작성
```

```javascript
yarn build
```

⇨ 결과: `build`폴더 생기고 그 안에 index.js파일 생김
