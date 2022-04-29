# TypeScript Essentials
## TypeScript
### 1. TypeScript 란 무엇인가
- 타입스크립트는 'Programming Language'입니다.
- 타입스크립트는 'Compiled Language'입니다.
	- 전통적인 'Compiled Language 와는 다른 점이 많습니다.
	- 그래서 'Transpile'이라는 용어를 사용하기도 합니다.
- 자바스크립트는 'Interpreted Language'입니다.
### 2. TypeScript 설치 및 사용
#### npm / Visual Studio plugin
- npm
	- npm i typescript -g
	- node modules/.bin/tsc
	- tsc source.ts
- Visual Studio plugin 설치
	- Visual Studdio 2017/2015 Update 3 이후로는 디폴트로 설치되어 있음
### 3. First Type Annotation
```ts
let a: string;
a = "Mark";
a = 39; // error

let b: number;
b = "Mark" //error
b = 39;

function hello(c: number) {
}
hello(39);
```
---
## Basic Types
### 1. Primitive Types
- 오브젝트와 레퍼런스 형태가 아닌 실제 값을 저장하는 자료형입니다.
- 프리미티브 형의 내장 함수를 사용 가능한 것은 자바스크립트 처리 방식 덕분
- (ES2015 기준) 6가지
	- boolean
	- number
	- string
	- null
	- undefined
	- symbol
```js
// literal 값으로 Primitive 타입의 서브 타입을 나타낼 수 있다.
true;
'hello';
3.14;
null;

// 래퍼 객체로 만들 수 있다.
new String('world');
new Number(42);
```
#### Type Casing
- 타입스크립트의 핵심 primitive types은 모두 소문자입니다.
- Number, String, Boolean, Symbol 또는 Object 유형이 위에서 권장한 소문자 버전과 동일하다고 생각하고 싶을 수 있습니다.  그러나 이러한 유형은 primitives를 나타내지 않으며, 타입으로 사용해서는 안된다.

### 2. boolean
```ts
let isDone: boolean = false;
isDone = true;
console.log(typeof isDone) // boolean

let isOk: Boolean = true;
let isNotOk: boolean = new Boolean(true); // error
```

### 3. number
```ts
let decimal: number = 6; // 10진수 리터럴

let hex: number = 0xf00d; // 16진수 리터럴

let binary: number = 0b1010; // 2진수 리터럴

let octal: number = 0o744; // 8진수 리터럴

let notANumber: number = NaN;

let underscoreNum: number = 1_000_000;
```

### 4. string
```ts
let myName: string = "Mark";

// Template String
// 행에 걸쳐 있거나, 표현식을 넣을 수 있는 문자열
// 이 문자열은 backtick기호에 둘러쌓여 있습니다.

let fullName: string = "Mark Lee";
let age: number = 39;
let sentence: string = `Hello, My name is ${fullName}.

I'll be ${age + 1} years old next month.`;
console.log(sentence);
```

### 5. symbol
```ts
// Symbol
// 프리미티브 타입의 값을 담아서 사용합니다.
// 고유하고 수정불가능한 값으로 만들어줍니다.
// 그래서 주로 접근을 제어하는데 쓰는 경우가 많습니다.

console.log(Symbol('foo') === Symbol('foo')); // false 

const sym = Symbol();

const obj = {
	[sym]: "value",
};

obj[sym]
```

### 6. null & undefined
```ts
let name: string = null;
let age: number = undefined;

// strictNullChecks => true
// Type 'null' is not assignable to type 'string'.
let name: string = null; // (x)

// null => null || void, undefined => undefined || void
// Type 'null' is not assignable to type 'undefined'
let u: undefined = null; // (x)

let v: void = undefined; // (o)

let union: string | null | undefined = 'str';
```

### 7. object
```ts
// object
// primitive type이 아닌 것 을 나타내고 싶을 때 사용하는 타입

let obj: object = {};
obj = {name: 'Mark'};
obj = [{name: 'Mark'}];
obj = 39; // error
obj = 'Mark'; // error
obj = true; // error
obj = undefined; // error
obj = null; // error

declare function create(o: object | null): void;
create({ prop: 0});
create(null);
create(42); // error
create("string") // error
```

### 8. Array
```ts
let list: number[] = [1, 2, 3];
let list2: Array<number> = [1, 2, 3];
let list3: (number | string)[] = [1, 2, 3, "4"];
```

### 9. Tuple
```ts
let x: [string, number];

x = ["hello", 39];

x = [10, "Mark"]; // error

// 배열 인덱스 수가 맞지 않아 할당 할 수 없다.
x[3] = "word"; // error

const person: [string, number] = ["Mark", 39];
const [first, second] = person;
```

### 10. any
- 어떤 타입이어도 상관없는 타입입니다.
- any 타입을 최닿ㄴ 쓰지 않는게 핵심입니다.
- 왜냐면 컴파일 타임에 타입 체크가 정상적으로 이뤄지지 않기 때문입니다.
- 그래서 컴파일 옵션 중에는 any를 써야하는데 쓰지 않으면 오류를 뱉도록 하는 옵션이 있습니다.(nolmplicitAny)

```ts
function returnAny(message: any): any {
	console.log(message);
}
const any1 = returnAny("리턴은 아무거나");

any1.toString();

let looselyTyped: any = {};

// 개체를 통해 계속 전파된다.
const d = looselyTyped.a.b.c.d;

function leakingAny(obj: any) {
	const a = obj.num;
	const b = a + 1;
	return b;
}

const c = leakingAny({num: 0});
c.indexOf('0');
```

### 11. unknown
- Typescript 3.0 버전부터 지원
- any와 짝으로 any 보다 Type-safe한 타입
	- any와 같이 아무거나 할당할 수 있다.
	- 컴파일러가 타입을 추론할 수 있게끔 타입의 유형을 좁히거나
	- 타입을 확정해주지 않으면 다른 곳에 할당 할 수 없고, 사용할 수 없다.
- unknown 타입을 사용하면 runtime error를 줄일 수 있을 것 같다.
```ts
declare const maybe: unknown;


const aNumber: number = maybe; // error

if (maybe === true) {
	const aBoolean: boolean = maybe;

	const aString: string = maybe; // error
}

if (typeof maybe === 'string') {
	const aString: string = maybe;

	const aBoolean: boolean = maybe; // error
}
```

### 12. never
- never 타입은 모든 타입의 subtype 이며, 모든 타입에 할당 할 수 있습니다.
- 하지만, never에는 그 어떤 것도 할당 할 수 없습니다.
- any 조차도 never에게 할당 할 수 없습니다.
- 잘못된 타입을 넣는 실수를 막고자 할 때 사용합니다.
```ts
function error(message: string): never {
	throw new Error(message);
}

function fail() {
	return error("failed");
}

function infiniteLoop(): never {
	while(true) {}
}

let a: string = "hello";

if (typeof a !== 'string') {
	a; // never 타입
}

declare const b: string | number;
if (typeof b !== 'string') {
	b; // number 타입
}
```

### 13. void
```ts
// 리턴 타입을 void로 지정하면 return 값으로 유일하게 undeined만 올 수 있다.
function returnVoid(message: string): void {
	console.log(message):
	
	return undefined;
}

returnVoid('리턴이 없다');
```
---
## Type System
### 1. 작성자와 사용자의 관점으로 코드 바라보기
#### 타입 시스템
- 컴파일러에게 사용하는 타입을 명시적으로 지정하는 시스템
- 컴파일러가 자동으로 타입을 추론하는 시스템

#### 타입스크립트의 타입 시스템
- 타입을 명시적으로 지정할 수 있다.
- 타입을 명시적으로 지정하지 않으면, 타입스크립트 컴파일러가 자동으로 타입을 추론한다.

### 2. Structural Type System vs Nominal Type System
```ts
// Structural Type System - 구조가 같으면, 같은 타입이다.
interface IPerson {
	name: string;
	age: number;
	speak(): string;
}

type PersonType = {
	name: string;
	age: number;
	speak(): string;
};

let personInterface: IPerson = {} as any;
let personType: PersonType = {} as any;

personInterface = personType;
personType = personInterface;

// Nominal Type System - 구조가 같아도 이름이 다르면, 다른 타입이다.
type PersonID = string & { readonly brand: unique symbol };
function PersonID(id: string): PersonID {
	return id as PersonID;
}

function getPersonById(id: PersonID) {}

getPersonById(PersonID('id-aaaaa'));
getPersonById('id-aaaaaa'); // error
```

### 3. 타입 호환성(Type Compatibility)
```ts
// 서브 타입
let sub1: 1 = 1;
let sup1: number = sub1;
sub1 = sup1; // error

let sub2: number[] = [1];
let sup2: object = sub2;
sub2 = sup2; // error

let sub3: [number, number] = [1, 2];
let sup3: number[] = sub3;
sub3 = sup3; // error

let sub4: number = 1;
let sup4: any = sub4;
sub4 = sup4;

let sub5: never = 0 as never;
let sup5: number = sub5;
sub5 = sup5; // error

class Animal {}
class Dog extends Animal {
	eat() {}
}

let sub6: Dog = new Dog();
let sup6: Animal = sub6;
sub6 = sup6; // error

// 1. 같거나 서브 타입인 경우, 할당이 가능하다. => 공변
// primitive type
let sub7: string = '';
let sup7: string | number = sub7;

// object - 각각의 프로퍼티가 대응하는 프로퍼티와 같거나 서브타입이어야 한다.
let sub8: { a: string; b: number } = { a: '', b: 1 };
let sup8: { a: string | number; b: number } = sub8;

// array - object 와 마찬가지
let sub9: Array<{ a: string; b: number }> = [{ a; '', b: 1}];
let sup9: Array<{ a: string | number; b: number }> = sub8;

// 2. 함수의 매개변수 타입만 같거나 슈퍼타입인 경우, 할당이 가능하다. => 반병
class Person {}
class Developer extends Person {
	coding() {}
}
class StartupDeveloper extends Developer {
	burning() {}
}

function tellme(f: (d: Developer) => Developer) {}

// Developer => Developer 에다가 Developer => Developer 를 할당하는 경우
tellme(function dToD(d: Developer): Developer {
	return new Developer();
});

// Developer => Developer 에다가 Person => Developer 를 할당하는 경우
tellme(function pToD(d: Person): Developer {
	return new Developer();
});

// Developer => Developer 에다가 StartupDeveloper => Developer 를 할당하는 경우
tellme(function sToD(d: StartupDeveloper): Developer {
	return new Developer();
});
```
### 4. 타입 별칭(Type Alias)
- Interface랑 비슷해 보입니다.
- Primitive, Union Type, Tuple, Function
- 기타 직접 작성해야하는 타입을 다른 이름을 지정할 수 있습니다.
- 만들어진 타입의 refer로 사용하는 것이지 타입을 만드는 것은 아닙니다.

```ts
// Aliasing Primitive
type MyStringType = string;
const str = 'world';

let myStr: MyStringType = 'hello';
myStr = str;

// Aliasing Union Type
let person: string | number = 0;
person = 'Mark';

type StringOrNumber = string | number;

let another: StringOrNumber = 0;
another = 'Anna';
/*
1. 유니온 타입은 A도 가능하고 B도 가능한 타입
2. 길게 쓰는걸 짧게
*/

// Aliasing Tuple
let person: [string, number] = ['Mark', 35];

type PersonTuple = [string, number];

let another: PersonTuple = ['Anna', 24];
// 1. 튜플 타입에 별칭을 줘서 여러군데서 사용할 수 있게 한다.

// Aliasing Function
type EatType = (food: string) => void;
```