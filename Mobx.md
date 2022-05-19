# Mobx

## 상태관리 라이브러리

- Simple - No Boilerplate
- Action - Derivative를 바꾸는 유일한 수단
- Reactive Programming - Observable / Observer

---

- with React - re-render issue(small component)
- makeAutoObservable - makeObservable을 보다 쉽게
- actions - runInAction / flow

---

- Computed - getter pure
- reaction - side effect
- reactive - observable 인 것이 바뀔때

```js
// ObservableTodoStore.js
import { action, autorun, computed, makeObservable, observable } from "mobx";

class ObservableTodoStore {
  todos = [];
  pendingRequests = 0;

  constructor() {
    makeObservable(this, {
      todos: observable,
      pendingRequests: observable,
      completedTodosCount: computed,
      report: computed,
      addTodo: action,
    });
    autorun(() => console.log(this.report));
  }

  get completedTodosCount() {
    return this.todos.filter((todo) => todo.completed === true).length;
  }

  get report() {
    if (this.todos.length === 0) return "<none>";
    const nextTodo = this.todos.find((todo) => todo.completed === false);
    return (
      `Next todo: "${nextTodo ? nextTodo.task : "<none>"}". ` +
      `Progress: ${this.completedTodosCount}/${this.todos.length}`
    );
  }

  addTodo(task) {
    this.todos.push({
      task: task,
      completed: false,
      assignee: null,
    });
  }
}

export const observableTodoStore = new ObservableTodoStore();
```

```js
// MobxExample.jsx
import React from "react";
import { observableTodoStore } from "../app/ObservableTodoStore";
import { todoStore } from "../app/TodoStore";

export default function MobxExample() {
  const run = () => {
    todoStore.addTodo("read MobX tutorial");
    console.log(todoStore.report());

    todoStore.addTodo("try MobX");
    console.log(todoStore.report());

    todoStore.todos[0].completed = true;
    console.log(todoStore.report());

    todoStore.todos[1].task = "try MobX in own project";
    console.log(todoStore.report());

    todoStore.todos[0].task = "grok MobX tutorial";
    console.log(todoStore.report());
  };
  const runObs = () => {
    observableTodoStore.addTodo("read MobX tutorial");
    observableTodoStore.addTodo("try MobX");
    observableTodoStore.todos[0].completed = true;
    observableTodoStore.todos[1].task = "try MobX in own project";
    observableTodoStore.todos[0].task = "grok MobX tutorial";
  };
  return (
    <>
      <button onClick={run}>run code</button>
      <button onClick={runObs}>run Obs code</button>
    </>
  );
}
```
