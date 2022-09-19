---
title: 'JavaScript'
date: '2022-09-19'
lastmod: '2022-09-19'
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

# 3. class(ES6) : JavaScript는 객체지향 언어

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

# 4. Prototype

---

# 5. Hoisting

---

# 6. Scope

---

# 7. Closure

---

## 📌 Browser APIs

# 1. DOM Manipulation

---

# 2. Events

---

# 3. Fetch API(Async)

---

# 4. Vanilla JavaScript, Window Web API, Document(DOM Web API)
