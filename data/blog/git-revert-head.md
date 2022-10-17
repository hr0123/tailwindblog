---
title: 'git revert 후, detached HEAD 해결'
date: '2022-10-17'
tags: [git revert, HEAD, branch]
draft: false
summary: 'git revert(특정 commit으로 되돌리기) 후, branch "HEAD detached from ..." 해결'
---

## ① 특정 commit 상태로 되돌려야 하는 상황 발생

```js
git revert ff67b96424a123454cfe62ce3313a8e290561592
```

---

## ② 그 후 작업 중, branch가 master가 아닌 ff67b96로 떠있는 것을 발견(이미 push 여러 번 한 상태)

➜ branch 확인 :

```js
git branch
```

➜ 결과 :

```js
HEAD detached from ff67b96
```

➜ 원인 :  
HEAD가 원래는 master branch를 가리킨 다음 commit hash를 가리키는 순서인데,  
revert commit 했을 때, 중간 단계(branch)를 생략하고, revert한 hash를 바로 가리키는 것으로 변경됐던 것!  
근데 못 알아채고 그 이후로도 `git push origin master` 해오고있었던 것이다.  
🔗[git HEAD 개념](http://sunphiz.me/wp/archives/2266)

---

## ③ 임시 branch 이용해 해결

🔗[참고](https://aroma-dev.tistory.com/m/4)

1. 임시 temp branch 생성 후 이동

```js
git branch temp
git checkout temp
```

2. master branch와 temp branch를 강제 merge(병합)

```js
git branch -f master temp
```

3. master branch로 이동

```js
git checkout master
```

4. `Switched to branch 'master'. commit 3~4건 있으니 pull받아라.`

```js
git pull origin master
```

5. conflict 확인해, push할 코드들로 최신화

```js
git add .
git commit
git push origin master
```

6. temp branch 삭제

```js
git branch -d temp
```
