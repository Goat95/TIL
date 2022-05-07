# React 맛보기

## 1. React

- as 라이브러리
  - 라이브러리: 라이브러리는 개발 편의를 위한 도구의 모음
  - 프레임워크: 프레임워크는 기반 구조까지 잡혀있음
- 생태계
  - 관련 라이브러리(도구)가 많고,
  - 문제를 해결할 방법을 찾기가 쉽고(stackover flow),
  - 나와 같은 고민을 하는/했던 사람이 많다.
  - 실무에서 사용할 확률이 높다.
- 기술적 근간
  - 많은 사람들에게 사랑받고 있다고해서 기술적 근간이 좋다는 것은 아니다.
  - 기술적으로 확실한 장점이 있다. Virtual DOM/JSX/Flux/Functional Programming
  - 새로운 기술을 배우는 시작점으로 좋다.
- with 라이브러리
  - 리액트를 풍성하게 해주는 라이브러리들이 많고,
  - 새로운 좋은 라이브러리들이 계속 나오고 있다.

## 2. DOM 다루기 Element 생성하기

- DOM(Document Object Model) - 문서를 논리 트리로 표현한다.
  Vanilla JS - 순수 자바스크립트, 특정 라이브러리나 프레임워크를 사용하지 않은 그 자체의 자바스크립트
- CDN(Content Delivery Network) - 웹에서 사용되는 다양한 컨텐츠(리소스)를 저장하여 제공하는 시스템.

```html
<!DOCTYPE html>
<html lang="en">
  <body>
    <script
      crossorigin
      src="https://unpkg.com/react@17/umd/react.development.js"
    ></script>
    <script
      crossorigin
      src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"
    ></script>
    <div id="root"></div>
    <script>
      const rootElement = document.getElementById("root");
      const element = React.createElement("h1", { children: "Hello, world!" });
      ReactDOM.render(element, rootElement);
    </script>
  </body>
</html>
```

## 3. JSX과 Babel, JSX 다루기

- JSX - 문자도 HTML도 아닌 JavaScript의 확장 문법

```
const element = React.createElement("h1", { children: "Hello, world!"});

const element = <h1>Hello, world!</h1>;
```

- Babel - JavaScript Compiler

```html
<!DOCTYPE html>
<html lang="en">
  <body>
    <script
      crossorigin
      src="https://unpkg.com/react@17/umd/react.development.js"
    ></script>
    <script
      crossorigin
      src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"
    ></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <div id="root"></div>
    <script type="text/babel">
      const rootElement = document.getElementById("root");
      const text = "Hello, world!";
      const titleClassName = "title";
      const props = { className: titleClassName, children: text };
      const element = <h1 {...props} />;
      ReactDOM.render(element, rootElement);
    </script>
  </body>
</html>
```

## 4. 멀티 Element 생성하기

- Fragment - React.Fragment or <></>

```html
<script type="text/babel">
  const rootElement = document.getElementById("root");
  const element = (
    <React.Fragment
      children={
        [
          React.createElement("h1", null, "hi");
          // <h1>hi</h1>
          React.createElement("h3", null, "bye");
          // <h3>bye</h3>
          React.createElement("h5", null, "children");
          // <h5>children</h5>
        ]
      }
    />
  );
  ReactDOM.render(element, rootElement);
</script>
```

## 5. Element 찍어내기

- Function - 재사용 가능한 Element
- Custom Element - Upper case
- Children 제한 - 없음

```html
<script type="text/babel">
  const rootElement = document.getElementById("root");
  const Paint = ({ title, description }) => {
    return (
      <>
        <h1>{title}</h1>
        <h3>{description}</h3>
      </>
    );
  };
  const element = (
    <>
      <Paint title="Good" description="good" />
      <Paint title="Bad" description="bad" />
      <Paint title="SoSo" description="soso" />
    </>
  );
  ReactDOM.render(element, rootElement);
</script>
```

## 6. JS와 JSX 섞어쓰기

- Interpolation - 이미 HTML에서 쓰고 있었다.

```html
<script type="text/babel">
  const rootElement = document.getElementById("root")
  const Text = ({ text }) => {
    return (
      // JavaScript 문법과 JSX 문법이 조건문안에 들어가 있다.
      if (text.charAt(0) === text.charAt(0).toUpperCase()) {
        return <h1>{text}</h1>;
      } else {
        return <h3>{text}</h3>;
      }
    );
  }
  const element = (
    <>
      <Text text="Text" />
      <Text text="text" />
    </>
  );
  ReactDOM.render(element, rootElement);
</script>
```

## 7. 리액트의 리랜더링

- 바닐라 JS - 변경으로 인해 Element를 다시 그림
- React - 변경된 부분만 다시 그림
- React 앨리먼트는 불변객체(immutable)입니다.
- 앨리먼트 타입이 바뀌면 이전 앨리먼트는 버리고 새로 그린다.
- 앨리먼트 타입이 같다면 props를 비교해서 변경사항을 반영한다.(Reconciliation)
- Virtual Dom - 비교시 활용

## 8. 이벤트 핸들러 써보기

- 바닐라 JS - on{event} / addEventListener
- React - on{Event}
- Object.assign - 객체 내용 복사
- 전역 변수 변경 - ReactDOM.render

```html
<script type="text/babel">
  const rootElement = document.getElementById("root");
  const handleClick = () => alert("pressed");
  const element = <button onCLick={handleClick}>Press</button>;
  ReactDOM.render(element, rootElement);
</script>
```

```html
<script type="text/babel">
  const rootElement = document.getElementById("root");
  const state = { keyword: "", typing: false, result: "" };

  const App = () => {
    function handleChange(event) {
      setState({ typing: true, keyword: event.target.value });
    }

    function handleClick() {
      setState({
        typing: false,
        result: `we find results of ${state.keyword}`,
      });
    }
    return (
      <>
        <input onChange={handleChange} />
        <button onClick={handleClick}>search</button>
        <p>{state.typing ? `Looking for ${state.keyword}...` : state.result}</p>
      </>
    );
  };

  function setState(newState) {
    Object.assign(state, newState);
    render();
  }

  function render() {
    ReactDOM.render(<App />, rootElement);
  }
  render();
</script>
```

## 9. 컴포넌트 상태 다루기

- 컴포넌트 - 앨리먼트의 집합
- useState - 상태값을 관리해주는 훅

```html
<script type="text/babel">
  const rootElement = document.getElementById("root");

  const App = () => {
    const [keyword, setKeyword] = React.useState("");
    const [result, setResult] = React.useState();
    const [typing, setTyping] = React.useState(false);

    function handleChange(event) {
      setKeyword(event.target.value);
      setTyping(true);
    }

    function handleClick() {
      setTyping(false);
      setResult(`we find results of ${keyword}`);
    }
    return (
      <>
        <input onChange={handleChange} />
        <button onClick={handleClick}>search</button>
        <p>{typing ? `Looking for ${keyword}...` : result}</p>
      </>
    );
  };
</script>
```

## 10. 컴포넌트 사이드 이펙트 다루기

- 사이드 이펙트(부작용) - 부수 효과
- useState - lazy initialize
- useEffect - dependency array

```html
<script type="text/babel">
  const rootElement = document.getElementById("root");

  const App = () => {
    const [keyword, setKeyword] = React.useState(() => {
      return windwo.localStorage.getItem("keyword");
    });
    const [result, setResult] = React.useState("");
    const [typing, setTyping] = React.useState(false);

    console.log("render");

    // keyword가 바뀔 때만 리렌더링 하고 싶을 때
    React.useEffect(() => {
      console.log("effect");
      window.localStorage.setItem("keyword", keyword);
    }, [keyword]);

    function handleChange(event) {
      setKeyword(event.target.value);
      setTyping(true);
    }

    function handleClick() {
      setTyping(false);
      setResult(`we find results of ${keyword}`);
    }
    return (
      <>
        <input onChange={handleChange} value={keyword} />
        <button onClick={handleClick}>search</button>
        <p>{typing ? `Looking for ${keyword}...` : result}</p>
      </>
    );
  };
</script>
```
