# TypeScript Essentials
## Interfaces
### 1. What are Interfaces
Interface는 컴파일 타임에만 필요합니다.
```ts
interface Person1 {
  name: string;
  age: number;
}

function hello1(person: Person1): void {
  console.log(`안녕하세요! ${person.name} 입니다.`);
}

const p1: Person1 = {
  name: 'Mark',
  age: 39
};

hello1(p1);
```
```js
"use strict";
function hello1(person) {
    console.log(`안녕하세요! ${person.name} 입니다.`);
}
const p1 = {
    name: 'Mark',
    age: 39
};
hello1(p1);
```

### 2. optional property
? - propert 값이 있어도 되고 없어도 된다.
```ts
interface Person2 {
  name: string;
  age?: number;
}

function hello2(person: Person2): void {
  console.log(`안녕하세요! ${person.name} 입니다.`);
}

hello2({name: 'Mark', age: 39});
hello2({name: 'Anna'});
```
[index: string]: any - 어떤 이름의 property가 와도 괜찮다.
```ts
interface Person3 {
  name: string;
  age?: number;
  [index: string]: any; 
}

function hello3(person: Person3): void {
  console.log(`안녕하세요! ${person.name} 입니다.`);
}

const p31: Person3 = {
  name: 'Mark',
  age: 39,
};
const p32: Person3 = {
  name: 'Anna',
  systers: ['Sung', 'Chan'],
};
const p33: Person3 = {
  name: 'Bokdaengi',
  father: p31,
  mother: p32,
};

hello3(p33);
```
### 3. function in interface
```ts
interface Person4 {
  name: string;
  age: number;
  hello(): void;
}

const p41: Person4 = {
  name: 'Mark',
  age: 39,
  hello: function(): void {
    console.log(`안녕하세요! ${this.name} 입니다.`);
  },
};
const p42: Person4 = {
  name: 'Mark',
  age: 39,
  hello(): void {
    console.log(`안녕하세요! ${this.name} 입니다.`);
  },
};
// const p43: Person4 = {
//   name: 'Mark',
//   age: 39,
//   hello: (): void => {
//     console.log(`안녕하세요! ${this.name} 입니다.`);
//   },
// };

p41.hello();
p42.hello();
```
### 4. class implements interface
```ts
interface IPerson1 {
  name: string;
  age?: number;
  hello(): void;
}

class Person implements IPerson1 {
  name: string;
  age?: number | undefined;

  constructor(name: string) {
    this.name = name
  }
  hello(): void {
    console.log(`안녕하세요! ${this.name} 입니다.`);
  }
}

const person: IPerson1 = new Person('Mark');
person.hello();
```
### 5. interface extends interface
```ts
interface IPerson2 {
  name: string;
  age?: number;
}

interface IKorean extends IPerson2 {
  city: string;
}

const k: IKorean = {
  name: '이웅재',
  city: '서울',
};
```
### 6. function interface
```ts
interface HelloPerson {
  (name: string, age?: number): void;
}

const helloPerson: HelloPerson = function(name: string, age?: number) {
  console.log(`안녕하세요! ${name} 입니다.`);
};

helloPerson('Mark', 39);
```
### 7. Readonly Interface Properties
```ts
interface Person8 {
  name: string;
  age?: number;
  readonly gender: string;
}

const p81: Person8 = {
  name: 'Mark',
  gender: 'male',
};

p81.gender = 'female';
```
### 8. type alias vs interface
```ts
//  - function -
// type alias
type EatType = (food: string) => void;
// interface
interface IEat {
  (food: string): void;
}
```
```ts
//  - array -
// type alias
type PersonList = string[];
// interface
interface IPersonList {
  [index: number]: string;
}
```
```ts
// - intersection -
interface ErrorHandling {
  success: boolean;
  error?: { message: string };
}
interface ArtistsData {
  artists: { name: string }[];
}
// type alias
type ArtistsResponseType = ArtistsData & ErrorHandling;
// interface
interface IArtistsResponse extends ArtistsData, ErrorHandling {}

let art: ArtistsResponseType;
let iar: IArtistsResponse;
```
```ts
// - union types -
interface Bird {
  fly(): void;
  layEggs(): void;
}
interface Fish {
  swim(): void;
  layEggs(): void;
}

type PetType = Bird | Fish;

interface IPet extends PetType {} // error
class Pet implements PetType {} // error
```
```ts
//  - Declaration Merging - interface
interface MergingInterface {
  a: string;
}
interface MergingInterface {
  b: string;
}
let mi: MergingInterface;

//  - Declaration Merging - type alias -
type MergingType = {
  a: string;
};
type MergingType = {
  b: string;
};
```
---
## Classes
### 1. What are Classes
- object를 만드는 blueprint(설계도)
- 클래스 이전에 object를 만드는 기본적인 방법은 function
- JavaScript에도 class는 es6부터 사용 가능
- OOP을 위한 초석
- TypeScript에서는 클래스도 사용자가 만드는 타입의 하나

### 2. Quick Start - class
- class 키워드를 이용하여 클래스를 만들 수 있다.
- class 이름은 보통 대문자를 이용한다.
- new를 이용하여 class를 통해 object를 만들 수 있다.
- constructor를 이용하여 object를 생성하면서 값을 전달할 수 있다.
- this를 이용해서 만들어진 object를 가리킬 수 있다.
- JS로 컴파일되면 es5의 경우 function으로 변경된다.

### 3. constructor & initialize
- 생성자 함수가 없으면, 디폴트 생성자가 불린다.
- 프로그래머가 만든 생성자가 하나라도 있으면, 디폴트 생성자는 사라진다.
- strict 모드에서는 프로퍼티를 선언하는 곳 또는 생성자에서 값을 할당해야 한다.
- 프로퍼티를 선언하는 곳 또는 생성자에서 값을 할당하지 않는 경우에는 !를 붙여서 위험을 표현한다.
- 클래스의 프로퍼티가 정의되어 있지만, 값을 대입하지 않으면 undefined이다.
- 생성자에는 async를 설정할 수 없다.

### 4. 접근 제어자(Access Modifiers)
- 접근 제어자에는 public, private, protected가 있다.
- 설정하지 않으면 public이다.
- 클래스 내부의 모든 곳에(생성자, 프로퍼티, 메서드)설정 가능하다.
- private으로 설정하면 클래스 외부에서 접근할 수 없다.
- 자바스크립트에서 private 지원하지 않아 오랜동안 프로퍼티나 메서드 이름 앞에 _를 붙여서 표현했다.

### 5. Getters & Setters
```ts
class Person10 {
  public constructor(private _name: string, private age: number) {

  }
  get name() {
    return this._name + " Lee";
  }

  set name(n: string) {
    this._name = n;
  }
}

const p10: Person10 = new Person10("Mark", 39);
console.log(p10.name); // get을 하는 함수 getter
p10.name = "Woongjae" // set을 하는 함수 setter
```
### 6. readonly properties
```ts
class Person10 {
  public readonly name: string = "Mark";
  public readonly country: string;
  
  public constructor(private _name: string, private age: number) {
    this.country = "Korea";
  }

  hello() {
    this.country = "China";
  }
}

const p10: Person10 = new Person10("Mark", 39);
console.log(p10.name); // get을 하는 함수 getter
p10.name = "Woongjae" // set을 하는 함수 setter
```
### 7. Index Signatures in class
```ts
// class => object
// { mark: 'male', jade: 'male' }
// { chloe: 'female', alex: 'male', anna: 'female' }

class Students {
  [index: string]: 'male' | 'female';

  mark: 'male' = 'male';
}

const a = new Students();
a.mark = 'male';
a.jade = 'male';

console.log(a);

const b = new Students();
b.chloe = 'female';
b.alex = 'male';
b.anna = 'female';

console.log(b);
```
### 8. Static Properties & Methods
```ts
class Person11 {
  private static CITY = 'Seoul';
  public hello() {
    console.log("안녕하세요", Person11.CITY);
  }
  public change() {
    Person11.CITY = 'LA';
  }
}

const p11 = new Person11();
// p11.hello();

const p12 = new Person11();

p12.hello();

p11.change();
```
### 9. Singletons
```ts
class ClassName {
  private static instance: ClassName | null = null;
  public static getInstance(): ClassName {
    // ClassName 으로부터 만든 object 가 있으면 그걸 리턴
    // className 으로부터 만든 object 가 없으면, 만든다.
    if (ClassName.instance === null) {
      ClassName.instance = new ClassName();
    }

    return ClassName.instance;
  }

  private constructor() {

  }
}

const a = ClassName.getInstance();
const b = ClassName.getInstance();

console.log(a === b);
```
### 10. 상속(Inheritance)
```ts
class Parent {
  constructor(protected _name: string, private _age: number) {}

  public print(): void {
    console.log(`이름은 ${this._name} 이고, 나이는 ${this._age} 입니다.`);
  }

  protected printName(): void {
    console.log(this._name, this._age);
  }
}

// const p = new Parent("Mark", 39);
// p.print();

class Child extends Parent {
  public gender = 'male';

  constructor(age: number) {
    super('Mark Jr.', age);

    this.printName();
  }
}

const c = new Child(1);
c.print();
```
### 11. Abstract Classes
```ts
abstract class AbstractPerson {
  protected _name: string = 'Mark';

  abstract setName(name: string): void; 
}

// new AbstractPerson()

class Person extends AbstractPerson {
  setName(name: string): void {
    this._name = name;
  }
}
const p = new Person();
p.setName();
```
---
## Generics
### 1. Generics, Any와 다른 점
```ts
function helloString(message: string): string {
  return message;
}

function helloNumber(message: number): number {
  return message;
}

// 더 많은 반복된 함수들...
function hello(message: any): any {
  return message;
}

console.log(hello("Mark").length);
console.log(hello(39).length);

function helloGeneric<T>(message: T): T {
  return message;
}

console.log(helloGeneric('Mark').length);
console.log(helloGeneric(39));
console.log(helloGeneric(true));
```
### 2. Generics Basic
```ts
function helloBasic<T, U>(message: T, comment: U): T {
  return message;
}

helloBasic<string, number>("Mark", 39);
helloBasic(36, 39);
```
### 3. Generics Array & Tuple
```ts
function helloArray<T>(message: T[]): T {
  return message[0];
}

helloArray(['Hello', 'World']);
helloArray(['hello', 5]);

function helloTuple<T, K>(message: [T, K]): T {
  return message[0];
}
helloTuple(["Hello", "World"]);
helloTuple(["Hello", 5]);
```
### 4. Generics Function
```ts
type HelloFunctionGeneric1 = <T>(message: T) => T; 

const helloFunction1: HelloFunctionGeneric1 = <T>(message: T): T => {
  return message;
};

interface HelloFunctionGeneric2 {
  <T>(message: T): T;
}

const helloFunction2: HelloFunctionGeneric2 = <T>(message: T): T => {
  return message;
};
```
### 5. Generics Class
```ts
class Person<T, K> {
  private _name: T;
  private _age: K;

  constructor(name: T, age: K) {
    this._name = name;
    this._age = age;
  }
}

new Person("Mark", 39);
// new Person<string>(39);
// new Person<string, number>("Mark", "age");
```
### 6. Generics with extends
```ts
class PersonExtends<T extends string | number> {
  private _name: T;

  constructor(name: T) {
    this._name = name;
  }
}

new PersonExtends("Mark");
new PersonExtends(39);
// new PersonExtends(true);
```
### 7. keyof & type lookup system
```ts
interface IPerson {
  name: string;
  age: number;
}

const person: IPerson = {
  name: 'Mark',
  age: 39,
};

// IPerson[keyof IPerson]
// => IPerson["name" | "age"] 
// => IPerson["name"] | IPerson["age"]
// => string | number
function getProp<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

getProp(person, "name");

function setProp<T, K extends keyof T>(obj: T, key: K, value: T[K]): void {
  obj[key] = value;
}

setProp(person, "name", "Anna");
```