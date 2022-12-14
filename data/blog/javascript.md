---
title: 'JavaScript'
date: '2022-09-19'
lastmod: '2022-09-20'
tags: ['javascript']
draft: false
summary: 'JavaScript νμ κΈ°λ³Έ'
---

## π ES6 + Syntax : λ¬Έλ²μ μ²«λ²μ§Έλ‘ μ΅νμΌνλ κ°μ₯ μ€μν κ²!

βοΈ `'use strict'` : added in ES5) Vamila JavaScriptμμ λ¬Έμ μ΅μλ¨μ μ¬μ©

# 1. (λ³μ) let, const

### 1) let : Variable, rw(read & write)

added in ES6) μ μΈ μ μ ν λΉ μ error λ°μ

### 2) const : Constant, r(read only)

- ν λ² ν λΉνλ©΄, κ° λ³κ²½ λΆκ° -> μ₯μ : security, thread safety, reduce human mistakes
- λ³μ κ°μ΄ λ³νλμ΄μΌν  μ ν©ν μ΄μ κ° μλ€λ©΄ μ λ§νλ©΄ const μ¬μ©νλ κ²μ΄ λ°λμ§ν¨

### 3) var μ°μ§ λ§μμΌνλ μ΄μ 

- λ³μ μ μΈ μ μ ν λΉ κ°λ₯νλ―λ‘
- hoisting : μ΄λμ μ μΈνλκ°μ μκ΄μμ΄ μ μΈμ μλ‘ λμ΄μ¬λ €μ€
- block scopeλ₯Ό λ¬΄μ

---

# 2. Data Type

### 1) immutable data type(λ€λ₯Έ κ°μ ν λΉνλ κ²μ κ°λ₯νλ, κ° μμ²΄λ₯Ό λ³νμν€λ κ²μ λΆκ°) : primitive type, frozen object(`object.freeze()`)

primitive type : λμ΄μ μμ λ¨μλ‘ λλ μ§ μ μλ single item(number, string, boolean, null, undefined, symbol)

#### number

- infinity : 1 / 0
- negative infinity : -1 / 0
- NAN : string / number
- bigInt : μΆκ° μ  number λ²μλ '-2μ 53μΉ ~ 2μ 53μΉ'μ΄μλλ°, λ ν° μ«μ ννμν΄ μΆκ°λ κ²μΌλ‘, μ«μλ€μ n λΆμ΄λ©΄ bigIntνμμΌλ‘ μΈμλ¨

#### string

- template literal

#### boolean

- false : 0, null, undefined, NaN, ' '
- true : any other value

#### null

- null : nullλ‘ κ°μ΄ ν λΉλμ΄μμ
- undefined : μ μΈμ λμμΌλ μλ¬΄ κ°λ ν λΉλμ§ μμκ±°λ undefinedλΌκ³  ν λΉλ μν

#### symbol

- mapμ΄λ λ€λ₯Έ μλ£κ΅¬μ‘°μμ κ³ μ  μλ³μκ° νμνκ±°λ λμλ€λ°μ μΌλ‘ μΌμ΄λ μμλ μ½λμμ μ°μ μμ μ£Όκ³ μΆμλ

```javascript
const symbol1 - Symbol('id');
const symbol2 = Symbol('id');
console.log(symbol1 === symbol2); //false

const gSymbol1 - Symbol.for('id');
const gSymbol2 = Symbol.for('id');
console.log(gSymbol1.description === gSymbol2.description); //true: Symbol.for('μ΄ κ°')μ΄ λμΌνλ€λ©΄ κ·Έ λμ μλ‘ κ°μ κ°μ΄ λ¨
//Symbolμ .descriptionμ μ¬μ©ν΄ stringμΌλ‘ λ³ν ν μΆλ ₯ν΄μΌ errorμλΈ
```

### 2) mutable data type : object type(object, array)

- single itemλ€μ λ¬Άμ box container
- λ€λ₯Έ objectλ‘ ν λΉμ λΆκ°νμ§λ§, object λ΄ Keyμ Value κ°κ°μ λ³κ²½ κ°λ₯
- `for...in` vs `for...of`

  ```javascript
  const obj = { name: 'Haeri', age: 20 }
  for (key in obj) {
    console.log(key) //name, age: objλΌλ κ°μ²΄μ λͺ¨λ  Keyλ€μ΄ μΆλ ₯λ¨
  }

  const arr = [1, 2, 3, 4]
  for (value of arr) {
    console.log(value) //1,2,3,4: arrλΌλ λ°°μ΄ λ΄ λͺ¨λ  μμλ€μ΄ μΆλ ₯λ¨
  }
  ```

- Cloning

  ```javascript
  const user = {name="Haeri", age:20};
  const user2 = user; //userμ user2μλ λμΌν referenceκ° λ€μ΄μμ
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
  console.log(mixed.color); //blue: λ?μ΄μμμ Έμ fruit2μ Valueκ° μΆλ ₯λ¨
  console.log(mixed.size); //big
  ```

### 3) function

first-class function : ν¨μλ₯Ό λ³μμ ν λΉ κ°λ₯, ν¨μμ μΈμλ‘ ν¨μ μ λ¬ κ°λ₯, ν¨μλ₯Ό λ¦¬ν΄ κ°λ₯

### 4) JavaScriptλ dynamically typed language(βοΈstatically) β TypeScript μ¬μ© μ΄μ 

λ³μ μ μΈ λ νμ μ μΈνμ§ μκ³ , νλ‘κ·Έλ¨μ΄ λμν  λ ν λΉλ κ°μ λ°λΌ νμμ΄ λ³κ²½λ  μ μμ

- μ₯μ  : λΉ λ₯΄κ² νλ‘ν νμν  λ μ μ°νκ² μ¬μ© κ°λ₯
- λ¨μ  : λ€μ μμ§λμ΄, κ·λͺ¨μλ νλ‘μ νΈ μ μν

### 5) operator(μ°μ°μ) - object

```javascript
const obj1 = { name: 'haeri' }
const obj2 = { name: 'haeri' }
const obj3 = obj1
conosle.log(obj1 == obj2) //false: λ³κ°μ κ°μ²΄λ μλ‘ λ€λ₯Έ referenceλ₯Ό κ°κ³ μμΌλ―λ‘
conosle.log(obj1 === obj2) //false: λ³κ°μ κ°μ²΄λ μλ‘ λ€λ₯Έ referenceλ₯Ό κ°κ³ μμΌλ―λ‘
conosle.log(obj1 === obj3) //true
```

---

# 3. if, switch, while, for

### 1) Ternary Operator

```
condition ? trueμ value : falseμ value
```

### 2) Switch Operator

```javascript
switch() { //1. κ΄νΈ μμ κ°μ΄
    case '': //2. μ΄κ²μΌ κ²½μ°
        return //3. μ΄κ²μ λ°ν
    //λ°λ³΅
    default:
        return //κΈ°λ³Έ λ°νκ° μ€μ 
}
```

### 3) While Loop(λ°λ³΅λ¬Έ)

```javascript
while() { //κ΄νΈ μμ λ‘μ§ μ€ν μ‘°κ±΄
    //λ°λ³΅μ€ν λ‘μ§
}

//body code(λ°λ³΅μ€ν λ‘μ§)κ° μ‘°κ±΄μ μκ΄μμ΄ λ¨Όμ  μ€νλκ² νλ €λ©΄
do {
    //λ°λ³΅μ€ν λ‘μ§
} while () //κ΄νΈ μμ λ‘μ§ μ€ν μ‘°κ±΄
```

### 4) nested loops : λλλ‘μ΄λ©΄ νΌνλκ² μ’μ

```javascript
for() {
    for() {

    }
}
```

### 5) break VS continue

- break : λ°λ³΅λ¬Έμ μμ ν λλ΄λ κ²
- continue : μ§κΈκΊΌλ§ skipνκ³ , λ€μ μ€νμΌλ‘ λμ΄κ°λ κ²

---

# 4. class(ES6) : JavaScriptλ κ°μ²΄μ§ν₯ μΈμ΄

π [JavaScript Object MDN Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference)

### 1) class VS object

- class(ν) : template / declare once / no data in
- object(νμ λ°μ£½μ λ£μ΄ μ°μ΄λΈ κ²°κ³Όλ¬Ό) : instance of a class / created many times / data in

### 2) classλ‘ λ§λ  templateμ μ¬μ©ν΄ β¨ object μμ±νκΈ°

- classλ syntatical sugar over prototype-based inheritance
- classλ fields, methodsλ‘ κ΅¬μ±λ¨

```javascript
// class μ μΈ
class Person {
    // 1. constructor: μΆν objectλ§λ€λ νμν λ°μ΄ν°μ κ°μ μ λ¬
    constructor(name, age) {
        // 2. fields: κ° νμν λ°μ΄ν°μ μ λ¬λ°μ κ°μ λ°λ‘ ν λΉ
        this.name = name;
        this.age = age;
    }
    // 3. methods μμ±
    speak() {
        console.log(`${this.name}: hello!`;)
    }
}

// class μ¬μ©ν΄, object μμ±
const haeri = new Person('haeri', 20);
conosle.log(haeri.name); //haeri
conosle.log(haeri.name); //20
haeri.speak(); //ν¨μ νΈμΆ => haeri: hello!
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
  // constructorλ₯Ό μ°μ§ μκ³  Fieldλ₯Ό μ μ κ°λ₯
  publicField = 2 // μΈλΆμμ μ κ·Ό κ°λ₯
  #privateField = 0 // classμΈλΆμμλ μ½μμλ λ³κ²½ν μλ μμ
}
const experiment = new Experiment()
console.log(experiment.publicField) // 2
console.log(experiment.privateField) // undefined
```

### 5) static : λ€μ΄μ€λ objectμ μκ΄μμ΄, κ³΅ν΅μ μΌλ‘ classλ¨μμμ μ¬μ©λλ λΆλΆ(λ©λͺ¨λ¦¬ μ¬μ© μ€μ΄κΈ° μν¨)

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

### 6) μμ & λ€μμ±

λ°λ³΅λλ κ³΅ν΅ λΆλΆλ§ μ μ ν -> μ¬μ¬μ©(μ μ§λ³΄μ μ¬μμ§)

```javascript
// class μμ±
class Shape {
  // field 3κ°
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

class Rectangle extends Shape {} // Shapeν΄λμ€μ λͺ¨λ  κ²λ€μ΄ Rectanleν΄λμ€μ ν¬ν¨λμ΄μ§(μμ)
const rectangle = new Rectangle(20, 20, 'blue')
rectangle.draw() // drawing blue color!
rectangle.getArea() // 400 (20*20)

//  Shapeν΄λμ€μ λͺ¨λ  κ²λ€μ΄ Triangleν΄λμ€μ ν¬ν¨λμ΄μ§λλ°, μμ  νμ μ κ·Έ λΆλΆλ§ ν¨μλ₯Ό μ¬μ μν΄ κ°μ Έμ¬ μ μλ€(overriding_λ€μμ±)
class Triangle extends Shape {
    return (this.width * this.height) / 2;
}
const triangle = new Triangle(20, 20, 'red')
triangle.draw() // drawing red color!
triangle.getArea() // 200 (20*20/2)
```

### 7) `instanceOf` operate

```javascript
objectName instanceOf className // => object1κ° class1λ₯Ό μ¬μ©ν΄ λ§λ€μ΄μ‘λ€λ©΄ true, μλλΌλ©΄ false λ°ν
```

```javascript
console.log(rectangle instanceOf Rectangle) // true
console.log(triangle instanceOf Rectangle) // false
console.log(triangle instanceOf Triangle) // true
console.log(triangle instanceOf Shape) // true
console.log(triangle instanceOf Object) // true: JavaScriptμ λͺ¨λ  κ°μ²΄λ Objectλ₯Ό μμν κ²
```

---

# 5. Array(λ°°μ΄)

Arrayλ μλ£κ΅¬μ‘° μ€ νλ : λΉμ·ν μ νμ objectλ€μ λͺ¨μλλ κ²

### 1) λ°°μ΄μ μ μΈ λ°©λ² 2κ°μ§

```javascript
const arr1 = new Array()
const arr2 = [1, 2]
```

### 2) Index

```javascript
λ°°μ΄μ΄λ¦[Index] //ν΄λΉ λ°°μ΄μ ν΄λΉ Indexμ μμκ° μΆλ ₯λ¨
```

### 3) Looping over an array

```javascript
const fruits = ['apple', 'banana']
for (let fruit of fruits) {
  console.log(fruit) //'apple', 'banana': fruitsλΌλ λ°°μ΄μ μμλ€μ΄ μμλλ‘ μΆλ ₯λ¨
}

// λ°°μ΄fruitsμ κ° μμ μμλλ‘ μ§μ  λ‘μ§μ μ€ν
fruits.forEach((fruit, index, array) => {
  console.log(fruit, index) //'apple' 0, 'banana' 1
  console.log(array) //['apple', 'banana']
})
//->μ€μ¬μ©: fruits.forEach((fruit) => console.log(fruit));
```

### 4) Addition, Deletion, Copy

- `shift`, `unshift`λ `push`, `pop`λ³΄λ€ λλ¦¬λ€
- `splice`
  ```javascript
  λ°°μ΄λͺ.splice(μμ μΈλ±μ€, μ κ±° κ°μ, λ£μ λ°μ΄ν°);
  ```
- `concat`
  ```javascript
  const λ°°μ΄3 = λ°°μ΄1.concat(λ°°μ΄2)
  console.log(λ°°μ΄3) //λ°°μ΄1κ³Ό λ°°μ΄2κ° ν©μ³μ§ μ λ°°μ΄
  ```

### 5) Searching

- `arr.indexOf()`
- `arr.lastIndexOf()`
- `arr.includes()`

---

# 6. JSON : μλ² ν΅μ μ μμ

### HTTP(Hypertext Transfer Protocol) / AJAX(Asynchronous JavaScript And XML)

- Client(Browser μμμ λμνκ³ μλ μΉμ¬μ΄νΈ, μΉμ νλ¦¬μΌμ΄μ)κ° Serverμ μ΄λ»κ² ν΅μ  μ¦, Hypertext(λ§ν¬, λ¬Έμ, μ΄λ―Έμ§ λ±)λ₯Ό Transferν  μ μλμ§ μ μ λ° κ·μ½ν Protocolμ νλ  
  : Clientκ° Serverμκ² λ°μ΄ν°λ₯Ό request β Serverκ° Clientμκ² ν΄λΉ λ°μ΄ν°λ₯Ό response
- HTTPλ₯Ό μ¬μ©ν΄ Clientκ° Serverμκ² λ°μ΄ν°λ₯Ό μμ²­ν΄ λ°μμ¬ μ μλ λ°©λ²μ AJAX(Asynchronous JavaScript And XML)  
  : μΉνμ΄μ§μμ λμ μΌλ‘ Serverμκ² λ°μ΄ν°λ₯Ό μ£Όκ³  λ°μ μ μλ κΈ°μ  - ex. XHR(XMLHttpRequest), fetch() API
  - XML : HTMLκ³Ό λ§μ°¬κ°μ§λ‘ MarkupμΈμ΄μ μΌμ’μΌλ‘ νκ·Έλ€μ μ¬μ©ν΄ λ°μ΄ν°λ₯Ό λνλ
  - XMLλΏλ§ μλλΌ λ€μν λ°μ΄ν°(νμΌ) ν¬λ§·μΌλ‘ Clientμ Serverκ° λ°μ΄ν°λ₯Ό μ£Όκ³  λ°μ μ μλ€
- μμ¦ μΆμΈ : XML λ§κ³  JSON(JavaScript Object Notation)μ λ§μ΄ μ¬μ©ν¨
  - 1999λ ECMAScript 3rdμ Objectμμ μκ°λ°μ λ§λ€μ΄μ§ λ°μ΄ν°(νμΌ) ν¬λ§·: `Object{Key: Value}`
  - BrowserμμλΏλ§ μλλΌ, Mobileμμ Serverμ λ°μ΄ν°λ₯Ό μ£Όκ³ λ°μ λ or objectλ₯Ό νμΌ μμ€νμ μ μ₯ν  λμλ μ΄μ©
  - νλ‘κ·Έλλ° μΈμ΄μ νλ«νΌμ μκ΄μμ΄, JSONμ μ¬μ©ν΄ serializationλ objectλ₯Ό λ€μ ν΄λΉ μΈμ΄μ νΉμ§μ λ§κ² objectλ‘ λ³ννκ³ , κ·Έ objectλ₯Ό λ€μ JSONμΌλ‘ serializationνλ κ²μ μ§μ(or μΈλΆ λΌμ΄λΈλ¬λ¦¬λ₯Ό ν΅ν΄ κ°λ₯νλλ‘ ν¨)

### 1) `stringify(obj)` Object to JSON: Objectλ₯Ό serialize(μ§λ ¬ν)νμ¬ JSONμΌλ‘ λ³ν λ°©λ²

```javascript
stringify(value:any, replacer?:(this:any, key:string, value:any)=>any, space?:string|number): string
```

```javascript
let json = JSON.stringify(true)
console.log(json) //true

json = JSON.stringify(['haeri', 'sally'])
console.log(json) //["haeri","sally"]: λ°°μ΄μ²λΌ λ³΄μ΄κ² νκΈ°λκ³  ν°λ°μ΄ν

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
// ν¨μjumpλ κ°μ²΄rabbitμ μλ λ°μ΄ν°κ° μλλ―λ‘ JSONμ ν¬ν¨λμ§ μμ JSONμΌλ‘ λ³νλμ§ μμ
// JavaScriptμλ§ μλ νΉλ³ν λ°μ΄ν° Symbol()λ JSONμ ν¬ν¨λμ§ μμ JSONμΌλ‘ λ³νλμ§ μμ

json = JSON.stringify(rabbit, ['name'])
console.log(json) //{"name": "haehaeri"}: μνλ Propertyλ§ JSONμΌλ‘ λ³ννλ κ²λ κ°λ₯

json = JSON.stringify(rabbit, (key, value) => {
  console.log(`key: ${key}, value: ${value}`)
  return key === 'name' ? 'HAERI' : value //{"name": "HAERI", "color": "white", "size": null, "birthDate": "2022-09-20..."}
})
```

### 2) `parse(json)` JSON to Object: μ§λ ¬νλ JSONμ deserializeνμ¬ λ€μ Objectλ‘ λ³ν λ°©λ²

```javascript
parse(text:string, reviver?:(this:any, key:string, value:any)=>any): any
```

```javascript
json = JSON.stringify(rabbit)
const obj = JSON.parse(json)
console.log(obj) //{name: "haehaeri", color: "white", size: null, birthDate: "2022-09-20..."}

rabbit.jump() //can jump!
obj.jump() //μλ¬λ°μ

console.log(rabbit.birthDate.getDate()) //29: new Date()λΌλ objectμμ²΄μ΄λ―λ‘
console.log(obj.birthDate) //2022-09-20...
obj = JSON.parse(json, (key, value)=>{
  console.log(`key: ${key}, value: ${value}`)
  return key ==== 'birshDate' ? new Date(value) : value
})
console.log(obj.birthDate.getDate()) //29
```

### μ μ© μ¬μ΄νΈ

- [JSON Diff](https://www.jsondiff.com/) : Clientκ° Serverμ μμ²­ν΄ λ°μμ¨ λ°μ΄ν°λ₯Ό μ²«λ²μ§Έμ λλ²μ§Έλ₯Ό λΉκ΅(λλ²κΉμ μ μ©)
- [JSON Beautifier](https://jsonbeautifier.org/) : Serverμ μμ²­ν΄ λ°μμ¨ λ°μ΄ν° ν¬λ§· λ§κ°μ§ κ²½μ° μ λΉ
- [JSON Parser](https://jsonparser.org/) : JSONνμ λ°μ΄ν°λ₯Ό objectννλ‘ νμΈ
- [JSON Validator](https://tools.learningcontainer.com/json-validator/): μ ν¨ν JSONμΈμ§, μ΄λ λ¬Έμ  μλμ§ νμΈ

---

# Prototype

---

# Hoisting

---

# Scope

---

# Closure

---

## π Browser APIs

# 1. DOM Manipulation

---

# 2. Events

---

# 3. Fetch API(Async)

---

# 4. Vanilla JavaScript, Window Web API, Document(DOM Web API)
