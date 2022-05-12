# React 맛보기

## 11. 커스텀 훅 만들기

- 반복 - 함수로 만든다.
- useState / useEffect 를 반복 - custom Hook으로 만든다.

```html
<script type="text/babel">
  const rootElement = document.getElementById("root");

  function useLocalStorage(itemName, value = "") {
    const [state, setState] = React.useState(() => {
      return windwo.localStorage.getItem(itemName) || value;
    });

    React.useEffect(() => {
      window.localStorage.setItem(itemName, state);
    }, [state]);

    return [state, setState];
  }

  const App = () => {
    const [keyword, setKeyword] = useLocalStorage("keyword");
    const [result, setResult] = useLocalStorage("result");
    const [typing, setTyping] = useLocalStorage("typing"false);

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

  ReactDOM.render(<App />, rootElement);
</script>
```

## 12. Hook Flow 이해하기

- hook flow - hook들의 호출 타이밍
- useState - setState시 prev이 주입된다

```html
<script type="text/babel">
  const rootElement = document.getElementById("root");

  const App = () => {
    console.log("App render start");
    const [show, setShow] = React.useState(() => {
      console.log("App useState");
      return false;
    });

    React.useEffect(() => {
      console.log("App useEffect, no deps");
    });
    React.useEffect(() => {
      console.log("App useEffect, empty deps");
    }, []);
    React.useEffect(() => {
      console.log("App useEffect, [show]");
    }, [show]);

    function handleClick() {
      // setState는 첫번째 인자로 이전 값을 받는다.
      setShow((prev) => !prev);
    }

    console.log("App render end");

    return (
      <>
        <button onClick={handleClick}>Search</button>
        {show ? (
          <>
            <input />
            <p></p>
          </>
        ) : null}
      </>
    );
  };

  ReactDOM.render(<App />, rootElement);
</script>
```

## 13. Hook Flow 이해하기2

- useEffect - render가 끝난 뒤
- update시 - useEffect clean up / uesEffect
- dependency array - 전달받은 값의 변화 있는 경우에만

```html
<script type="text/babel">
  const rootElement = document.getElementById("root");

  const Child = () => {
    console.log("   Child render start");
    const [text, setText] = React.useState(() => {
      console.log("   Child useState");
      return "";
    });

    React.useEffect(() => {
      console.log("   Child useEffect, no deps");

      return () => {
        console.log("   Child useEffect [Cleanup], no deps");
      };
    });
    React.useEffect(() => {
      console.log("   Child useEffect, empty deps");

      return () => {
        console.log("   Child useEffect [Cleanup], empty deps");
      };
    }, []);
    React.useEffect(() => {
      console.log("   Child useEffect, [text]");

      return () => {
        console.log("   Child useEffect [Cleanup], [text]");
      };
    }, [text]);

    function handleChange(e) {
      setText(e.target.value);
    }
    const element = (
      <>
        <input onChange={handleChange} />
        <p>{text}</p>
      </>
    );

    console.log("   Child render end");
    return element;
  };

  const App = () => {
    console.log("App render start");
    const [show, setShow] = React.useState(() => {
      console.log("App useState");
      return false;
    });

    React.useEffect(() => {
      console.log("App useEffect, no deps");

      return () => {
        console.log("App useEffect [Cleanup], no deps");
      };
    });
    React.useEffect(() => {
      console.log("App useEffect, empty deps");

      return () => {
        console.log("App useEffect [Cleanup], empty deps");
      };
    }, []);
    React.useEffect(() => {
      console.log("App useEffect, [show]");

      return () => {
        console.log("App useEffect [Cleanup], [show]");
      };
    }, [show]);

    function handleClick() {
      // setState는 첫번째 인자로 이전 값을 받는다.
      setShow((prev) => !prev);
    }

    console.log("App render end");

    return (
      <>
        <button onClick={handleClick}>Search</button>
        {show ? <Child /> : null}
      </>
    );
  };

  ReactDOM.render(<App />, rootElement);
</script>
```

## 14. 리액트 Element에 스타일 입히기

- className - 문자열
- style - 객체, 카멜케이스, className보다 먼저

```html
<body>
  <style>
    .button {
      background-color: #4caf50; /* Green */
      border: none;
      color: white;
      padding: 15px 32px;
      text-align: center;
      text-decoration: none;
      display: inline-block;
      font-size: 16px;
    }
    .blue {
      background-color: #008cba;
    } /* Blue */
    .red {
      background-color: #f44336;
    } /* Red */
    .gray {
      background-color: #e7e7e7;
      color: black;
    } /* Gray */
    .black {
      background-color: #555555;
    } /* Black */
  </style>
</body>
<script type="text/babel">
  function Button({ className = "", color, style, ...rest }) {
    return (
      <button
        className={`button ${className} ${color}`}
        style={{ fontSize: 30, ...style }}
        {...rest}
      />
    );
  }
  const element = (
    <>
      <Button style={{ borderRadius: "50%" }}>Green</Button>
      <Button color="blue" style={{ borderRadius: 8 }}>
        Blue
      </Button>
      <Button color="red">Red</Button>
      <Button color="gray">Gray</Button>
      <Button color="black">Black</Button>
    </>
  );

  ReactDOM.render(element, document.getElementById("root"));
</script>
```

## 15. Ref로 DOM 다루기

- Vanilla JS - document.get~ / document.query~
- React - useRef / ref

```html
<script type="text/babel">
  const App = () => {
    const inputRef = React.useRef();
    const divRef = React.useRef();

    React.useEffect(() => {
      inputRef.current.focus();

      setTimeout(() => {
        divRef.current.style.backgroundColor = "pink";
      }, 1000);
    }, []);
    return (
      <>
        <input ref={inputRef} />
        <div
          ref={divRef}
          style={{ height: 100, width: 300, backgroundColor: "brown" }}
        />
      </>
    );
  };
  ReactDOM.render(<App />, document.getElementById("root"));
</script>
```

## 16. Form 다루기

- onSubmit - event.preventDefault()
- event.target.elements - console.dir(element)

```html
<script type="text/babel">
  const App = () => {
    const handleSubmit = (e) => {
      e.preventDefault();
      console.dir(e.target);
      alert(
        `FirstName: ${e.target.elements.fname.value}, LastName: ${e.target.elements.lname.value}`
      );
    };
    return (
      <>
        <form onSubmit={handleSubmit}>
          <label htmlFor="fname">First name:</label>
          <br />
          <input type="text" id="fname" name="fname" defaultValue="John" />
          <br />
          <label htmlFor="lname">Last name:</label>
          <br />
          <input type="text" id="lname" name="lname" defaultValue="Doe" />
          <br />
          <br />
          <input type="submit" value="Submit" />
        </form>
      </>
    );
  };
  ReactDOM.render(<App />, document.getElementById("root"));
</script>
```

- validation - onChange
- controlled - input의 value를 직접 관리

```html
<script type="text/babel">
  const App = () => {
    const [message, setMessage] = React.useState("");
    const [phoneNumber, setPhoneNumber] = React.useState("");

    const handleSubmit = (e) => {
      e.preventDefault();
      alert(phoneNumber);
    };

    const handleChange = (e) => {
      if (e.target.value.startsWith(0)) {
        setMessage("Phone Number is valid");
        setPhoneNumber(e.target.value);
      } else if (e.target.value.length === 0) {
        setPhoneNumber("");
        setMessage("");
      } else {
        setMessage("Phone Number should starts with 0");
      }
    };

    return (
      <>
        <form onSubmit={handleSubmit}>
          <label htmlFor="phone">Phone Number: </label>
          <br />
          <input
            id="phone"
            name="phone"
            onChange={handleChange}
            value={phoneNumber}
          />
          <p>{message}</p>
          <br />
          <br />
          <button
            type="submit"
            disabled={
              phoneNumber.length === 0 || message !== "Phone Number is valid"
            }
          >
            Submit
          </button>
        </form>
      </>
    );
  };
  ReactDOM.render(<App />, document.getElementById("root"));
</script>
```

## 17. Error 다루기

- Error Boundary - Catch Error해서 보여주기
- Fallback - Error가 났을 때 보여줄 컴포넌트

```html
<script type="text/babel">
  class ErrorBoundary extends React.Component {
    state = { error: null };
    static getDerivedStateFromError(error) {
      return { error }
    }
    render() {
      const { error } = this.state;
      if (error) {
        return <this.props.fallback error={error} />;
      }
      return this.props.children;
    }
  }
  const Child = () => {
    throw new Error("Something wrong....");
    return (
      <p>Child...</p>
    )
  };

  const Fallback = ({ error }) => {
    return <p>{error.message}</p>
  };

  const App = () => {
    return (
      <>
        <p>App</p>
        <ErrorBoundary fallback={Fallback}>
          <Child />
        <ErrorBoundary/>
      </>
    );
  };

  ReactDOM.render(<App />, document.getElementById("root"));
</script>
```

## 18. Key와 리렌더링 알아보기

- Key - Value를 특정하는 이름

```html
<script type="text/babel">
  const todos = [
    { id: 1, value: "wash dishes" },
    { id: 2, value: "Clean the bed" },
    { id: 3, value: "Running" },
    { id: 4, value: "Learning" },
  ];
  const App = () => {
    const [items, setItems] = React.useState(todos);

    const handleDoneClick = (todo) => {
      setItems((items) => items.filter((item) => item !== todo));
    };

    const handleRestoreClick = () => {
      setItems((items) => [
        ...items,
        todos.find((item) => items.includes(item)),
      ]);
    };
    return (
      <>
        {items.map((todo) => (
          <div key={todo.id}>
            <span>{todo.value}</span>
            <button onClick={() => handleDoneClick(todo)}>Done</button>
          </div>
        ))}
        <button onClick={handleRestoreClick}>Restore</button>
      </>
    );
  };

  ReactDOM.render(<App />, document.getElementById("root"));
</script>
```

- 재사용 - key를 제대로 줘야 재사용 가능
- 제대로 준다 - 중복없고, 바뀌지 않는

```html
<script type="text/babel">
  const todos = [
    [
      { id: 1, value: "wash dishes" },
      { id: 2, value: "Clean the bed" },
      { id: 3, value: "Running" },
      { id: 4, value: "Learning" },
    ],
    [
      { id: 4, value: "Learning" },
      { id: 1, value: "wash dishes" },
      { id: 2, value: "Clean the bed" },
      { id: 3, value: "Running" },
    ],
    [
      { id: 3, value: "Running" },
      { id: 4, value: "Learning" },
      { id: 1, value: "wash dishes" },
      { id: 2, value: "Clean the bed" },
    ],
    [
      { id: 2, value: "Clean the bed" },
      { id: 3, value: "Running" },
      { id: 4, value: "Learning" },
      { id: 1, value: "wash dishes" },
    ],
  ];
  const App = () => {
    const [items, setItems] = React.useState(todos[0]);

    React.useEffect(() => {
      const interval = setInterval(() => {
        const random = Math.floor(Math.random() * 3);
        setItems(todos[random]);
      }, 1000);

      return () => {
        clearInterval(interval);
      };
    }, []);

    const handleDoneClick = (todo) => {
      setItems((items) => items.filter((item) => item !== todo));
    };

    const handleRestoreClick = () => {
      setItems((items) => [
        ...items,
        todos.find((item) => items.includes(item)),
      ]);
    };
    return (
      <>
        {items.map((todo, index) => (
          <div key={index}>
            <button onClick={() => handleDoneClick(todo)}>{todo.value}</button>
          </div>
        ))}
        <button onClick={handleRestoreClick}>Restore</button>
      </>
    );
  };

  ReactDOM.render(<App />, document.getElementById("root"));
</script>
```

## 19. 상태 끌어올리기

- 형제 컴포넌트의 상태 궁금 - 필요하면 부모로 lifting up
- Props drilling - 과도한 lifting은 drilling을 야기

```html
<script type="text/babel">
  const Id = ({ handelIdChange }) => {
    return (
      <>
        <label>ID: </label>
        <input onChange={handelIdChange} />
      </>
    );
  };

  const Password = ({ handelPasswordChange }) => {
    return (
      <>
        <label>PW: </label>
        <input type="password" onChange={handelPasswordChange} />
      </>
    );
  };
  const App = () => {
    const [id, setId] = React.useState("");
    const [password, setPassword] = React.useState("");

    const handelIdChange = (e) => {
      setId(e.target.value);
    };

    const handelPasswordChange = (e) => {
      setPassword(e.target.value);
    };

    const handleLoginClick = () => {
      alert(`id: ${id}, pw: ${password}`);
    };

    return (
      <>
        <Id handleIdChange={handelIdChange} />
        <br />
        <Password handelPasswordChange={handelPasswordChange} />
        <button
          disabled={id.length === 0 || password.length === 0}
          onClick={handleLoginClick}
        >
          LOGIN
        </button>
      </>
    );
  };

  ReactDOM.render(<App />, document.getElementById("root"));
</script>
```

## 20. 데이터 Fetch 해보기

- Fetch api - 네트워크 통신 도구
- 상황별 핸들링 - 로딩 / 데이터 / 에러

```html
<script type="text/babel">
  const App = () => {
    const [data, setData] = React.useState(null);
    const [error, setError] = React.useState(null);

    React.useEffect(() => {
      fetch(
        "http://raw.githubusercontent.com/techoi/raw-data-api/main/simple-api.json"
      )
        .then(function (response) {
          return response.json();
        })
        .then(function (myJson) {
          setData(myJson.data);
        })
        .catch((error) => {
          setError(error.message);
        });
    }, []);

    if (error != null) {
      return <p>There is some Error!</p>;
    }
    if (data == null) {
      return <p>Loading....</p>;
    }
    return (
      <>
        <div>
          <p>People</p>
          {data.people.map((person) => (
            <div>
              <span>name: {person.name}</span>
              <span>age: {person.age}</span>
            </div>
          ))}
        </div>
      </>
    );
  };

  ReactDOM.render(<App />, document.getElementById("root"));
</script>
```
