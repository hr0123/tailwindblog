---
title: '동기/비동기 | Callback함수 | Promise | async await'
date: '2022-09-25'
lastmod: '2022-09-26'
tags:
  [
    'synchronous',
    'asynchronous',
    'callback',
    'promise',
    'async await',
    'promise.all',
    'promise.race',
  ]
draft: false
# summary: ''
---

# JavaScript의 동기/비동기

#### JavaScript는 코드를 동기적으로 실행한다(각 요청이 응답 완료되어야, 다음 로직 요청을 보냄) → 그래서 처리시간이 오래 소요되는 요청이 있을 경우, 사용자 화면에 UI가 렌더링되는 시간이 오래 걸리는 문제가 생긴다 → 따라서, 처리시간 오래 걸리는 heavy work들은 비동기 처리를 해줘야함(방법: 인자로 Callback함수를 받는: Promise, asymc await)

- JavaScript는 heavy work(network, read files 등)를 비동기적으로 실행 가능하므로, heavy work라 오래걸리는 작업 완료를 기다리지 않고도 다음 코드를 시작 가능하므로 효율적이다
- JavaScript는 hoisting(코드 실행에 앞서 일단, 선언된 변수와 함수들을 문서 최상단 순서로 끌어올려 요청들을 브라우저에 전달)한다  
  → 그 후, 응답 오는 것을 전부 기다렸다가 한꺼번에 실행하는 것(동기 Synchronous)이 아닌,
  각각 응답이 오는대로 그 응답을 실행한다(비동기 Asynchronous)

---

# Callback함수로 동기/비동기 이해하기

## 1. Callback함수

함수 안에서 함수를 전달해 실행시키기도 하는데 그 안쪽 함수를 Callback함수라고 하며, 겉함수보다 나중에 불려지는 순서라 ‘Callback’이라고 이름 붙여짐

## 2. 동기(synchronous) Callback함수 : ex) arr.find / arr.map / arr.filter

#### 배열 메서드 find `array.find(( predicate:()=>value, thisArg ))` : 함수 안에 위치한 함수(Callback함수)가 겉함수와 별개로 인자를 받아와 본인 로직에 사용 -> returns the value of the first element (in the array) where **predicate(Callback함수)** is true

1. calls **predicate`()=>value`(Callback함수)** once for each element of the array until it finds one where **predicate(Callback함수)** returns true
2. If such an element is found, immediately returns that element value

```js
'use strict'

class Movie {
  constructor(title, runningTime) {
    this.title = title
    this.runningTime = runningTime
  }
  introduce() {
    console.log(`The running time of ${this.title} is ${this.runningTime}.`)
  }
}

const movieArray = [
  new Movie('Iron Man', 160),
  new Movie('Captain America', 125),
  new Movie('Frozen', 100),
]

// const result = movieArray.find(function(value, index) {
//   // console.log(value, index);
//   return value.runningTime < 120;
// });
const result = movieArray.find((value) => value.runningTime < 120) //화살표함수로 표기 시, return문이 한문장이면 {return ... ;}생략 가능
console.log(result) //결과: Movie {title: 'Frozen', runningTime: 100}
```

## 3. 비동기(asynchronous) Callback함수

#### 함수가 순서대로 실행될 수 없는 것으로, 잘 보여주는 예로 setTimeout이라는 web API가 있다 : `setTimeout(function() { return }, #000ms)` -> #초 지난 시점에 Callback함수를 실행

```js
console.log('바로 뜸 1')

setTimeout(() => console.log('1초 뒤 실행되어 4번째로 뜸'), 1000)

console.log('바로 뜸 2')

// sync Callback
// 1. 함수 선언 : print라는 함수 인자를 받아와, 그 함수인자를 실행하는 로직 작성
const PrintImmediately = (print) => {
  print()
}
// 2. 함수 실행 : argumet(print) 자리에 함수
PrintImmediately(() => console.log('바로 뜸 3'))

// async Callback
// 1. 함수 선언 : print라는 함수 인자와 지연시간 인자를 받아와, web API setTimeout에 넣어 -> 그 시간만큼 지난 후 그 함수인자를 실행하는 로직 작성
const PrintWithDelay = (print, timeout) => {
  setTimeout(print, timeout)
}
// 2. 함수 실행 : argumet1(print) 자리에 함수, argument2(timeout)자리에 숫자
PrintWithDelay(() => console.log('2초 뒤 실행되어 5번째로 뜸'), 2000)
```

<Image src="/static/images/async-callback.png" width="200px" height="120px"/>

## 4. Callback Hell(Callback Chain)

```js
//class 사용해, 로그인 성공/실패 함수와 회원role 받아오는 함수 생성틀 각각 제작
class UserStorage {
  loginUser(id, password, onSuccess, onFail) {
    setTimeout(() => {
      if (
        (id === 'haeri@google.com' && password === '1234') ||
        (id === 'sally@google.com' && password === '0909')
      ) {
        onSuccess(id) //회원정보 일치해 로그인 성공 시, 함수onSuccess통해 id를 넘겨줌
      } else {
        onError(new Error('not found')) //회원정보 불일치해 로그인 실패 시, 에러 띄움
      }
    }, 2000)
  }

  getRole(user, onSuccess, onError) {
    setTimeout(() => {
      if (user === 'haeri@google.com') {
        onSuccess({ name: 'Haeri', role: 'admin' }) //로그인 성공한 회원 이름 확인해 맞으면, name과 role 반환
      } else if (user === 'sally@google.com') {
        onSuccess({ name: 'Sally', role: 'customer' })
      } else {
        onError(new Error('no access')) //틀리면, 에러 띄움
      }
    }, 1000)
  }
}

// Callback Hell
const user1 = new UserStorage()
const id = prompt('enter your id') //브라우저 API 사용해, 로그인하는 유저의 id와 password 받아오기
const password = prompt('enter your password')
user1.loginUser(
  id,
  password,
  // 1.로그인 성공 시 실행하는 함수(onSuccess)
  (user) => {
    user1.getRole(
      user,
      // 2.role받아오기 성공 시 실행하는 함수(onSuccess)
      (userWithRole) => {
        alert(`Hello ${userWithRole.name}, you have a ${userWithRole.role} role.`)
      },
      // 2.role받아오기 실패 시 실행하는 함수(onError)
      (error) => console.log(error)
    )
  },
  // 1.로그인 실패 시 실행하는 함수(onError)
  (error) => {
    console.log(error)
  }
)
```

#### 문제점 : 콜백함수 안에 또 콜백함수, 그 안에 또 콜백함수, 그 안에 또 콜백함수

- 코드 가독성이 떨어져, 연결관계 파악이 어려워 로직을 한눈에 알아보기 어렵다
- 디버깅하고 문제 분석하기 어렵다
- 유지보수 어렵다

---

# [Callback Hell 해결방법 1] Promise

## 1. Promise란

- 비동기 코드를 깔끔하게 작성하는 방법, 병렬적이고 효율적으로 네트워크 통신하는 방법
- JavaScript에서 제공하는, 비동기를 간편하게 처리하기 위한 object(따라서, Class 사용하듯 사용함)

## 2. State : pending → fulfilled or rejected

정해진 장시간의 기능을 수행 후(pending) →  
A. 기능이 정상적으로 수행됐으면(fulfilled) : 성공 메시지와 데이터를 전달(resolve) → then이용해, 전달받은 데이터를 사용  
B. 기능 수행 중 문제 발생 시(rejected) : 에러 전달(reject) → catch이용해, 전달받은 에러내용을 사용

## 3. Producer & Consumer

- Producer : 비동기적으로 수행하고자 하는 작업을, 성공/실패했을때 각각 어떻게 처리할지 로직을 작성
- Consumer : then(성공 시 데이터를 받아와 어떻게 쓸지), catch(실패 시 받아온 에러메시지를 어떻게 쓸지), finally(성공/실패 상관없이 화면에 어떤 처리를 할지) -> chian형태로 작성

```js
// 1. Producer : 비동기적으로 수행하고자 하는 작업을, 성공/실패했을때 각각 어떻게 처리할지 로직을 작성
const promise = new Promise((resolve, reject) => {
  // doing some heavy work(network, read files, ...)
  console.log('doing something...')
  setTimeout(() => {
    // resolve("fulfilled!!");
    reject(new Error('rejected!! - no network'))
  }, 2000)
})

// 2. Consumer : then(성공 시 데이터를 받아와 어떻게 쓸지), catch(실패 시 받아온 에러메시지를 어떻게 쓸지), finally(성공/실패 상관없이 화면에 어떤 처리를 할지) -> chian형태로 작성
promise
  .then((value) => {
    console.log(value)
  })
  .catch((error) => {
    console.log(error)
  })
  .finally(() => {
    console.log('finally^_^')
  })
```

## 4. Promise Chaining

```js
const fetchNumber = new Promise((resolve, reject) => {
  setTimeout(() => resolve(1), 1000)
})

fetchNumber
  .then((num) => num * 2) //2
  .then((num) => num * 3) //6
  .then((num) => {
    return new Promise((resolve, reject) => {
      setTimeout(() => resolve(num - 1), 1000) //5
    })
  })
  .then((num) => console.log(num)) //최종: 2초간 실행 후 콘솔에 5 찍힘
```

```js
const getHen = () =>
  new Promise((resolve, reject) => {
    setTimeout(() => resolve('🐓'), 1000)
  })
const getEgg = (hen) =>
  new Promise((resolve, reject) => {
    // setTimeout(() => resolve(`${hen} => 🥚`), 1000);
    setTimeout(() => reject(new Error(`error! ${hen} => 🥚`)), 1000)
  })
const cook = (egg) =>
  new Promise((resolve, reject) => {
    setTimeout(() => resolve(`${egg} => 🍳`), 1000)
  })

getHen() //
  .then(getEgg) //.then(hen => getEgg(hen))
  .catch((error) => {
    return '🧀' //바로 이어서 catch사용해 에러(egg못받아옴) 어떻게 처리할지 지정
  })
  .then(cook) //.then(egg => cook(egg))
  .then(console.log) //.then(meal => console.log(meal)) : 여기까지만 작성하면, 3초간 실행 후 결과: 🐓 => 🥚 => 🍳
  .catch(console.log) //.then(error => console.log(error)): 3초간 실행 후 결과=> Error: error! 🐓 => 🥚 at 4. promise.js:47:31
```

## 5. Callback Hell을 Promise 사용해 해결하기

Promise를 사용하여 => 콜백을 전달받지 않아도 되어 api로직이 더 간결해짐

```js
//class 사용해, 로그인 성공/실패 함수와 회원role 받아오는 함수 생성틀 각각 제작
class UserStorage {
  loginUser(id, password) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        if (
          (id === 'haeri@google.com' && password === '1234') ||
          (id === 'sally@google.com' && password === '0909')
        ) {
          resolve(id) //회원정보 일치해 로그인 성공 시, 함수onSuccess통해 id를 넘겨줌
        } else {
          reject(new Error('not found')) //회원정보 불일치해 로그인 실패 시, 에러 띄움
        }
      }, 2000)
    })
  }

  getRole(user) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        if (user === 'haeri@google.com') {
          resolve({ name: 'Haeri', role: 'admin' }) //로그인 성공한 회원 이름 확인해 맞으면, name과 role 반환
        } else {
          reject(new Error('no access')) //틀리면, 에러 띄움
        }
      }, 1000)
    })
  }
}

const user1 = new UserStorage()
const id = prompt('enter your id') //브라우저 API 사용해, 로그인하는 유저의 id와 password 받아오기
const password = prompt('enter your password')
user1
  .loginUser(id, password) //로그인
  .then((user) => user1.getRole(user)) // 로그인 성공 시 실행
  .then((user) => alert(`Hello ${user.name}, you have a ${user.role} role.`)) // role받아오기 성공 시 실행
  .catch((error) => console.log(error)) // 로그인 또는 role받아오기 실패 시 실행
```

---

# [Callback Hell 해결방법 2] async await

Promise를 사용하지 않아도 결과로 Promise를 반환(코드 더 간결해지는 장점)

## 1. Promise 함수를 async 사용해 바꾸기

```js
//1️⃣ Promise 로직
function fetchUser() {
  return new Promise((resolve, reject) => {
    //do network request in 10 secs...
    //return 'haeri'
    resolve('haeri')
  })
}

//📌 결과 : Promise쓴 위 로직이랑 async쓴 아래 로직이랑 동일
const user = fetchUser()
console.log(user) //Pending -> fetchUser()의 Promise 로직에 resolve 사용 -> fulfilled로 바뀜
user.then(console.log) //'haeri'

//2️⃣ async 사용해 리팩토링
async function fetchUser() {
  return 'haeri'
}
```

## 2. async & await

Promise를 반환하는 함수는 원래는 비동기적으로 실행되지만,  
async 안에서만 사용 가능한 await을 Promise 함수 앞에 사용하면  
➜ 마치 동기적으로 실행되듯, Promise 함수의 결과(응답)가 나온 후 그 다음 줄 로직을 실행한다

- async await 에러처리 구문은 `try {} catch() {}`

```js
function delay(ms) {
  //return new Promise((resolve, reject) => {
  //  setTimeout(resolve, ms)
  //})
  return new Promise((resolve) => setTimeout(resolve, ms))
}

//동기적으로 실행시킬 Promise반환 함수 delay()의 결과(응답)가 나온 후 그 다음 줄 로직을 실행
async function getApple() {
  await delay(1000)
  throw 'error'
  return '🍎'
}

async function getBanana() {
  await delay(1000)
  return '🍌'
}
```

## 3. 병렬 처리(1)

Promise반환 함수를 선언&할당 하면 그 즉시 실행되므로 서로 영향주지않고 진행되기 때문에,  
병렬처리(순차 아닌 동시 진행)하여 => 시간을 효율적으로 사용

```js
//1️⃣ Promise 사용: Promise도 너무 중첩 사용하게 되면 콜백지옥과 유사한 문제점 발생함
function pickFruits() {
  return getApple().then(apple => {
    return getBanana().then(banana =>
      `${apple}+${banana}`
    )
  })
}

//📌 결과(위 로직으로 다 받아와지면, 콘솔에 찍히게)
//pickFruits().then(result =>
//  console.log(result);
//)
pickFruits().then(console.log);  //2초 뒤(아래 병렬처리 후에는 1초 뒤), 🍎+🍌

//2️⃣ 리팩토링1: async&awiat 사용
async function pickFruits() {
  try {
    //const apple = await getApple();
    //const banana = await getBanana();
    //위 두 로직은 Promise반환 함수라 만들자마자(선언&할당 하자마자) 실행되어 서로 영향주지않고 진행되므로,
    //병렬처리(순차 아닌 동시 진행)하여 시간을 효율적으로 사용
    const applePromise = getApple();
    const bananaPromise = getPromise();
    const apple = await applePromise;
    const banana = await bananaPromise;
  } catch() {

  };
  return `${apple}+${banana}`;
}
```

## 4. 병렬처리(2) : Promise API `.all`

```js
//3️⃣ 리팩토링2: Promise API(.all) 사용
function pickAllFruits() {
  return Promise.all([getApple(), getBanana()].then(fruitsArr =>
    fruitsArr.join('+');
  ))
}

pickAllFruits().then(console.log);  //1초 뒤, 🍎+🍌(위의 병렬처리한 pickFruits와 같은 결과)
```

## 5. 병렬처리(3) : Promise API `.race`

Promise함수들 중 더 먼저 결과 나오는 것의 결과만 반환

```js
function pickOnlyOne() {
  return Promise.race([getApple(), getBanana()])
}

pickOnlyOne().then(console.log) //1초 뒤, 🍌
```
