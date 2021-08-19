# Router

### Router란?

:**URL이 어떻게 시작하느냐에 따라 나눈 방법**  
공통 시작 부분으로 url을 그룹화하여 정리해준다.

**예**  
/edit-video\_\_comment-on-video (x)
/video/comment/edit (o)

**사용하는 이유?**  
_url을 더 낫고 독립적인 방법으로 관리하기 위해 라우터를 사용한다._

```javascript
import express from "express";
import morgan from "morgan";

const PORT = 4000;
const app = express();

const logger = morgan("dev");
app.use(logger);

const globalRouter =  express.Router(); // global router 생성

const handleHome = (req, res) => res.send("Home");

globalRouter.get("/", handleHome);

const userRouter = express.Router();

const handleEditUser = (req, res) => res.send("Edit User")

userRouter.get("/edit", handleEditUser);

const videoRouter = express.Router();

const handleWatch = (req, res) => res.send("Watch Video");

videoRouter.get("/watch", handleWatch); // URL을 조회하여 정보를 가져온다.


app.use("/", globalRouter); // 주소("/")의 요청이 있을 경우에만 설정한 미들웨어를 실행(express를 인자로 받는다.).  ​
app.use("/users", userRouter);
app.use("/videos", videoRouter);

const handleListening = () => {
   ​console.log(`server Listening on port http://localhost:${PORT}`);
}

app.listen(PORT, handleListening)
```

#

서버에 각 router를 생성해준다

```javascript
const globalRouter = express.Router(); // global router 생성
const userRouter = express.Router();
const videoRouter = express.Router();
```

#

app.use()를 이용하여 해당 URL의 요청이 있을 경우에만 미들웨어를 실행 시킨다.

#

_e.g. "/users"로 시작하는 URL에 들어가면._

```javascript
app.use("/", globalRouter); // 주소("/")의 요청이 있을 경우에만 express를 인자로 받는 설정된 미들웨어(globalRouter)를 실행.
app.use("/users", userRouter);
app.use("/videos", videoRouter);
```

#

해당 함수에서 URL을 조회하여 무언가를 리턴하는 미들웨어를 실행시킨다. 이곳에서 express는 나머지에 해당하는 URL을 찾고 응답을 준다.

```javascript
globalRouter.get("/", handleHome);
const handleHome = (req, res) => res.send("Home");

userRouter.get("/edit", handleEditUser);
const handleEditUser = (req, res) => res.send("Edit User");

videoRouter.get("/watch", handleWatch);
const handleWatch = (req, res) => res.send("Watch Video");
```

---

### Refactoring

---

프로젝트에 있는 모든 파일은 분리된 모듈이다.
(= 독립되어있다.)
그래서 무언가를 바깥에 공유하기 위해선(혹은 import 하기 위해서) 먼저 export 해준 뒤 쓸 곳에서 impoort 해주어야한다.

![Alt text](/img/router-refac.png)

#

한 파일에 붙어있는 router와 controller 들을
분리하여 router파일, controller에 담아
router에 controller를 import하면 더 깔끔하게 코드를 정리할 수 있다.

이런 식으로 만들다보면 여러개의 컨트롤러를 export해야하는 상황이 온다. 참고로 export default 는 오직 한번만 쓸 수 있다.  
다음과 같이 세개의 함수를 바깥과 공유하고 싶다면 어떻게 해야할까?

```javascript
export const join = (req, res) => res.send("Join~~");

export const editUser = (req, res) => res.send("Edit user :0");

export const deleteUser = (req, res) => res.send("Delete user :-X");
```

정답은 바로 각각의 함수에 export를 담아주는 것이다.

```javascript
import yummyExpress from "express";
import { editUser, deleteUser } from "../controllers/userController";
```

#

export default 일 떈 이름을 바꾸어 써도 상관없지만
**여러개의 함수를 export해서 가져온 것들은 이름을 그대로 써주어야한다.**  
즉,어느 함수를 쓸지 정확히 언급해주어야한다.
같은 이유로 import 해온 express는 이름을 바꿔 사용할 수 있다.

### Router's Parameter

---

#### 개념

: **URL에 변수를 넣을 수 있게 한다. ':' 표시가 express에게 변수라는걸 알려준다.**

변수를 넣을 수 있게되면 수백, 수천가지 요청에 대한 라우터와 컨트롤러를 만들지 않아도 된다.
강의 영상들의 각 url을 보면 끝에 숫자가 있는데 그게 parameter로 받아진 각 영상의 id값이다

#

#### 사용 예

> /users/:id (이름은 id, potato, coffee 뭐든 상관없다)

```javascript
videoRouter.get("/:dinosour", see);
```

```javascript
export const see = (req, res) => {
  console.log(req.params); // express는 내가 고른 이름(id, potato, coffee)과 함께 값을 제공해준다
  return res.send("Watch videos!");
};
```

그런데 아래와 같이 변수가 없는 라우터가 변수가 있는 라우터보다 하단에 위치하게 된다면?

```javascript
videoRouter.get("/:id", see);
videoRouter.get("/upload", upload); // 변수가 없는 라우터, 요청에 제대로된 응답이 불가능
videoRouter.get("/:id/edit", edit);
videoRouter.get("/:id/delete", deleteVideo);
```

#

서버는 변수 설정 후 나오는 자리에 있는 것은 모두 변수값으로 취급하게 되어서 결국

```javascript
url 입력 localhost:4000/videos/123 // watch a video #123
url 입력 localhost:4000/videos/upload // watch a video #upload
```

이런 불상사를 만들어낸다.  
즉 express가 upload라는 단어를 찾을 수 가 없는 것이다.
이론적으로 express의 입장에선 충분히 upload가 id처럼 보일 수 있으니 화를 낼 순 없는 일이다.  
**그런 일이 없게끔 변수가 없는 라우터는 항상 변수가 있는 라우터보다 상단에 위치하게 해야한다.**

#### Express 정규식

---

: 문자열로 부터 특정 정보를 추출하는 방법
변수에 들어갈 데이터 타입을 설정할 수 있다.  
(number or string or specified string.. and so on)
이처럼 변수의 타입을 설정하게 되면 변수가 없는 라우터가 최하단에 위치하더라도 문제가 없다.

```javascript
videoRouter.get("/:id(\\d+)", see);
videoRouter.get("/:id(\\d+)/edit", edit);
videoRouter.get("/:id(\\d+)/delete", deleteVideo);
videoRouter.get("/upload", upload); // 요청에 제대로 응답 가능.
```

- 정규식 연습사이트  
  link : https://regexr.com/
- 정규식 배우기  
  link : https://kasterra.github.io/regex1-the-basic-operation/

#

보충 내용

- get("URL", handleSomething)

: URL을 조회하여 정보(handleSomething)를 가져온다.

- ../ : 현재 폴더 바깥으로 나간다.
- ./ : 현재 있는 폴더.
