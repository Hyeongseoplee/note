# Make my first server

#

#### GET Request

---

```javascript
import express from "express"; // (1)

const PORT = 4500;

const app = express(); // (2)

const handleHome = (req, res) => {
  //(5)
  return res.send("this is response!"); // (6)
};

const handleLogin = (req, res) => {
  return res.end("END"); // (6)
};

app.get("/", handleHome); //(4)
app.get("/login", handleLogin);

app.listen(PORT, () => {
  // (3)
  console.log(`✅ Server listening on port http://localhost:${PORT}`);
});
```

1.  최상단의 코드는 'express 를 import 후 express라는 이름으로 쓰겠다!' 라는 뜻이다.

2.  express를 사용해서 app을 만든다.(by ES6)  
    = 서버를 만든다

3.  listen("PORT NUMBER in local", callback Func) 함수는 http 서버를 시작하게 하며 여기서 사용자의 요청을 받도록 대기한다.

4.  app.get("URL", CallbackFunc)

    :URL로 get request가 오면, express는
    CallbackFunc에다가 request와 response object를 넣어준다.

5.  console.log(request 혹은 response)를 해보면
    무수한 request 와 response object들을 받아온 것을 확인할 수 있다.

6.  send() : 응답으로 보내주는 값. 메시지 등을 넣을 수 있다.
    end() : 서버에게 아무것도 보내지않고 끝낸다. 서버를 killing.

---

### 정리

#

**서버와 브라우저와의 상호작용**

브라우저가 request를 보냄 -> 내 server가 response
