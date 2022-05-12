# React 공식문서로 디테일 잡기

## 1. 공식문서를 보는 이유와 방법

- 공식문서 - 라이브러리 설명서
- 공식문서 읽기 - 리액트로 시작 후 반복 숙달

## 2. 환경 설정

- vscode - IDE
- node, npm, npx - create-react-app

## 3. JSX

- JSX - React.createElement 간편 표현식

## 4. Props

- Props - 컴포넌트에 전달되는 단일 객체
- 순수함수처럼 동작 - Props 자체를 수정해서는 안됨
- 컴포넌트 합성 - 여러 컴포넌트를 모아서
- 컴포넌트 추출 - 여러곳에서 사용되거나 / 복잡한 경우

## 5. State

- 컴포넌트 내의 상태 - 자신의 출력값을 변경
- Class component - State LifeCycle
- Functional component - 훅으로 관리
- 유의사항 - 직접 수정 X / 비동기적일 수 있음

## 6. 컴포넌트 생명주기

- constructor - state 초기화 및 메서드 바인딩
- componentDidMount - Dom 노드 초기화 및 데이터 fetch
- componentWillUnmount - 타이머 제거 및 요청 취소 및 구독 해제
- Functional Component - hook으로 대부분 구현 가능

## 7. 이벤트

- 합성 이벤트 - 인터페이스는 같지만 직접 대응되지 않음
- Bubble / Capture - Capture > target > Bubble
- return false - e.preventDefault() 해줘야 함

## 8. 조건부 렌더링

- if - if(condition){return A} else {return B}
- && - condition && A, falsy 주의
- 삼항연산자 - condition ? A : B
- 아예 안그리고 싶은 경우 - return null;

## 9. List

- map - 배열의 개별 요소를 순회
- default key - 안주면 react는 index를 쓴다(워닝 O)
- 고유성 - 형제 사이에서만 고유하면 됨
- key props - key는 props로 넘어가지 않음

## 10. Form

- Controlled Component - input의 value를 state로 관리
- 다중 입력 - event.target.name
- Uncontrolled Component - form element 자체의 내부 상태 활용
- defaultValue, ref - 기본값 / value 확인
