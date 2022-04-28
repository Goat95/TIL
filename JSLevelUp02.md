# Javascript Level Up 
## JS 데이터 실습
### 1. 가져오기, 내보내기
```javascript
import _ from 'lodash' // From `node_modules`

import checkType from './getType' // getType.js
export default function(data) {
	return Object.prototype.toString.call(data).slice(8, 12)
}

// default 키워드를 사용하지 않았을 때 중괄호로 묶어서 불러야 한다.
import { random } from './getRandom' // getRandom.js
export function	random() {
	return Math.floor(Math.random() * 10)
}

console.log(_.camelCase('the hello world'))
console.log(checkType([1, 2, 3]))
console.log(random(), random())
```

### 2. JSON
```javascript
// JSON (Javascript Object Notation)
// 자바스크립트 객체 표기법
const user = {
	name: 'HEROPY',
	age: 85,
	emails: [
		'thesecon@gmail.com',
		'neo@zillinks.com'
	]
}
console.log('user', user)

// 객체를 string으로 변환
const str = JSON.stringify(user)
console.log('str', str) 
console.log(typeof str) // string

// string을 객체로 변환
const obj = JSON.parse(str)
console.log('obj', obj)
```

### 3. Storage
```javascript
const user = {
	name: 'HEROPY',
	age: 85,
	emails: [
		'thesecon@gmail.com',
		'neo@zillinks.com'
	]
}
// 브라우저에 저장된 user 객체를 받아오고, 가져오고, 삭제한다.
localStorage.setItem('user', JSON.stringify(user))
console.log(JSON.parse(localStorage.getItem('user')))
localStorage.removeItem('user')
```
