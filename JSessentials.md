# Javascript Essentials
## Node.js
Node.js는 Chrome V8 Javascript엔진으로 빌드된 Javascript 런타임이다.

### 1. NPM(Node Package Manager)
NPM은 전 세계의 개발자들이 만든 다양한 기능(패키지, 모듈)들을 관리.
- npm i -D xxx: 개발용 의존성 패키지 설치
- npm i xxx: 일반 의존성 설치

### 2. 유의적 버전(Semantic Versioning, SemVer)
Major.Minor.Patch - xx.xx.x
- Major: 기존 버전과 호환되지 않는 새로운 버전.
- Minor: 기존 버전과 호환되는 새로운 기능이 추가된 버전.
- Patch: 기존 버전과 호환되는 버그 및 오타 등이 수정된 버전.
- ^: Major 버전 안에서 가장 최신 버전으로 업데이트 가능.

## JS 시작하기
### 1. 데이터 타입 확인
```javascript
console.log(typeof 'Hello world!') // string
console.log(typeof 123) // number
console.log(typeof true) // boolean
console.log(typeof undefined) // undefined
console.log(typeof null) // object
console.log(typeof {}) // object
console.log(typeof []) // object

function getType(data) {
	return Object.prototype.toString.call(data).slice(8, -1)
}

console.log(getType(123)) // Number
console.log(getType(false)) // Boolean
console.log(getType(null)) // Null
console.log(getType({})) // Object
console.log(getType([])) // Array
```

### 2. 산술, 할당 연산자
```javascript
// 산술 연산자(arithmetic operator)
console.log(1 + 2) // 3
console.log(5 - 7) // -2
console.log(3 * 4) // 12
console.log(10 / 2) // 5
console.log(7 % 5) // 2

// 할당 연산자(assignment operator)
let a = 2
// a = a + 1
a += 1
```

### 3. 비교, 논리 연산자
```javascript
// 비교 연산자(comparison operator)
const a = 1
const b = 1

console.log(a === b) // 일치 연산자
console.log(a !== b) // 불일치 연산자
console.log(a < b)
console.log(a > b)
console.log(a >= b)
console.log(a <= b)

// 논리 연산자(logical operator)
const a = 2 === 2
const b = 'AB' === 'AB'
const c = true

console.log(a && b) // &&: and연산자, 전부 true일 때 true
console.log(a || b) // ||: or연산자, 하나라도 true면 true
console.log(!a) // !: Not연산자, true면 false를 반환하고 false면 true를 반환

// 삼항 연산자(ternary operator)
const a = 1 < 2
if (a) {
	console.log('참')
} else {
	console.log('거짓')
}

console.log(a ? '참' : '거짓')
```

### 4. 조건문
```javascript
function random () {
	return Math.floor(Math.random() * 10)
}

// 조건문(If statement)
const a = random()

if (a === 0) {
	// a가 0이면 출력
	console.log('a is 0')
} else if (a === 2) {
	// a가 2면 출력
	console.log('a is 2')
} else {
	// a가 0이 아니면 출력
	console.log('rest...')
}

// 조건문(Switch statement)
switch (a) {
	case 0:
		console.log('a is 0')
		break
	case 2:
		console.log('a is 2')
		break
	default:
		console.log('rest...')
}
```

### 5. 반복문
```javascript
// 반복문(For statement)
// for (시작조건; 종료조건; 변화조건) {}

for (let i = 0; i < 3; i += 1) {
	console.log(i)
}
```

### 6. 변수 유효범위
```javascript
// 변수 유효범위(Variable Scope)
// var 함수 레벨 유효범위를 가짐.
// let, const는 블록 레벨 유효범위를 가짐.
function scope () {
	console.log(b) // undefined
	if (true) {
		console.log(a) // undefined
		const a = 123
		var b = 123
		console.log(a) // 123
	}
	console.log(a) // a is not defined
	console.log(b) // 123
}
scope()
```

### 7. 형 변환
```javascript
// 형 변환(Type conversion)
// Truthy(참 같은 값): true, {}, [], 1, 2, 3, 'false', ...
// Falsy(거짓 같은 값): false, '', null, undefined, 0, NaN
const a = 1
const b = '1'

```

## JS 함수
### 1. 화살표 함수
```javascript
// () => {} vs function () {}
const double = function (x) {
	return x * 2
}
console.log('double: ', double(7))

const doubleArrow = (x) => {
	return x * 2
}
console.log('doubleArrow', doubleArrow(7))
```

### 2. IIFE
```javascript
// 즉시실행함수 Immediately-Invoked Function Expression
const a = 7
function double () {
	console.log(a * 2)
}
double()

(function () {
	console.log(a * 2)
})();
```

### 3. 호이스팅
```javascript
// 함수 선언부가 유효범위 최상단으로 끌어올려지는 현상
const a = 7
double() 
function double () {
	console.log(a * 2)
}
```

### 4. 타이머 함수
```javascript
// setTimeout(함수, 시간): 일정 시간 후 함수 실행
// setInterval(함수, 시간): 시간 간격마다 함수 실행
// clearTimeout(): 설정된 Timeout 함수를 종료
// clearInterval(): 설정된 Interval 함수를 종료

const timer = setTimeout( () => {
	console.log('Heropy!')
}, 3000)

const h1El = document.querySelector('h1')
h1El.addEventListener('click', () => {
	clearTimeout(timer)
})
```

### 5. 콜백
```javascript
// 함수의 인수로 사용되는 함수
function timeout(cb) {
	setTimeout(() => {
		console.log('Heropy!')
		cb()
	}, 3000)
}
timeout(() => {
	console.log('Done!')
})
```

## JS 클래스
### 1. 생성자 함수(prototype)
```javascript
functino User (first, last) {
	this.firstName = first
	this.lastName = last
}
user.prototype.getFullName = function () {
	return `${this.firstName} ${this.lastName}`
}

//  인스턴스   생성자 함수
const heropy = new User('Heropy', 'Park')
const amy = new User('Amy', 'Clarke')
const neo = new User('Neo', 'Smith')

console.log(heropy.getFullName()) // Heropy Park
```

### 2. This
```javascript
// 일반 함수는 호출 위치에 따라 this 정의!
// 화살표 함수는 자신이 선언된 함수 범위에서 this 정의!
const heropy = {
	name: 'Heropy',
	normal: function () {
		console.log(this.name)
	},
	arrow: () => {
		console.log(this.name)
	}
}
heropy.normal() // Heropy
heropy.arrow() // undefined

function User(name) {
	this.name = name
}
User.prototype.normal = function () {
	console.log(this.name)
}
User.prototype.arrow = () => {
	console.log(this.name)
}

const heropy = new User('Heropy')

heropy.normal() // Heropy
heropy.arrow()  // undefined
```

### 3. ES6 Classes
```javascript
class User {
	constructor(first, last) {
		this.firstName = first
		this.lastName = last
	}
	getFullName() {
		return `${this.firstName} ${this.lastName}`
	}
}
```

### 4. 상속
```javascript
class Vehicle {
	constructor(name, wheel) {
		this.name = name
		this.wheel = wheel
	}
}

// Vehicle의 내용을 Bicycle에 상속
class Bicycle extends Vehicle {
	constructor(name, wheel) {
		// super는 Vehicle을 가리킴
		super(name, wheel)
	}
}

// Vehicle의 기본 로직에 내용을 추가 할 수 있다.
class Car extends Vehicle {
	constructor(name, wheel, license) {
		super(name, wheel)
		this.license = license
	}
}
```
