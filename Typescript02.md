# TypeScript Essentials
## TypeScript Compiler
### 1. Compilation Context
컴파일 컨텍스트는 기본적으로 TypeScript가 유효한 것과 그렇지 않은 것을 결정하기 위해 구문 분석하고 분석할 파일 그룹화에 대한 멋진 용어입니다.<br> 어떤 파일에 대한 정보와 함께 컴파일 컨텍스트에는 어떤 컴파일러 옵션에 대한 정보가 포함됩니다.<br> 이 논리적 그룹을 정의하는 좋은 방법(프로젝트라는 용어도 사용하고 싶습니다)은 tsconfig.json 파일을 사용하는 것입니다.

### 2. tsconfig schema
#### 최상위 프로퍼티
- compileOnSave
- extends
- compileOptions
- files
- include
- exclude
- references

### 3. compileOnSave
파일을 save 하면 compile하겠다.
- true/false(default false)
- 누가??
  - Visual Studio 2015 with TypeScript 1.8.4 이상
  - atom-typescript 플러그인

### 4. extends
- 파일(상대) 경로명: string
- TypeScript 2.1 New Spec

### 5. files, include, exclude
- 셋다 설정이 없으면, 전부다 컴파일
- files
  - 상대 혹은 절대 경로의 리스트 배열입니다.
  - exclude 보다 쎕니다.
- include, exclude
  - glob 패턴(마치 .gitignore)
  - include
    - exclude 보다 약합니다.
    - *같은걸 사용하면, .ts/.tsx/.d.ts만 include(allowJS)
  - exclude
    - 설정 안하면 4가지(node_modules, bower_components, jspm_packages, &lt;outDir&gt;)를 default로 제외합니다.
    - &lt;outDir&gt;은 항상 제외합니다.(include에 있어도)

### 6. compileOptions - typeRoots, types
@types
- TypeScript 2.0 부터 사용 가능해진 내장 type definition 시스템
- 아무 설정 안하면?
  - node_modules/@types 라는 모든 경로를 찾아서 사용
- typeRoots를 사용하면?
  - 배열 안에 들어있는 경로들 아래서만 가져옵니다.
- types를 사용하면?
  - 배열 안의 모듈 혹은 ./node_modules/@types/ 안의 모듈 이름에서 찾아옵니다.
  - [] 빈 배열을 넣는다는건 이 시스템을 이용하지 않겠다는 것입니다.
- typeRoots와 types를 같이 사용하지 않습니다.

### 7. compileOptions - target과 lib
- target
  - 빌드의 결과물을 어떤 버전으로 할 것이냐
  - 지정을 안하면 es3입니다.
- lib
  - 기본 type definition 라이브러리를 어떤 것을 사용할 것이냐
  - lib를 지정하지 않을 때,
    - target이 'es3'이고, 디폴트로 lib.d.ts를 사용합니다.
    - target이 'es5'이면, 디폴트로 dom, es5, scripthost를 사용합니다.
    - target이 'es6'이면, 디폴트로 dom, es6, dom.iterable, scripthost를 사용합니다.
  - lib를 지정하면 그 lib 배열로만 라이브러리를 사용합니다.
    - 빈 [] => 'no definition found 어쩌구'

### 8. compileOptions - outDir, outFile, rootDir
- outFile: 모든 출력을 하나의 자바스크립트 파일로 묶는 파일을 지정합니다. 'declaration'이 true이면 모든 .d.ts 출력을 묶는 파일도 지정합니다.
- outDir: 내보낸 모든 파일에 대한 출력 폴더 지정.
- rootDir: 소스 파일 내에 루트 폴더를 지정하십시오.

### 9. compileOptions - strict
strict: 엄격하게 타입을 확인하는 옵션을 활성화 한다.
#### --noImplicitAny
명시적이지 않게 any 타입을 사용하여, 표현식과 선언에 사용하면, 에러를 발생.
```ts
function noImplicitAnyTestFunc(arg) {
  console.log(arg);
}
```
- 타입스크립트가 추론을 실패한 경우, any가 맞으면, any 라고 지정하라.
- 아무것도 쓰지 않으면, 에러를 발생
- 이 오류를 해결하면, any라고 지정되어 있지 않은 경우는 any가 아닌 것이다.(타입 추론이 되었으므로)
---
#### suppressImplicitAnyIndexErrors
noImplicitAny 사용할 때, 인덱스 객체에 인덱스 signature가 없는 경우 오류가 발생 하는데 이를 예외처리 합니다.
```ts
var obj = {
  bar: 10
};
obj['foo'] = 10; // error
obj['bar'] = 10; // okay
obj.baz = 10;
```
- obj['foo']로 사용할 때, 인덱스 객체라 판단하여, 타입에 인덱스 시그니처가 없는 경우, 에러를 발생시킵니다.
- 이때 suppressImplicitAnyIndexErrors 옵션을 사용하면, 이런 경우 예외로 간주하여, 에러를 발생시키지 않습니다.
---
#### --noImplicitThis
명시적이지 않게 any 타입을 사용하여, this 표현식에 사용하면, 에러를 발생합니다.
```ts
function noImplicitThisTestFunc(this, name: string, age: number) {
  this.name = name;
  this.age = age;
  return this;
}
```
- 첫번째 매개변수 자리에 this를 놓고, this에 대한 타입을 어떤 것이라도 표현하지 않으면, noImplicitAny가 오류를 발생시킨다.
- JavaScript에서는 매개변수에 this를 넣으면, 이미 예약된 키워드라 SyntaxError를 발생시킨다.
- call/apply/bind와 같이 this를 대체하여 함수 콜을 하는 용도로도 쓰입니다.
- 그래서 this를 any로 명시적으로 지정하는 것은 합리적입니다.
```ts
class NoImplicitThisTestClass {
  private _name: string;
  private _age: number;

  constructor(name: string, age: number) {
    this._name = name;
    this._age = age;
  }

  public print(this: NoImplicitThisTestClass) {
    console.log(this._name, this._age);
  }
}

new NoImplicitThisTestClass('Mark', 36).print();
```
- Class에서는 this를 사용하면서, noImplicitThis와 관련한 에러가 나지 않습니다.
- Class에서 constructor를 제외한 멤버 함수의 첫번째 매개변수도 일반 함수와 마찬가지로 this를 사용할 수 있습니다.
---
#### --strictNullChecks
- strictNullChecks 모드에서는, null 및 undefined 값이 모든 유형의 도메인에 속하지 않으며, 그 자신을 타입으로 가지거나, any 일 경우에만 할당이 가능합니다.
- 한 가지 예외는 undefined에 void 할당 가능
```ts
const a: number = null; // error
const b: string = undefined; // error
const c: number | null = null
const d: any = null;
const e: any = undefined;
const f: void = undefined;
```
- strictNullChecks를 적용하지 않으면,
  - 모든 타입은 null, undefined 값을 가질 수 있습니다.
  - string으로 타입을 지정해도, null 혹은 undefined 값을 할당할 수 있다는 것입니다.
- strictNullChecks를 적용하면,
  - 모든 타입은 null, undefined 값을 가질 수 없고, 가지려면 union type을 이용해서 직접 명시 해야 합니다.
  - any 타입은 null, undefined를 가집니다. 예외적으로 void 타입의 경우 undefined를 가집니다.
---
#### --strictFunctionTypes
함수 타입에 대한 bivariant 매개변수 검사를 비활성화합니다.
- 반환 타입은 공변적
- 인자 타입은 반공변적
- 그런데 타입스크립트에서 인자 타입은 공변적이면서 반공변적인게 문제!
- 이 문제를 해결하는 옵션이 strictFunctionTypes
```ts
const button = document.querySelector('#id') as HTMLButtonElement;
button.addEventListener('keydown', (e: MouseEvent) => {});
```
---
#### --strictPropertyInitialization
정의되지 않은 클래스의 속성이 생성자에서 초기화되었는지 확인합니다. <br>이 옵션을 사용하려면 --strictNullChecks를 사용하도록 설정해야 합니다.
- constructor에서 초기 값을 할당한 경우 => 정상
```ts
class Person {
  private _name: string;
  private _age: number;

  constructor(name: string, age: number) {
    this._name = name;
    this._age = age;
  }

  public print() {
    console.log(this._name, this._age);
  }
}
```
- constructor에서 안하는 경우
  - 보통 다른 함수로 이니셜라이즈 하는 경우(async 함수)
  - constructor에는 async를 사용할 수 없다.
```ts
class Person {
  private _name!: string;
  private _age!: number;

  public async initialize(name: string, age: number) {
    this._name = name;
    this._age = age;
  }
  public print() {
    console.log(this._name, this._age);
  }
}
```
---
#### --strictBindCallApply
- Function의 내장 함수인 bind/call/apply를 사용할 때, 엄격하게 체크하도록 하는 옵션입니다.
- bind는 해당 함수안에서 사용할 this와 인자를 설정해주는 역할을 하고, call과 apply는 this와 인자를 설정한 후, 실행까지 합니다.
- call과 apply는 인자를 설정하는 방식에서 차이점이 있습니다.
  - call은 함수의 인자를 여러 인자의 나열로 넣어서 사용하고, apply는 모든 인자를 배열 하나로 넣어서 사용 합니다.
---
#### --alwaysStrict
각 소스 파일에 대해 JavaScript의 strict mode로 코드를 분석하고, "엄격하게 사용"을 해제합니다.