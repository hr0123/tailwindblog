---
title: 'JavaScript'
date: '2022-09-19'
lastmod: '2022-09-20'
tags: ['javascript']
draft: false
summary: 'JavaScript 필수 기본'
---

## 📌 ES6 + Syntax : 문법은 첫번째로 익혀야하는 가장 중요한 것!

✔️ `'use strict'` : added in ES5) Vamila JavaScript에서 문서 최상단에 사용

# 1. (변수) let, const

### 1) let : Variable, rw(read & write)

added in ES6) 선언 전에 할당 시 error 발생

### 2) const : Constant, r(read only)

- 한 번 할당하면, 값 변경 불가 -> 장점: security, thread safety, reduce human mistakes
- 변수 값이 변화되어야할 적합한 이유가 없다면 왠만하면 const 사용하는 것이 바람직함

### 3) var 쓰지 말아야하는 이유

- 변수 선언 전에 할당 가능하므로
- hoisting : 어디에 선언했는가에 상관없이 선언을 위로 끌어올려줌
- block scope를 무시

---

# 2. Data Type

### 1) immutable data type(다른 값을 할당하는 것은 가능하나, 값 자체를 변형시키는 것은 불가) : primitive type, frozen object(`object.freeze()`)

primitive type : 더이상 작은 단위로 나눠질 수 없는 single item(number, string, boolean, null, undefined, symbol)

#### number

- infinity : 1 / 0
- negative infinity : -1 / 0
- NAN : string / number
- bigInt : 추가 전 number 범위는 '-2의 53승 ~ 2의 53승'이었는데, 더 큰 숫자 표현위해 추가된 것으로, 숫자뒤에 n 붙이면 bigInt타입으로 인식됨

#### string

- template literal

#### boolean

- false : 0, null, undefined, NaN, ' '
- true : any other value

#### null

- null : null로 값이 할당되어있음
- undefined : 선언은 되었으나 아무 값도 할당되지 않았거나 undefined라고 할당된 상태

#### symbol

- map이나 다른 자료구조에서 고유 식별자가 필요하거나 동시다발적으로 일어날수있는 코드에서 우선순위 주고싶을때

```javascript
const symbol1 - Symbol('id');
const symbol2 = Symbol('id');
console.log(symbol1 === symbol2); //false

const gSymbol1 - Symbol.for('id');
const gSymbol2 = Symbol.for('id');
console.log(gSymbol1.description === gSymbol2.description); //true: Symbol.for('이 값')이 동일하다면 그 둘은 서로 같은 값이 됨
//Symbol은 .description을 사용해 string으로 변환 후 출력해야 error안뜸
```

### 2) mutable data type : object type(object, array)

- single item들을 묶은 box container
- 다른 object로 할당은 불가하지만, object 내 Key와 Value 각각은 변경 가능
- `for...in` vs `for...of`

  ```javascript
  const obj = { name: 'Haeri', age: 20 }
  for (key in obj) {
    console.log(key) //name, age: obj라는 객체의 모든 Key들이 출력됨
  }

  const arr = [1, 2, 3, 4]
  for (value of arr) {
    console.log(value) //1,2,3,4: arr라는 배열 내 모든 요소들이 출력됨
  }
  ```

- Cloning

  ```javascript
  const user = {name="Haeri", age:20};
  const user2 = user; //user와 user2에는 동일한 reference가 들어있음
  user2.name = "coder";
  console.log(user); //{name:"coder", age:20}

  // old way
  const user3 = {};
  for(key in user) {
    user3[key] = user[key];
  }
  console.log(user3); //{name="Haeri", age:20}

  // other way
  const user4 = Object.assign({}, user);
  console.log(user4); //{name="Haeri", age:20}

  // another example
  const fruit1 = {color: "red"};
  const fruit2 = {color: "blue", size:"big"};
  const mixed = Object.assign({}, fruit1, fruit2);
  console.log(mixed.color); //blue: 덮어씌워져서 fruit2의 Value가 출력됨
  console.log(mixed.size); //big
  ```

### 3) function

first-class function : 함수를 변수에 할당 가능, 함수의 인자로 함수 전달 가능, 함수를 리턴 가능

### 4) JavaScript는 dynamically typed language(↔︎statically) ➜ TypeScript 사용 이유

변수 선언 때 타입 선언하지 않고, 프로그램이 동작할 떄 할당된 값에 따라 타입이 변경될 수 있음

- 장점 : 빠르게 프로토타입할 떄 유연하게 사용 가능
- 단점 : 다수 엔지니어, 규모있는 프로젝트 시 위험

### 5) operator(연산자) - object

```javascript
const obj1 = { name: 'haeri' }
const obj2 = { name: 'haeri' }
const obj3 = obj1
conosle.log(obj1 == obj2) //false: 별개의 객체는 서로 다른 reference를 갖고있으므로
conosle.log(obj1 === obj2) //false: 별개의 객체는 서로 다른 reference를 갖고있으므로
conosle.log(obj1 === obj3) //true
```

---

# 3. if, switch, while, for

### 1) Ternary Operator

```
condition ? true시 value : false시 value
```

### 2) Switch Operator

```javascript
switch() { //1. 괄호 안의 값이
    case '': //2. 이것일 경우
        return //3. 이것을 반환
    //반복
    default:
        return //기본 반환값 설정
}
```

### 3) While Loop(반복문)

```javascript
while() { //괄호 안에 로직 실행 조건
    //반복실행 로직
}

//body code(반복실행 로직)가 조건에 상관없이 먼저 실행되게 하려면
do {
    //반복실행 로직
} while () //괄호 안에 로직 실행 조건
```

### 4) nested loops : 되도록이면 피하는게 좋음

```javascript
for() {
    for() {

    }
}
```

### 5) break VS continue

- break : 반복문을 완전히 끝내는 것
- continue : 지금꺼만 skip하고, 다음 스텝으로 넘어가는 것

---

# 4. class(ES6) : JavaScript는 객체지향 언어

🔗 [JavaScript Object MDN Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference)

### 1) class VS object

- class(틀) : template / declare once / no data in
- object(틀에 반죽을 넣어 찍어낸 결과물) : instance of a class / created many times / data in

### 2) class로 만든 template을 사용해 ⇨ object 생성하기

- class는 syntatical sugar over prototype-based inheritance
- class는 fields, methods로 구성됨

```javascript
// class 선언
class Person {
    // 1. constructor: 추후 object만들때 필요한 데이터의 값을 전달
    constructor(name, age) {
        // 2. fields: 각 필요한 데이터에 전달받은 값을 바로 할당
        this.name = name;
        this.age = age;
    }
    // 3. methods 생성
    speak() {
        console.log(`${this.name}: hello!`;)
    }
}

// class 사용해, object 생성
const haeri = new Person('haeri', 20);
conosle.log(haeri.name); //haeri
conosle.log(haeri.name); //20
haeri.speak(); //함수 호출 => haeri: hello!
```

### 3) Getter & Setter

```javascript
class User {
  constructor(firstName, lastName, age) {
    this.firstName = firstName
    this.lastName = lastName
    this.age = age // 3.
  }
  // 1. Getter
  get age() {
    return this._age
  }
  // 2. Setter
  set age(value) {
    // if(value < 0) {
    //     throw Error('age can not be negative');
    // }
    this._age = value < 0 ? 0 : value
  }
}

const user1 = new User('haeri', 'Lee', -1)
console.log(user1.age) // 0
```

### 4) Fields - Public VS Private

```javascript
class Experiment {
  // constructor를 쓰지 않고 Field를 정의 가능
  publicField = 2 // 외부에서 접근 가능
  #privateField = 0 // class외부에서는 읽을수도 변경할수도 없음
}
const experiment = new Experiment()
console.log(experiment.publicField) // 2
console.log(experiment.privateField) // undefined
```

### 5) static : 들어오는 object에 상관없이, 공통적으로 class단위에서 사용되는 부분(메모리 사용 줄이기 위함)

```javascript
class Article {
  static publisher = 'Haeri'
  constructor(articleNumber) {
    this.articleNumber = articleNumber
  }
  static printPublisher() {
    console.log(Article.publisher)
  }
}

const article1 = new Article(1)
const article2 = new Article(2)
console.log(article1.publisher) //undefined
console.log(Article.publisher) //Haeri
Article.printPublisher() //Haeri
```

### 6) 상속 & 다양성

반복되는 공통 부분만 정의 후 -> 재사용(유지보수 쉬워짐)

```javascript
// class 생성
class Shape {
  // field 3개
  constructor(width, height, color) {
    this.width = width
    this.height = height
    this.color = color
  }
  // method 1
  draw() {
    console.log(`drawing ${this.color} color!`)
  }
  // method 2
  getArea() {
    return this.width * this.height
  }
}

class Rectangle extends Shape {} // Shape클래스의 모든 것들이 Rectanle클래스에 포함되어짐(상속)
const rectangle = new Rectangle(20, 20, 'blue')
rectangle.draw() // drawing blue color!
rectangle.getArea() // 400 (20*20)

//  Shape클래스의 모든 것들이 Triangle클래스에 포함되어지는데, 수정 필요 시 그 부분만 함수를 재정의해 가져올 수 있다(overriding_다양성)
class Triangle extends Shape {
    return (this.width * this.height) / 2;
}
const triangle = new Triangle(20, 20, 'red')
triangle.draw() // drawing red color!
triangle.getArea() // 200 (20*20/2)
```

### 7) `instanceOf` operate

```javascript
objectName instanceOf className // => object1가 class1를 사용해 만들어졌다면 true, 아니라면 false 반환
```

```javascript
console.log(rectangle instanceOf Rectangle) // true
console.log(triangle instanceOf Rectangle) // false
console.log(triangle instanceOf Triangle) // true
console.log(triangle instanceOf Shape) // true
console.log(triangle instanceOf Object) // true: JavaScript의 모든 객체는 Object를 상속한 것
```

---

# 5. Array(배열)

Array는 자료구조 중 하나 : 비슷한 유형의 object들을 모아두는 것

### 1) 배열을 선언 방법 2가지

```javascript
const arr1 = new Array()
const arr2 = [1, 2]
```

### 2) Index

```javascript
배열이름[Index] //해당 배열의 해당 Index의 요소가 출력됨
```

### 3) Looping over an array

```javascript
const fruits = ['apple', 'banana']
for (let fruit of fruits) {
  console.log(fruit) //'apple', 'banana': fruits라는 배열의 요소들이 순서대로 출력됨
}

// 배열fruits의 각 요소 순서대로 지정 로직을 실행
fruits.forEach((fruit, index, array) => {
  console.log(fruit, index) //'apple' 0, 'banana' 1
  console.log(array) //['apple', 'banana']
})
//->실사용: fruits.forEach((fruit) => console.log(fruit));
```

### 4) Addition, Deletion, Copy

- `shift`, `unshift`는 `push`, `pop`보다 느리다
- `splice`
  ```javascript
  배열명.splice(시작 인덱스, 제거 개수, 넣을 데이터);
  ```
- `concat`
  ```javascript
  const 배열3 = 배열1.concat(배열2)
  console.log(배열3) //배열1과 배열2가 합쳐진 새 배열
  ```

### 5) Searching

- `arr.indexOf()`
- `arr.lastIndexOf()`
- `arr.includes()`

---

# 6. JSON : 서버 통신의 시작

### HTTP(Hypertext Transfer Protocol) / AJAX(Asynchronous JavaScript And XML)

- Client(Browser 위에서 동작하고있는 웹사이트, 웹애플리케이션)가 Server와 어떻게 통신 즉, Hypertext(링크, 문서, 이미지 등)를 Transfer할 수 있는지 정의 및 규약한 Protocol의 하나  
  : Client가 Server에게 데이터를 request ➜ Server가 Client에게 해당 데이터를 response
- HTTP를 사용해 Client가 Server에게 데이터를 요청해 받아올 수 있는 방법은 AJAX(Asynchronous JavaScript And XML)  
  : 웹페이지에서 동적으로 Server에게 데이터를 주고 받을 수 있는 기술 - ex. XHR(XMLHttpRequest), fetch() API
  - XML : HTML과 마찬가지로 Markup언어의 일종으로 태그들을 사용해 데이터를 나타냄
  - XML뿐만 아니라 다양한 데이터(파일) 포맷으로 Client와 Server가 데이터를 주고 받을 수 있다
- 요즘 추세 : XML 말고 JSON(JavaScript Object Notation)을 많이 사용함
  - 1999년 ECMAScript 3rd의 Object에서 영감받아 만들어진 데이터(파일) 포맷: `Object{Key: Value}`
  - Browser에서뿐만 아니라, Mobile에서 Server와 데이터를 주고받을 때 or object를 파일 시스템에 저장할 때에도 이용
  - 프로그래밍 언어와 플랫폼에 상관없이, JSON을 사용해 serialization된 object를 다시 해당 언어의 특징에 맞게 object로 변환하고, 그 object를 다시 JSON으로 serialization하는 것을 지원(or 외부 라이브러리를 통해 가능하도록 함)

### 1) `stringify(obj)` Object to JSON: Object를 serialize(직렬화)하여 JSON으로 변환 방법

```javascript
stringify(value:any, replacer?:(this:any, key:string, value:any)=>any, space?:string|number): string
```

```javascript
let json = JSON.stringify(true)
console.log(json) //true

json = JSON.stringify(['haeri', 'sally'])
console.log(json) //["haeri","sally"]: 배열처럼 보이게 표기되고 큰따옴표

const rabbit = {
  name: 'haehaeri',
  color: 'white',
  size: null,
  birthDate: new Date(),
  jump: () => {
    console.log(`${this.name} can jump!`)
  },
  symbol: Symbol('id'),
}
json = JSON.stringify(rabbit)
console.log(json) //{"name": "haehaeri", "color": "white", "size": null, "birthDate": "2022-09-20..."}
// 함수jump는 객체rabbit에 있는 데이터가 아니므로 JSON에 포함되지 않아 JSON으로 변환되지 않음
// JavaScript에만 있는 특별한 데이터 Symbol()도 JSON에 포함되지 않아 JSON으로 변환되지 않음

json = JSON.stringify(rabbit, ['name'])
console.log(json) //{"name": "haehaeri"}: 원하는 Property만 JSON으로 변환하는 것도 가능

json = JSON.stringify(rabbit, (key, value) => {
  console.log(`key: ${key}, value: ${value}`)
  return key === 'name' ? 'HAERI' : value //{"name": "HAERI", "color": "white", "size": null, "birthDate": "2022-09-20..."}
})
```

### 2) `parse(json)` JSON to Object: 직렬화된 JSON을 deserialize하여 다시 Object로 변환 방법

```javascript
parse(text:string, reviver?:(this:any, key:string, value:any)=>any): any
```

```javascript
json = JSON.stringify(rabbit)
const obj = JSON.parse(json)
console.log(obj) //{name: "haehaeri", color: "white", size: null, birthDate: "2022-09-20..."}

rabbit.jump() //can jump!
obj.jump() //에러발생

console.log(rabbit.birthDate.getDate()) //29: new Date()라는 object자체이므로
console.log(obj.birthDate) //2022-09-20...
obj = JSON.parse(json, (key, value)=>{
  console.log(`key: ${key}, value: ${value}`)
  return key ==== 'birshDate' ? new Date(value) : value
})
console.log(obj.birthDate.getDate()) //29
```

### 유용 사이트

- [JSON Diff](https://www.jsondiff.com/) : Client가 Server에 요청해 받아온 데이터를 첫번째와 두번째를 비교(디버깅에 유용)
- [JSON Beautifier](https://jsonbeautifier.org/) : Server에 요청해 받아온 데이터 포맷 망가진 경우 정비
- [JSON Parser](https://jsonparser.org/) : JSON타입 데이터를 object형태로 확인
- [JSON Validator](https://tools.learningcontainer.com/json-validator/): 유효한 JSON인지, 어디 문제 있는지 확인

---

# Prototype

---

# Hoisting

---

# Scope

---

# Closure

---

## 📌 Browser APIs

# 1. DOM Manipulation

---

# 2. Events

---

# 3. Fetch API(Async)

---

# 4. Vanilla JavaScript, Window Web API, Document(DOM Web API)
