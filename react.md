
# React Component Guide

> DevPMO실의 타입스크립트로 작성된 React 스타일 가이드 입니다. (버전 0.0.1) `Airbnb React/JSX Style Guide`를 참고 했습니다.

---

### Component 파일 이름은 `PascalCase` 규칙을 사용한다.
> 이유 : 리액트 규칙
---
### Component 파일은 코드 100줄을 넘기지 않도록 한다.
> 이유 : 내부 규칙 코드 가독성 & 컴팩트한 컴포넌트 관리를 위해서
---
### 1개 파일에는 1개의 컴포넌트만 작성한다. (파일 이름과 컴포넌트 명을 통일한다.)
> 이유 : 가독성을 위해서, 글로벌 규칙에 따른다.
---
## 모든 컴포넌트는 함수형 컴포넌트로 작성한다. (선언식 권장)
> 이유 : 이제는 함수형 컴포넌트가 글로벌 스탠다드로 확립되어 있다.
```tsx
function Listing({ hello }) {
  return <div>{hello}</div>;
}
```
---
### `map`메서드 을 통해 요소를 반복하여 생성시 key에 (index, uuid)를 사용하지 않는다. 요소가 업데이트 되지 않을 때까지 고유한 값을 key로 설정한다.

> 이유 : 랜더링 로직에서 key 리랜더링 판단에 쓰임으로 key에 유동적인 값이 들어가면 비효율 성능저하를 유발시킨다.
```tsx
🚫
{todos.map((todo, index) =>
  <Todo
    {...todo}
  key={index}
  />
)}

✅ 
{todos.map(todo => (
  <Todo
    {...todo}
  key={todo.id}
  />
))}
```
 ---
### `spread props`은 사용을 지양한다.
> 이유 : 코드양은 줄일 수있지만 협업시의 해독 시간이 더 필요해 진다.
```tsx

✅  return <WrappedComponent name={value1} age={value2} />

🚫  return <WrappedComponent {...this.props} />

```
---
### JSX 중괄호를 공백으로 채우지 마십시오. react/jsx-curly-spacing
> 이유 : 불필요한 공백으로 오히려 가독성을 해친다.
```tsx
<Foo bar={baz} />
```
---
### `prop` 네이밍은 속성 타입에 따라 컴포넌트의 경우  `PascalCase`를 이외에는 `lowerCamelCase` 를 사용한다.
> 이유 : Airbnb 표준이고 코드의 통일성을 위해서
```tsx
<Foo
  userName="hello"
  phoneNumber={12345678}
  Component={SomeComponent}
/>
```
---
### 자식이 없는 요소는 태그를 항상 닫는다.
> 이유 : Airbnb 표준이고 코드양을 줄일수 있다. react/self-closing-comp
```tsx
🚫
<Foo variant="stuff"></Foo>

✅ 
<Foo variant="stuff" />
```
---
### `state`는 UI 조작  이외에는 로직에 사용하지 않는다. (`state` 값 외부로 바인딩 X)
> 이유 : 랜더링은 어느정도 제어 가능하지만 로직에 사용할 수 있을 정도로 제어하려면 UI의 성능을 포기해야 한다.
```ts
✅ const [score, setScore] = useState(0);

🚫 const [user, createUser] = useState({
  name: '',
  ...
});
```
---
### `state`최대 3개 이하로만 사용한다.
> 이유 : 컴팩트한 컴포넌트 관리를 위해서.
---
### `props`에 약어의 사용을 자제한다. (사용해야 한다면 주석을 꼭 달자.)
> 이유 : 의미 파악이 어렵다.     
---


