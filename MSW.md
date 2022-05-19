# MSW(Mork Service Worker)

## 모킹(Mocking)이란?

Mock(모의 데이터)을 만들어서 활용하는 방식<br/>
통상적으로 data fetch를 해야하는 경우 통신을 통해 응답을 내려주는 서버가 있어야 함<br/>
서버가 없는 경우, api 요청으로 내려올 데이터를 프론트에서 모킹하거나 서버의 역할을 해주는 무언가가 필요

- Mocking - 모의 데이터 활용
- Browser - Service worker 활용
- REST API / GraphQL - 모두 모킹 가능

---

- mock - handler / browser 만 있어도 동작
- public - public폴더에 npx msw init public/
- 기타 커스텀 - query / patching / error

```js
// src/mocks/browser.js
import { setupWorker } from "msw";
import { handlers } from "./handlers";

export const worker = setupWorker(...handlers);
```

```js
// src/mocks/handlers.js
import { rest } from "msw";

export const handlers = [
  rest.post("/login", (req, res, ctx) => {
    // Persist user's authentication in the session
    sessionStorage.setItem("is-authenticated", "true");

    return res(
      // Respond with a 200 status code
      ctx.status(200)
    );
  }),

  rest.get("/user", (req, res, ctx) => {
    // Check if the user is authenticated in this session
    const isAuthenticated = sessionStorage.getItem("is-authenticated");

    if (!isAuthenticated) {
      // If not authenticated, respond with a 403 error
      return res(
        ctx.status(403),
        ctx.json({
          errorMessage: "Not authorized",
        })
      );
    }

    // If authenticated, return a mocked user details
    return res(
      ctx.status(200),
      ctx.json({
        username: "admin",
      })
    );
  }),
];
```
