---
title: 'Hoisting, Scope | var VS let VS const'
date: '2022-09-22'
lastmod: '2022-09-22'
tags: ['hoisting', 'scope', 'var', 'let', 'const', 'es6']
draft: false
# summary: ''
---

|                                           | var                              | let                                       | const                                     |
| ----------------------------------------- | -------------------------------- | ----------------------------------------- | ----------------------------------------- |
| Global Scope에서 선언한 전역변수          | 로직 안/밖 모든 곳에서 참조 가능 | 로직 안/밖 모든 곳에서 참조 가능          | 로직 안/밖 모든 곳에서 참조 가능          |
| Local(Block) Scope에서 선언한 지역변수    | 로직 안/밖 모든 곳에서 참조 가능 | 해당 로직 안에서만 참조 가능              | 해당 로직 안에서만 참조 가능              |
| Local(Function) Scope에서 선언한 지역변수 | 해당 로직 안에서만 참조 가능     | 해당 로직 안에서만 참조 가능              | 해당 로직 안에서만 참조 가능              |
| 동일한 이름의 변수를 다시 선언+할당       | 가능                             | 불가능                                    | 불가능                                    |
| 변수를 선언+할당 후 할당만 다시해 값 수정 | 가능                             | 가능(따라서, 선언 시 할당 같이 안해도 됨) | 불가능(따라서, 선언 시 할당 같이 해야 함) |

---

# Hoisting

JavaScript는 로직 실행 전에 먼저, 선언된 변수들이 어떤게 있는지 먼저 쭉 확인해 메모리에 저장하는데, 이로써 변수들을 범위의 최상단으로 끌어올리는 것이 된다. 이것을 hoisting이라고 함

---

# Scope

선언한 변수를 참조(접근해 사용) 가능한 범위(영역,위치)

## Global vs Local(Function / Block-`var vs let,const`)

### [1] Global Scope에서 선언 (=전역변수)

이 위치에서 선언된 변수는 로직(for/if문이나 함수) 안/밖 등 모든 곳에서 참조(approach해 가져다가 사용)할 수 있는데,

1. let/const로 선언한 변수는 : 선언 위치가 로직 밖인 경우이고
2. var로 선언한 변수의 경우 : 선언 위치가 (1)로직 밖인 경우와 (2)Local Scope 중 Block인 경우가 해당한다

### [2] Local Scope에서 선언 (=지역변수)

- Function Scope(함수 내 지역변수) : 함수 중괄호 안 영역으로
  - 이 위치에서 var/let/const로 선언된 변수는 해당 함수 중괄호 안에서만 참조 가능
- Block Scope(for/if문 등 내 지역변수) : for/if문 등 로직 중괄호 안 영역
  1. 이 위치에서 var로 선언한 변수는 : Global Scope가 되어버려, 해당 로직의 안/밖 모든 곳에서 참조 가능
  2. 이 위치에서 let/const로 선언한 변수는 : 해당 로직의 중괄호 안에서만 참조 가능

```javascript
var globalVar = 20
let globalLet = 'haeri'

if (true) {
  console.log(globalVar) //20 : 전역변수는 로직 안/밖 모두에서 참조 가능
  var globalVar = 40
  var blockVar = -1
  console.log(globalLet) //"haeri" : 전역변수는 로직 안/밖 모두에서 참조 가능
  let blockLet = 'potter'
  console.log(blockLet) //"potter" : let으로 선언한 지역변수는 해당 중괄호 안에서만 참조 가능
}

console.log(globalVar) //40 : 전역변수는 로직 안/밖 모두에서 참조 가능 + var는 선언+할당 후, 동일한 이름의 변수를 또 var로 선언+할당 시 -> 에러 안나고 값이 갱신됨
console.log(blockVar) //-1 : var로 선언한 (지역변수 중)Block Scope에서 선언한 변수는 해당 Block 밖에서도 참조 가능
console.log(globalLet) //"haeri" : 전역변수는 로직 안/밖 모두에서 참조 가능
console.log(blockLet) //error : let으로 선언한 지역변수는 해당 중괄호 밖에서는 참조 불가

function test() {
  console.log(globalVar) //40 : 전역변수는 로직 안/밖 모두에서 참조 가능 + var는 선언+할당 후, 동일한 이름의 변수를 또 var로 선언+할당 시 -> 에러 안나고 값이 갱신됨
  console.log(blockVar) //-1 : var로 선언한 (지역변수 중) Block Scope에서 선언한 변수는 해당 Block 밖에서도 참조 가능
  var funcVar = 999
  console.log(funcVar) //999 : 지역변수 중 Function Scope에서 선언한 변수는 해당 로직 안에서만 참조 가능
  console.log(globalLet) //"haeri" : 전역변수는 로직 안/밖 모두에서 참조 가능
  console.log(blockLet) //error : let,const로 선언한 지역변수(Block, Function 모두)는 해당 로직 안에서만 참조 가능
  let funcLet = 'chang'
  console.log(funcLet) //"chang" : let,const로 선언한 지역변수(Block, Function 모두)는 해당 로직 안에서만 참조 가능
}

console.log(funcVar) //undefined or error : var로 선언한 (지역변수 중)Function Scope에서 선언한 변수는 해당 Function 밖에서는 참조 불가
console.log(funcLet) //error : let,const로 선언한 지역변수(Block, Function 모두)는 해당 로직 안에서만 참조 가능
```

---

# var

1. Global Scope에서 var로 선언한 변수(전역변수)는 : 로직 안/밖 모든 곳에서 참조(접근해 가져다가 사용) 가능
2. Local Scope 중 Block Scope에서 var로 선언한 변수(지역변수)도 : 로직 안/밖 모두에서 참조 가능
3. Local Scope 중 Funciton Scope에서 var로 선언한 변수(지역변수)는 : 해당 함수 안에서만 참조 가능 -> 밖에서 사용 시 undefined(? or error?)

---

# let, const

1. Gloval Scope에서 let/const로 선언한 변수(저역변수)는 : 로직 안/밖 모든 곳에서 참조 가능
2. Local Scope(Block, Function 모두)에서 선언한 변수(지역변수)는 : 해당 로직 중괄호 안에서만 참조 가능 -> 밖에서 사용 시 error 발생

### ES6(2015)에서 var 문제점을 보완 위해 등장 : let/const로 변수를 선언하면, var로 선언했을때에 비해

- 코드가 어떻게 작동할지 직관적으로 예측하기 더 용이해지고
- for문, if문 등의 반환값을 더 정확하게 전달 혹은 반환 가능해진다
- 그리고 let을 사용해 TDZ 개념을 작동시켜야하는 이유는 JavaScript가 동적 언어여서 runtime type check가 필요하기 때문이다

### let과 const의 차이점은

#### 1. let으로 선언하는 변수는 mutable :

- 변수를 let으로 선언+할당 후에 → 동일한 이름의 변수를 다시 let으로 선언+할당 하는 것은 불가능하지만,
- 해당 변수에 할당만 다시 해 값을 수정하는 것은 가능
- ⇨ 그래서 선언만 하고 후에 할당은 따로 가능

#### 2. const로 선언하는 변수는 immutable :

- 변수를 const로 선언+할당 후에 → 동일한 이름의 변수를 다시 const로 선언+할당 하는 것도 불가능하고,
- 할당만 다시 하는 것도 불가능
- ⇨ 그래서 선언 시 할당도 같이 해야 함
