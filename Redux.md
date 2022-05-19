# Redux

## 상태관리 라이브러리

- 전역 상태 관리 - VS 지역 상태 관리
- 단 방향 테이터(상태) 흐름 - Flux
- 구성 요소 - Store / Reducer / Action / Selector

- One way data flow

  - multiple components issue
  - Lifting state up
  - Extract shared state from the component tree
    ![one-way-data-flow](https://ko.redux.js.org/assets/images/one-way-data-flow-04fe46332c1ccb3497ecb04b94e55b97.png)

- Immutable

  - object / array
  - ...spread

- Terminology

  - action { type, payload }
  - reducer (state, action) => newState
  - store (state lives) created by passing reducer
  - dispatch only way to update state(pass in an action object)
  - selectors extract specific pieces of information from a store state

- Initial setup

  - store created by using reducer function
  - store calls root reducer once save initial state
  - UI first rendered

- Updates
  - Something happend / dispatch action
  - store run reducer with prev state & current action save new state
  - notifies all parts store has been updated / Each UI check update
  - need to changed UI re-render

---

- RTK - Redux 라이브러리들 조합
- 라이브러리들 - immer / saga / thunk / reselect
- Redux Dev Tools - Chrome extension

```js
// store.js
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "../features/counter/counterSlice";

export default configureStore({
  reducer: {
    counter: counterReducer,
  },
});
```

```js
// counterSlice.js
import { createSlice } from "@reduxjs/toolkit";

export const counterSlice = createSlice({
  name: "counter",
  initialState: {
    value: 0,
  },
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload;
    },
  },
});

export const { increment, decrement, incrementByAmount } = counterSlice.actions;

export default counterSlice.reducer;
```

```js
// Counter.js
import React from "react";
import { useDispatch, useSelector } from "react-redux";
import { decrement, increment, incrementByAmount } from "./counterSlice";

export default function Counter() {
  const count = useSelector((state) => state.counter.value);
  const dispatch = useDispatch();

  return (
    <div>
      <div>
        <button onClick={() => dispatch(increment())}>Increment</button>
        <span>{count}</span>
        <button onClick={() => dispatch(decrement())}>Decrement</button>
        <button onClick={() => dispatch(incrementByAmount(5))}>+5</button>
      </div>
    </div>
  );
}
```

---

- Hooks - useSelector / useDispatch
- API 통신 - 비동기 작업(RTK-Query)
- Redux-Thunk - Action으로 API 요청 / 결과 Store에 반영
