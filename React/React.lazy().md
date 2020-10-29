React.lazy 는 동적으로 Component를 임포트하여 이용한다. import 를 호출하는 함수를 인자로 가진다.

import 구문은 아래와 같다.
`const App = React.lazy(() => import('./components/App'));`

동적으로 컴포넌트를 불러오는 동안 예비 페이지를 보여주기 위해 lazy 로 부른 컴포넌트는 Suspense 컴포넌트 안에서 랜더링된다.
```javascript
<Suspense fallback={<div>Loading...</div>}>
  <App/>
</Suspense>
```
