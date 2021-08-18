# Recap

### NodeJS setup

**dependencies vs devDependencies**

패키지의 체계화를 위해서 나누었다.

dependencies : 프로젝트를 돌릴 떄 필요한 패키지

> e.g express

devDependencies : 사람(개발자)를 위해 사용하는 것

> e.g nodemon : 파일을 보고있다가 변화가 생기면 commend를 준다.
> "nodeman --exec ~블라블라"

```
package.json이 있는 상태로 npm i 를 하면
npm이 dependencies, devDependencies 를 찾아서 있는 모든 걸 자동으로 설치해준다.
그러므로 node_modules 폴더를 다운로드할 필요가 없음.
(.gitignore로 고고)
```

> babel-node :  
> babel이 최신 JS문법을 학인하고 node.js 방식으로 변환하여 node.js 서버를 작동시킨다.

> babel.config.json :  
> babel.node를 사용하려면 babel.config.json을 만들어야 한다. 그 파일안에 우리가 babel에 축하고 싶은 plugin을 넣는다.
> preset-env -> 최신 JS를 사용하게 해준다.
> { "preset" : ["@babel/preset-env]}

#

### NodeJS Server

---

서버란? 24시간 켜져있고 request를 listening 하고 있는 컴퓨터.

request란? 브라우저가 서버에게 하는 모든 상호작용.
user가 직접 요청하는게 아니라 브라우저가 대신 request하고 response를 받는다.  
내 행동을 listening 하고 있는 서버에게만 request를 보내 수 있다.

- expresss application을 사용할 수 있도록 app에 담는다. 즉, 모든게 app에 있다.

- port 를 쓰는 이유?
  서버는 내 퓨터 전체응 listen 할 수 없다.
  그러므로 내 서버에 개방된 해당 port로 request를 보내는 것이다. like open the door or window.
  이때부터 4000을 통해 소통한다.

**브라우저가 server에 request를 하면 server가 response 해준다.**

### Controllers

---

#

: 이벤트함수의 콜백함수와 같은 위치에 있는 함수.
3 개의 인자가 있다.(req, res, next)
각 인자는 는 express로부터 request,respond, next 관련된 객체를 물려받는다.(이름은 마음대로 지어도 상관없지만 첫 번째 인자는 resquest, response라는게 중요하다.)
중요한건 뭐가 됐든 응답을 해주어야 한다는것..!
그렇지 않으면 무한로딩, 웹사이트는 느려진다.
관습적으로 마지막 controller에는 next()를 쓰지 않는다. 그래서 인자에 next 빼도 무관하다.

### Middleware

---

#

: request와 response의 상호작용 중간에 낀 controller.
모든 middleware는 controller이다.

```javascript
import express from "express";

const PORT = 4000;

const app = express();

const handleHome = (req, res) => res.send("hey how are you?");

const methodLogger = (req, res, next) => {
  console.log("path", req.path);
  next();
};

const routerLogger = (req, res, next) => {
  console.log("method", req.method);
  next();
};

app.get("/", methodLogger, routerLogger, handleHome); // /
// "페이지를 가져가도 좋아"
// 실제로 express가 /(home) 페이지로 가려는게 확인되면 함수실행 ( 응답을 위해 return 필수!)

const handleListening = () => {
  console.log(`server Listening on port http://localhost:${PORT}`);
};

app.listen(PORT, handleListening);
```

#

여기서 methodLogger 와 routerLogger controller가 middleware 이다.
이유는 next()를 통해 작업을 다음 함수로 넘기고 있기 떄문이다.

> _함수와 controller의 차이?_  
> controller에서는 router에서 활용되는 함수들을 관리할 수 있다.  
> 당연히 컨트롤러가 함수보다 큰 개념.

#### use의 사용

---

많은 middleware들을 싸그리 묶어서 전역에서 사용할 수 있게끔 도와주는 method이다.

- `app.use(middleware1, middleware2)` 이용방식과 읽는 순서( |, -> )

```javascript
| (1)
 -> app.use( -> methodLogger,-> routerLogger)
| (2)
 -> app.get("/", handleHome)
```

단 전역에서 사용할 수 있게끔 요청을 받아와서 함수를 실행시키는 app.get()등 의 최상단에 위치해야한다.

### Bonus!

#### Morgan function

---

\_정의 : node.js용 request logger middleware.  
요청에 대한 정보를 콘솔에 기록해준다.

morgan 함수를 호출하면 내가 설정한 대로 middleware를 return 해준다.

함수의 인자로

- dev

- short

- common

- combined

등을 줄 수 있다.

#### Morgan function

---

\_정의 : node.js용 request logger middleware.  
요청에 대한 정보를 콘솔에 기록해준다.

morgan 함수를 호출하면 내가 설정한 대로 middleware를 return 해준다.

함수의 인자로

- dev

- short

- common

- combined

등을 줄 수 있다.

```javascript
import express from "express";
import morgan from "morgan"; // morgan 모듈을 import 해서 morgan 이라는 이름을 준다.

const PORT = 4000;

const logger = morgan("dev"); //morgan 이 가지고 있는 인자 "dev"

const app = express();

const handleHome = (req, res) => res.send("hey how are you?");

app.use(logger);
app.get("/", handleHome);

const handleListening = () => {
  console.log(`server Listening on port http://localhost:${PORT}`);
};

app.listen(PORT, handleListening);

//콘솔에 찍힌 값
//GET /login 304 5.558 ms - -
// METHOD, PATH, Status code, 응답시간
```

> ! morgan 부분 복습 필요함
