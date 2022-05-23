# GraphQL

## 1. GraphQL 소개

- vs SQL - Server와 DB 간의 질의어 => Server와 Web Client 간의 질의어
- vs REST API - 다중 엔드포인트 => 단일 엔드포인트
- Overfetching 문제 - 필요한 데이터만 요청으로 해결
- Underfetching 문제 - 한번의 요청으로 해결

### REST API vs GraphQL

- 리소스
  - 리소스 모양과 크기는 서버에 의해 결정된다. VS 클라이언트가 필요한 리소스를 요청한다.
- 엔드포인트
  - 다중 엔드포인트, URL과 Method에 따라 접근할 수 있는 데이터가 다르다. VS 보통 단일 엔드포인트, GraphQL 스키마에 따라 데이터가 다르다.
- 라우트 핸들러와 리졸버
  - 각 요청은 정확히 하나의 경로 처리 함수를 호출 VS 하나의 쿼리가 여러 리졸버를 호출하여 여러 리소스가 포함된 중첩 응답 구성

> REST API를 사용하면 일반적으로 여러 엔드포인트에 엑세스해서 데이터를 수집해야 한다.<br/>
> GraphQl은 구체적인 데이터 요구 사항이 포함된 단일 쿼리로 요청가능<br/>
> REST API는 overfetching과 underfetching을 유발시킨다.<br/>
> GraphQL은 필요한 데이터만 요청할 수 있다.

## 2. 환경 설정 및 프로젝트 생성

- GraphQL은? - 라이브러리가 아니라 명세다.
- 다뤄보려면 - 구현체가 필요하다.
- star wars api - clone 해서 로컬에서
- 다양한 도구들 - graphql graphiql express... 등

## 3. GraphQL 기본

- 쿼리 - 요청, 결과 동일 / 주석 / 작업(타입 / 이름)
- 쿼리 - 필드 객체 참조(다중콜X / 인자 / 별칭)
- Fragment - 반복되는 필드셋 / 변수 전달 가능
- 변수 / 지시어 - 동적 쿼리 방법 / @include @skip

---

- 뮤테이션 - 데이터의 수정을 가하는 방법
- Apollo GraphQL - 다양한 기능이 추가된 라이브러리
- 뮤테이션 다중 필드 - 순차 실행(쿼리는 병렬)
- 인라인 프래그먼트 - interface / union 일때 사용

---

- 타입 시스템 - 객체 타입과 필드
- 특별한 타입 - 쿼리 타입 / 뮤테이션 타입
- 스칼라 타입 - 구체적 데이터
- 기타 - 인터페이스 / 유니온 / 인풋

## 4. GraphQL 심화

- Apollo GraphQL - 프론트와 서버를 모두 제공하는 라이브러리
- GraphQL 서버 - apollo-server graphql
- 스키마 - 프론트와 쉐어할 데이터 구조
- 데이터 소스 - REST API(기본 캐싱 O) / DB(캐싱 X)

---

- 리졸버 - 쿼리 요청에 대한 응답 생성
- 페이지네이션 - 서버 부하를 줄임
- 뮤테이션 리졸버 - 로그인 / 예약
- SQLite - 데이터 축적됨

---

- 프론트엔드 연결 - ApolloClient
- useQuery - data, loading, error
- 페이지네이션 / 캐시 - fetchMore / InMemoryCache
- useMutation / makeVar - 뮤테이션 / client 로컬 상태 관리
