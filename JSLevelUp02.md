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

## 정규표현식(RegExp)
정규표현식이란 문자열을 검색하고 대체하는 데 사용 가능한 일종의 형식 언어입니다.  
정규표현식은 크게 다음과 같은 역할을 수행합니다.  
1. 문자 검색(search)
2. 문자 대체(replace)
3. 문자 추출(extract)

```js
// 예제 문자
const str = `
010-1234-5678
thesecon@gmail.com
https://www.omdbapi.com/?apikey=7035c60c&s=frozen
The quick brown fox jumps over the lazy dog.
abbcccdddd
`
```

### 1. 정규식 생성
```js
// 생성자
new RegExp('표현', '옵션')
new RegExp('[a-z]', 'gi')

// 리터럴
/표현/옵션
/[a-z]/gi

const regexp = new RegExp('the', 'gi')
const regexp = /the/gi
```

### 2. 메소드

메소드 | 문법 | 설명
--|--|--
test | `정규식.test(문자열)` | 일치 여부(Boolean) 반환
match | `문자열.match(정규식)` | 일치하는 문자의 배열(Array) 반환
replace | `문자열.replace(정규식, 대체문자)` | 일치하는 문자를 대체

```js
const regexp = /fox/gi
console.log(regexp.test(str)
console.log(str.replace(regexp, 'AAA'))
```

### 3. 플래그(옵션)

플래그 | 설명
--|--
g | 모든 문자 일치(global)
i | 영어 대소문자를 구분 않고 일치(ignore case)
m | 여러 줄 일치(multi line)

### 4. 패턴(표현)

패턴 | 설명
--|--
^ab | 줄(Line) 시작에 있는 ab와 일치
ab$ | 줄(Line) 끝에 있는 ab와 일치
. | 임의의 한 문자와 일치
a&verbar;b | a 또는 b와 일치
ab? | b가 없거나 b와 일치
{3} | 3개 연속 일치
{3, } | 3개 이상 연속 일치
{3, 5} | 3개 이상 5개 이하(3~5개) 연속 일치
[abc] | a 또는 b 또는 C
[a-z] | a부터 z 사이의 문자 구간에 일치(영어 소문자)
[A-Z] | A부터 Z사이의 문자 구간에 일치(영어 대문자)
[0-9] | 0부터 9 사이의 문자 구간에 일치(숫자)
[가-힣] | 가부터 힣 사이의 문자 구간에 일치(한글)
\w | 63개 문자(word, 대소영문52개 + 숫자10개 + _ )에 일치
\b | 63개 문자에 일치하지 않는 문자 경계(Boundary)
\d | 숫자(Digit)에 일치
\s | 공백(Space, Tab 등)에 일치
(?=) | 앞쪽 일치(Lookahead)
(?<=) | 뒤쪽 일치(Lookbehind)

```js
console.log(str.match(/d$/gm))
console.log(str.match(/^t/gim))
console.log(str.match(/h..p/g)
console.log(str.match(/fox|dog/g)
console.log(str.match(/https?/g)
console.log(str.match(/d{2}/g)
console.log(str.match(/\b\w{2,3}\b/g)
console.log(str.match(/\w/g)
```
