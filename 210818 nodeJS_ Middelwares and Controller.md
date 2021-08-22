# Middleware and Controllers

#

#### Middleware

_middle + software 의 약자_  
 :request와 response의 사이에 껴있는 함수이고 next함수를 호출한다.
이 함수를 호출하면 앱 내의 그 다음 함수가 호출된다.
이로써 requesst를 하는 함수가 아니라 어떤 작업을 다음 함수에게 넘기는 역할을 한다.

    Middleware(사실상 모든 함수)는 3가지 인자를 받을 수 있다.
    (사용하냐 안하냐/ middlware가 되냐 안되냐 의 차이)
      1. req
      2. res
      3. next


    Middleware는 4가지 역할을 한다.
      1. 모든 코드를 실행.
      2. 요청 및 응답 오브젝트에 대한 변경을 실행.
      3. 요청-응답 주기를 종료.
      4. 스택 내의 그 다음 미들웨어를 호출.

모든 컨트롤러는 next()의 유무에 따라 **middleware가 될 수도 controller가 될 수도** 있다. next()가 있으면 middleware, 없으면 함수.
없으면 브라우저와 서버의 연결을 중단시키기 떄문에 middleware가 될 수 없다.

#

```javascript
import express from "express";

const PORT = 4500;

const app = express();

const gossipMiddleware = (req, res, next) => {
  // next를 인자로 받아
  console.log(`someone is going to your ${res.url}`);
  next(); // 다음 함수로 넘긴다.
};

const handleHome = (req, res) => {
  return res.send("this is response!");
};

app.get("/login", gossipMiddleware, handleHome);

app.listen(PORT, () => {
  console.log(`✅ Server listening on port http://localhost:${PORT}`);
});
```

#

#### use

#

---

미들웨어 함수를 실행하려면 미들웨어함수를 정한 후 app.use()를 호출하면 된다.
미들웨어를 실행할 때 등록한 경로와 지금 들어온 요청 주소가 일치할 뗴만 그 미들웨어 함수를 실행할 수 있다.

```javascript
const myLogger = (req, res, next) => {
  console.log(`${req.method} , ${req.url}`);
  next();
};

const handleHome = (req, res) => {
  return res.send("this is response!");
};

app.use(myLogger);
app.get("/", handleHome);

// 만약 루트 경로에 대한 라우팅(get) 이후에 myLogger가 로드된다면
// 루트 경로의 라우트 핸들러(handleHome)가 요청-응답 주기를 종료하므로 요청은 myLogger에 도달하지못하고 앱은 "Logged"를 인쇄하지 않는다.
// javascript 와 같이 nodeJS도 로직이 위에서 아래 순으로 실행된다는 것을 유념.
```

아래 코드는 use()를 쓰지않았지만 이와 같은 코드이다.  
포인트는 middleware는 왼쪽에서 오른쪽으로 실행된다는 점.

```javascript
const myLogger = (req, res, next) => {
  console.log(`${req.method} , ${req.url}`);
  next();
};

const handleHome = (req, res) => {
  return res.send("this is response!");
};

app.get("/", myLogger, handleHome);
```
