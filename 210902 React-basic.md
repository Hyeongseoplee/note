## React

#### useEffect()

> useEffect(함수, [변경된 state])

: state 가 변경되고 **rendering이 끝난 뒤에** 함수를 실행시킨다.  
state 가 변경되고 API를 불러 올 떄 쓴다.

#### 의존성 배열

두 번째 인자엔 배열이 들어간다. [] 안을 비어있는 채로 두게 되면 함수가 최초 단 한번만 호출된다.  
하지만 의존성 error가 뜬다면 useEffect 내부에서 특정값을 사용하면 (변경된 state 라던지.. 변수라던지 .. 혹은 변수라던지..) []안에 해당값을 적어주어야한다.

#### useParams

useParams는 path parameter의 정보를 얻을 수 있는 hooks이다.

```javascript
<Route path="/words/:day">
  {" "}
  // url에 딸려온 숫자 정보를 가져온다
  <Day></Day>
</Route>
```

```javascript
import { useParams } from "react-router-dom"; // 패키지에서 useParams를 가져오고

const { day } = useParams(); // = const day = useParams().day;

// use
```

#### useHistory

link 대신 사용하는 hook.
useHistory 모듈을 import 한 뒤
history 변수를 만든다.

> import { useHistory } from "react-router";  
> const history = useHistory();

이동하고 싶은 url을 입력한다.

> history.push(URL}
