# Javascript Level Up
## JS 데이터
### 1. 문자
- String.prototype.indexOf(): 호출한 String 객체에서 주어진 값과 일치하는 첫  
번째 인덱스를 반환합니다. 일치하는 값이 없으면 -1을 반환합니다.
```javascript
const result = 'Hello world!'.indexOf('world')
console.log(result) // 6
```
- String.prototype.slice(): 문자열의 일부를 추출하면서 새로운 문자열을 반환합니다.
```javascript
const str = 'Hello world!'
console.log(str.slice(0, 3)) // Hel
```
- String.prototype.replace(): 어떤 패턴에 일치하는 일부 또는 모든 부분이 교체된 새로운 문자열을 반환합니다.
```javascript
const str = 'Hello world!'
console.log(str.replace('world', 'Heropy')) // Hello Heropy!
```
- String.prototype.trim(): 문자열 양 끝의 공백을 제거합니다.
```javascript
const str = '     Hello world  '
console.log(str.trim()) // Hello world
```

### 2. 숫자와 수학
Math: 수학적인 상수와 함수를 위한 속성과 메서드를 가진 내장 객체입니다. 
```javascript
const pi = 3.14159265358979
console.log(pi)

const str = pi.toFixed(2)
console.log(str) // 3.14
console.log(typeof str) // string

const integer = parseInt(str) 
const float = parseFloat(str)
console.log(integer) // 3
console.log(float) // 3.14
console.log(typeof integer, typeof float) // number number

// 절대값 반환
console.log('abs: ', Math.abs(-12)) // abs: 12

// 인수로 들어온 숫자 데이터 중 가장 작은 값 반환
console.log('min: ', Math.min(2, 8)) // min: 2

// 인수로 들어온 숫자 데이터 중 가장 큰 값 반환
console.log('max: ', Math.max(2, 8)) // max: 8

// 올림한 값 반환
console.log('ceil: ', Math.ceil(3.14)) // ceil: 4

// 내림한 값 반환
console.log('floor: ', Math.floor(3.14)) // floor: 3

// 반올림한 값 반환
console.log('round: ', Math.round(3.14)) // round: 3

// 랜덤한 숫자 반환
console.log('random: ', Math.random()) // random: 무작위 숫자 
```

### 3. 배열
```javascript
// .length
const numbers = [1, 2, 3, 4]
const fruits = ['Apple', 'Banana', 'Cherry']

console.log(numbers.length) // 4
console.log(fruits.length) // 3

// .concat()
console.log(numbers.concat(fruits)) // [1, 2, 3, 4, "Apple", "Banana", "Cherry"]

// .forEach()
fruits.forEach(function (element, index, array) {
	console.log(element, index, array)
})

// .map()
const b = fruits.map(function (fruit, index) {
	return `${fruit} - ${index}`
})
console.log(b) // ["Apple-0", "Banana-1", "Cherry-2"]

// .filter()
const a = numbers.filter(number => {
	return number < 3
})
console.log(a) // [1, 2]

// .find() .findIndex()
const a = fruits.find(fruit => {
	return /^B/.test(fruit)
})
console.log(a) // Banana

const b = fruits.findIndex(fruit => {
	return /^C/.test(fruit)
})
console.log(b) // 2

// .includes()
const a = numbers.includes(3)
console.log(a) // true

// .push .unshift() 
// 원본 수정됨 주의!
numbers.push(5)
console.log(numbers) // [1, 2, 3, 4, 5]
numbers.unshift(0)
console.log(numbers) // [0, 1, 2, 3, 4, 5]

// .reverse()
// 원본 수정됨 주의!
numbers.reverse() // [4, 3, 2, 1]

// .splice()
// 원본 수정됨 주의!
numbers.splice(2, 1) // [1, 2, 4]
```

### 4. 객체
```javascript
const userAge = {
	// key: value
	name: 'Heropy',
	age: 85
}
const userEmail = {
	name: 'Heropy',
	email: 'thesecon@gmail.com'
}

const target = Object.assign({}, userAge, userEmail)
console.log(target)
console.log(userAge)
console.log(target === userAge) // false

const user = {
	name: 'Heropy',
	age: 85,
	email: 'thesecon@gmail.com'
}
const keys = Object.keys(user)
console.log(keys) // ['name', 'age', 'email']
```

### 5. 구조 분해 할당
```javascript
// 구조 분해 할당(Destructuring assignment)
// 비구조화 할당

const fruits = ['Apple', 'Banana', 'Cherry']
const [a, b, c, d] = fruits
console.log(a, b, c, d) // Apple Banana Cherry undefined
```

### 6. 전개 연산자
```javascript
// 전개 연산자(Spread)
const fruits = ['Apple', 'Banana', 'Cherry']
console.log(...fruits) // Apple Banana Cherry

function toObject(a, b, c) {
	return {
		a: a,
		b: b,
		c: c
	}
}
console.log(toObject(...fruits)) // {a: "Apple", b: "Banana", c: "Cherry"}
```

### 7. 불변성
```javascript
// 데이터 불변성(Immutability)
// 원시 데이터: String, Number, Boolean, undefined, null
// 한 번 메모리에 만들어지면 불변한다.
let a = 1
let b = 4
console.log(a, b, a === b) // 1 4 false
b = a
console.log(a, b, a === b) // 1 1 true
a = 7
console.log(a, b, a === b) // 7 1 false
let c = 1
console.log(b, c, b === c) // 1 1 true

// 참조형 데이터: Object, Array, Function
// 같은 메모리를 바라보는 여러 변수가 있을 때 한 쪽 변수를 수정하게 되면
// 다른 값에서 의도치 않게 바껴줘 있을 수 있다.
let a = { k: 1 }
let b = { k: 1 }
console.log(a, b, a === b) // {k:1} {k:1} false
a.k = 7
b = a
console.log(a, b, a === b) // {k:7} {k:7} true
a.k = 2
console.log(a, b, a === b) // {k:2} {k:2} true
let c = b
console.log(a, b, c, a === c) // {k:2} {k:2} {k:2} true
a.k = 9
console.log(a, b, c, a === c) // {k:9} {k:9} {k:9} true
```

### 8. 얕은 복사와 깊은 복사
```javascript
const user = {
	name: 'Heropy',
	age: 85,
	emails: ['thesecon@gmail.com']
}
const copyUser = user
console.log(copyUser === user) // true

// 메모리 주소가 같기 때문에 user의 값을 바꾸면 copyUser 값도 바뀐다.
user.age = 22
console.log('user', user) // {name: "Heropy", age: 22, emails: Array(1)}
console.log('copyUser', copyUser) // {name: "Heropy", age: 22, emails: Array(1)}

// Object.assign() 을 통한 얕은  복사 
const copyUser = Object.assign({}, user)
console.log(copyUser === user) // false

// 전개 연산자를 통한 얕은 복사
const copyUser = {...user}
console.log(copyUser === user) // false 

// user 객체만 표면적으로 복사한거지 객체안에 또다른 참조데이터는 복사X
user.emails.push('neo@zillinks.com')
console.log(user.emails === copyUser.emails) // true

// lodash 패키지를 통해 깊은 복사
import _ from 'lodash'
const copyUser = _.cloneDeep(user)
console.log(user.emails === copyUser.emails) // false
```
