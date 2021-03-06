# Next.js

## 1. Next.js 소개

### SSR 이란?

클라이언트로 전달될 HTML 파일 내용(일부를) 미리 그려서 내려주는 것

- 클라이언트 랜더링의 속도를 빠르게 하여, 사용자 체감 속도 증진
- 검색 엔진이 JavaScript를 실행하지 않고 크롤링 가능 SEO

---

- Next.js - React Framework
- Vercel - Frontend Deploy platform
- SSR vs CSR - 보여질 화면을 그리는 주체
- SSR 장점 - SEO / 렌더 속도 / 기타

## 2. 환경 설정 및 프로젝트 생성

- CSR vs SSR - Next.js로 둘다 가능
- 쇼케이스 - Next.js 실제 사용 예
- SSG vs SSR - getStaticProps vs getServerSideProps
- 예시 - github

## 3. Next.js 기본

- Next.js - 다양한 기능을 추상화해서 제공
- Navigate / prefetching - &lt;a&gt; with &lt;List&gt; / code splitting
- Image / Head - "next/image" / "next/head" : meta
- built in styling / global - Css modules / Sass / styled-jsx

---

- hydration - js 실행으로 interactive 할 준비 과정
- SSG - Build time에 서버에서만 동작
- SSR - Request time에 동작 / TTFB slow
- CSR - Request time 이후 동작 SWR

---

- Dynamic Routes - getStaticPaths
- 키 값 - 동적으로 만들어서 대응
- fallback - false면 404, true면 router.isFallback
- API Routes - /pages/api/hello.js

## 4. Next.js 심화

- Pages - Pre-rendering / Dynamic routes
- getStaticProps - revalidate(ISR) / redirect / notFound
- getStaticPaths - fallback: 'blocking'
- getServerSideProps - req.cookies

---

- Layouts - Page.getLayout
- Optimization - Image / Font / Script
- Static file / Fast Refresh - public / 똑똑하게 reload 판단
- 기타 - ESLint / Typescript / 환경 변수

---

- Next.js의 라우팅 - pages 폴더의 file system 활용
- Dynamic Routes - [slug] / [...slug] / [[...slug]]
- Router - 직접 라우터를 조작 가능 push / shallow
- API Routes - API 서버로의 동작 middlewares

## 5. Next.js 실제

- 제품으로서의 웹 - 실제 배포 전에 고려해야하는 점들
- 번들 사이즈 - 번들 포비아 / Webpack analyzer
- Deploy Vercel - Github와 연동
- PR - 새로운 PR 생성시 Preview 제공

---

- 인증 - 클라이언트 사이드 / 서버 사이드
- Testing - E2E testing / Unit testing
- Preview / Dynamic Import - Headless CMS 초안 / 필요할 때 import
- 기타 - Static Optimization / export / path alias

---

- AMP - 렌더링 속도를 극단적으로 높이는 방법
- Babel - next/babel / plugins / presets
- AST - 추상 구문 트리 / 소스코드를 트리로
- PostCSS - Autoprefixer 등 / browserslist

---

- Custom - Server / App / Document / Error Page
- src Directory - src/pages 가능 단, pages 가 없을 때
- Multi zones - 여러개의 next app로 하나의 도메인 구성
- 성능측정 - reportWebVitals(metric)

---

- 디버깅 - 실무에서 많이 쓰일 방법
- 소스맵 - 배포된 코드와 원본의 연결
- codemods - 코드 변경 도구
- 기타 - int'l route / trace / react 18 / next 12

---

- Upgrade Guide - 최신인 12버전 까지
- Cli / CNA - Next.js 다루는 간편 도구
- 기타 - Router / Link / Image / Head / Server
- next.config.js - Next.js 프로젝트 구성 커스텀
