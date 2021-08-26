### Router\_\_React

#### router

router는 Hashrouter 안에서 쓰여야 한다.  
비슷한 기능으로 Browserouter도 있다.  
gh-pages에서 쓰기엔 Hashrouter가 낫다.

```javascript
import { HashRouter, Route } from "react-router-dom"; // react-router-dom 패키지에서 import

-----------------

function App() {
  return (
  <HashRouter>
    <Navigation></Navigation>
    <Route path="/" exact={true} component={ Home }>
    </Route>
    <Route path="/about" component={ About }>
    </Route>
  </HashRouter>
  )
}

```

#

#### navigation

---

navigation 안에 SPA기능을 살려주는 link , to 를 쓰려면 역시 react-router-dom 패키지에서 import 후 반드시 **hashrouter 안에 navigation을 넣어주어야만 동작한다.**

```javascript
import { Link } from "react-router-dom";

function Navigation() {
  return (
    <div>
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
    </div>
  );
}
```

#

#### history.push

---

props 를 콘솔로 찍어보면 location(props값을 담은), history 등 다양한 property들이 나온다.
그 중 history.push는 만약 원치않은 방법으로 url에 접근해서 router로 부터 props가 제대로 받아지지 않았다면 해당 url로 강제 redirect 시킬 수 있다.

```javascript
if (location.state === undefined) {
  history.push("/");
}
```
