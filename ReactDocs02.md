# React 공식문서로 디테일 잡기(고급)

## Hooks

- Hooks 등장 - Class의 단점 보완 / 재사용성 강화
- Hook 사용 규칙 - 최상위 / 함수형 컴포넌트 / custom Hook
- Class의 state - 훅을 먼저 배웠기에 고민 할 필요 X

---

- useEffect - 데이터 fetch / 구독 / Dom 수정
- clean up - 구독과 구독해지를 한 공간에서
- dependency array - 필요한 변경시에만 effect 실행

---

- Custom Hook - 컴포넌트들에 반복되는 Hooks 묶기
- 다양한 Hooks - 필요한 타이밍에 참고해서 사용

## Composition

- Composition - 컴포넌트에 컴포넌트 담기
- 담는 방법 - Children / Custom

---

- typeof - type check
- 확장성 - 다양한 상황을 품을 수 있도록

## HOC

- HOC - Higher Order Component
- HOC - 함수를 받아서 함수를 리턴

## Memoization

- 메모이제이션 - 메모이제이션은 컴퓨터 프로그램이 동일한 계산을 반복해야 할 때, 이전에 계산한 값을 메모리에 저장함으로써 동일한 계산의 반복 수행을 제거하여 프로그램 실행 속도를 빠르게 하는 기술이다.
- React.memo - HOC / Props 비교하여 메모
- Profiler - 리액트 성능 분석 도구
- callback - useCallback
- value - useMemo

## Context

- 컴포넌트 트리 제약 - Props drilling의 한계 해소
- 재사용성 - Context를 사용하면 재사용하기 어려움
- API - createContext / Provider / Consumer
- useContext - Consumer 대체

## Portals

- createPortal - 부모 컴포넌트 DOM 트리로부터 벗어나기
- 이벤트 - Portal에 있더라도 Event는 트리로 전파

## Render Props

- render props - 무엇을 렌더링할 지 알려주는 함수
- render일 필요 - 없음, children도 되고 뭐든 됨
- PureComponent - props, state 비교하여 성능 최적화

## PropTypes

- 개발 모드에서만 동작 - 유효하지 않은 prop에 대한 경고
- custom - RegExp 등으로 사용자 정의 가능
- children 제한 - 원래 제약없던 갯수 제약 가능

## Reconciliation

- 루트부터 비교 - 무엇을 렌더링할 지 알려주는 함수
- 트리를 파괴 - 부모가 바뀌었다면 트리를 버린다
- Keys - 자식 재귀 처리 시 효율성 확보

---

- Virtual DOM - 실제 DOM과 동기화 할 가상 표현
- 재조정 - 실제 DOM과 Virtual DOM의 동기화
- React Fiber - 스택 reconciler 대체한 재조정 엔진

## React Dev Tool

- 개발자 도구 확장 - React에서 확인하고 싶은 것들
- 성능 측정 - Profiler
