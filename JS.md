# JS 선행학습
## 개요
- 표기법:
	- dash-case: 단어와 단어 사이를 '-'로 구분하는 표기법
	- snakecase: 단어와 단어 사이를 '-'로 구분하는 표기법
	- camelCase: 첫 글자는 소문자로 시작하고 다음 단어는 대문자로 시작하는 표기법
	- PascalCase: 첫 글자도 대문자로 시작하고, 다음 단어도 대문자로 시작하는 표기법
- Zero-based Numbering: 0 기반 번호 매기기! 특수한 경우를 제외하고 0부터 숫자를 시작합니다.
```javascript
let fruits = ['Apple', 'Banana', 'Cherry'];

console.log(fruits[0]); // 'Apple'
console.log(fruits[1]); // 'Banana'
console.log(fruits[2]); // 'Cherry'

console.log(new Date('2021-01-30').getDay()); // 6, 토요일
console.log(new Date('2021-01-31').getDay()); // 0, 일요일
console.log(new Date('2021-02-01').getDay()); // 1, 월요일
```
- 주석
```javascript
// 한 줄 메모
/**
* 여러 줄
* 메모 1
* 메모 2
*/
```

## 데이터 종류(자료형)
String, Number, Boolean, Undefined, Null, Object, Array
```javascript
// String(문자 데이터)
// 따옴표를 사용합니다.
let myName = "HEROPY";
let hello = `Hello ${myName}?!`

console.log(myName); // HEROPY
console.log(hello); // Hello HEROPY?!

// Number(숫자 데이터)
// 정수 및 부동소수점 숫자를 나타냅니다.
let number = 123;
let opacity = 1.57;

console.log(number); // 123
console.log(opacity); // 1.57

// Boolean(불린 데이터)
// true, false 두 가지 값밖에 없는 논리 데이터입니다.
let checked = true;
let isShow = false;

// Undefined
// 값이 할당되지 않은 상태를 나타냅니다.
let undef;
let obj = { abc: 123 };

console.log(undef); // undefined
console.log(obj.xyz); // undefined

// Null
// 어떤 값이 의도적으로 비어있음을 의미합니다.
let empty = null;

// Object(객체 데이터)
// 여러 데이터를 Key: Value 형태로 저장합니다.
let user = {
	// key: value
	name: 'HEROPY',
	age: 85,
	isValid: true
};

console.log(user.name); // HEROPY
console.log(user.age); // 85
console.log(user.isValid); // true

// Array(배열 데이터)
// 여러 데이터를 순차적으로 저장합니다.
let fruits = ['Apple', 'Banana', 'Cherry'];

console.log(fruits[0]); // 'Apple'
```

## 변수, 예약어
- 변수: 데이터를 저장하고 참조(사용)하는 데이터의 이름.
```javascript
// 재사용이 가능!
// 변수 선언!
let a = 2;
let b = 5;

console.log(a + b); // 7
console.log(a - b); // -3

// 값(데이터)의 재할당 가능!
let a = 12;
console.log(a); // 12

a = 999;
console.log(a); // 999

// 값(데이터)의 재할당 불가능!
const a = 12;
console.log(a); // 12

a = 999;
console.log(a); // TypeError: Assignment to constant variable.
```

- 예약어: 특별한 의미를 가지고 있어, 변수나 함수 이름 등으로 사용할 수 없는 단어
```javascript
let this = 'Hello!'; // SyntaxError
let if = 123; // SyntaxError
```

## 함수
함수: 특정 동작(기능)을 수행하는 일부 코드의 집합(부분), function
```javascript
// 함수 선언
function helloFunc() {
	// 실행 코드
	console.log(1234);
}

// 함수 호출
helloFunc(); // 1234

// 반환
function returnFunc() {
	return 123;
}
let a = returnFunc();
console.log(a); // 123

// 매개변수
function sum(a, b) { // a와 b는 매개변수(Parameters)
	return a + b;
}

// 재사용!
let a = sum(1, 2); // 1과 2는 인수(Arguments)
let b = sumb(7, 12);

console.log(a, b); // 3, 19

// 기명(이름이 있는) 함수
// 함수 선언문
function hello() {
	console.log('Hello!');
}

// 익명(이름이 없는) 함수
// 함수 표현식
let world = function() {
	console.log('World~');
}

// 객체 데이터
const heropy = {
	name: 'HEROPY',
	age: 85,
	// 메소드(Method)
	getName: function() {
		return this.name
	}
};

const hisName = heropy.getName();
console.log(hisName); // HEROPY
```

## 조건문
조건문: 조건의 결과(truthy, falsy)에 따라 다른 코드를 실행하는 구문
```javascript
let isShow = true;
let checked = false;

if (isShow) {
	console.log('Show!'); // Show!
}

if (checked) {
	console.log('Checked!'); // 실행X
}

// true면 if 구문 안이 실해 false면 else 구문 안이 실행된다.
if (isShow) {
	console.log('Show!');
} else {
	console.log('Hide?');
}
```

## DOM API(Document Object Model, Application Programming Interface)
DOM API: 자바스크립트에서 HTML을 제어하는 여러가지 명령들.
```javascript
// HTML 요소(Element) 1개 검색/찾기
const boxEl = document.querySelector('.box');

// HTML 요소에 적용할 수 있는 메소드!
boxEl.addEventListener();

// 인수(Arguments)를 추가 가능!
boxEl.addEventListener(1, 2);

// 1 - 이벤트(Event, 상황)
boxEl.addEventListener('click', 2);

// 2 - 핸들러(Handler, 실행할 함수)
boxEl.addEventListenre('click', function () {
	console.log('Click~!');
});

// 요소의 클래스 정보 객체 활용!
boxEl.classList.add('active');
let isContains = boxEl.classList.contains('active');
console.log(isContains); // true

boxEl.classList.remove('active');
isContains = boxEl.classList.contains('active');
console.log(isContains); // false

// HTML 요소(Element) 모두 검색/찾기
const boxEls = document.querySelectorAll('.box');

// 찾은 요소들 반복해서 함수 실행!
// 익명 함수를 인수로 추가!
boxEls.forEach(function () {});

// 첫 번째 매개변수(boxEl): 반복 중인 요소.
// 두 번째 매개변수(index): 반복 중인 번호.
boxEls.forEach(function (boxEl, index) {});

// 출력!
boxEls.forEach(function (boxEl, index) {
	boxEl.classList.add(`order-${index + 1}`);
	console.log(index, boxEl);
});

// Getter, 값을 얻는 용도
const boxEl = document.querySelector('.box');
console.log(boxEl.textContent); // Box!!

// Setter, 값을 지정하는 용도
boxEl.textContent = 'HEROPY?!';
console.log(boxEl.textContent); // HEROPY?!
```

## 메소드 체이닝
```javascript
const a = 'Hello~';
// split: 문자를 인수 기준으로 쪼개서 배열로 반환.
// reverse: 배열을 뒤집기.
// join: 배열을 인수 기준으로 문자로 병합해 반환.
const b = a.split('').reverse().join(''); // 메소드 체이닝...

console.log(a); // Hello~
console.log(b); // ~olleH
```
