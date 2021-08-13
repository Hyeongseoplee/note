# Promise

### 개념

#### promise란?

---

**자바스크립트 비동기 처리에 사용되는 객체.**

비동기 처리 : 특정 코드의 실행이 완료될 떄 까지 기다리지 않고(코드의 시행을 멈추지 않고) 다음 코드를 먼저 수행하는 자바스크릡트의 특성

#### 왜 promise를 써야하지?

---

프로미스는 주로 서버에서 받아온 데이터를 화면애 표시할 때 사용한다.
서버가 언제 그 요청에 대한 응답을 줄지 모르는데 마냥 다른 코드를 실행 안하고 기다릴 순 없다.

만약 그렇게 된다면 간단한 요청 10000개를 서버에 보낸다고 가정하면 사용자가 웹 애플리케이션을 실행하는데는 수십 분이 걸릴 것이다.

즉, 데이터를 받아오기도 전에 마치 데이터를 다 받아온 것 마냥 화면에 데이터를 표시하려고 하면 오류가 발생하거나 빈 화면이 뜨게된다. 이와 같은 문제점을 해결하기 위한 방법 중 하나가 프로미스이다.

    요청 -> 대기 -> 응답 -> 요청 -> 대기 ->
    응답 -> ... 반복 x10000 -> 웹 실행

#

#### 비동기 처리의 두 가지 사례

---

**제이쿼리의 ajax & setTimeout 함수**

Link: https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/ "captain pangyo"

AJAX(asynchronous Javascript And Xml)
: 웹브라우저 내에서 새로운 정보가 요청되었을 떄 화면 전체를 reload하는 것이 아니라 변경되는 부분만 AJAX를 통해 받아 갱신하면서 자원, 시간 낭비의 문제점을 줄였다.  
그렇게 자바스크립트는 비동기적으로 서버에 요청을 보낸 뒤 계속해서 다른 작업을 가능할 수 있게 되었다.

#

#### 문제점

---

그런데 만약 API 서버에서 데이터를 받아온 뒤 메인 페이지로 이동하는 기능이 실행되어야 하는데,  
그 API서버에 요청을 보내고 언제 줄 지 모르는 응답을 기다리는 중에 메인페이지로 이미 이동해버린다면 이것참 곤란하게된다.  
즉, 응답이 아직 오지 앟았는데 다음 코드인 메인 페이지로 이동하는 로직이 실행되는 문제가 생겨버린 것이다.  
이러한 문제점 떄문에 비동기적 처리의 실행 순서를 제어하는 것이 필요해졌고, 그 방법으로 콜백함수가 있다.

####콜백 지옥
\*\*\*하지만 실전은 녹록치 않았다.  
실제 웹서비스에서처럼 AJAX를 통해 서버는 진짜 데이터만 전송하고 모든 것을 클라이언트에서 처리한다고 했을 떄 통신 이후 해야 하는 작업이 엄청 많을 것이다.
그리고 그 작업들에 순서도 있을테고.  
그럴 경우 함수에서 다른 함수를 계속 호출시킬 것이고 바로 콜백 지옥이 펼쳐진다.  
예제는 아래 링크를 참고.

link : https://tangoo91.tistory.com/42

그마저도 함수를 나눠 분리하는 패턴을 사용해도 결국엔 마찬가지이다.
그래서 ES6부터 **Promise** 객체가 추가 되었다.

이는 이러한 콜백지옥을 해결해 주고 비동기 처리도 이전보다 간결한 코드로 작성할 수 있게 되었다. :D

### Promise

---

Promise는 비동기 처리를 실행하고 그 처리가 끝난 후 다음 처리를 실행하기 위한 기능을 제공한다.  
Promise는 아래와 같이 Promise 객체를 생성하는 것부터 시작한다.

```javascript
let promise = new Promise((resolve, reject) {
// 최초 비동기 처리 코드
}
```

1. resolve : 함수 안의 처리가 성공적으로 끝났을 때 호출해야 하는 콜백 함수.  
   어떠한 값도 인수로 넘길 수 있다. 이 값은 다음 처리를 실행하는 함수에 전달된다.
2. reject : 함수 안의 처리가 실패했을 떄 호출해야 하는 콜백 함수.

프로미스의 상태

1. pending : 대기
2. fulfilled : 연산이 성공적으로 완료됨.
3. rejected : 연산이 실패.

#

#### Then( )

---

promise의 값을 반환해주는 함수

#

#### Promise chaining

---

- promise를 then으로 연결한다.
- catch로 에러를 잡아낼 수 있음.
- 단, 매번 return 값을 정해주어야 한다.

```javascript
<script>
  const sandwich = new Promise((resolve, reject) =>{" "}
  {
    //new Promse() 메서드 호출 할 떄 인자로 resolve, reject 콜백 함수 선언
    resolve(2) // 콜백 함수의 인자 resolve 실행, 요청 완료 시 호출할 함수에 인자로 2를 넘겨줌
  }
  ) const timesTwo = (number) => number * 2; sandwich .then(timesTwo) // 4
  .then(timesTwo) // 8 .then(timesTwo) // 16 .then(timesTwo) // 32
  .then(timesTwo) // 64 .then(timesTwo) // 128 .then(() =>{" "}
  {
    throw Error("It is all your fault") // 에러가 난 부분
  }
  ) .then(finalResult => console.log(finalResult)) .catch(error =>
  console.log(error)) // error : It is all your fault
</script>
```

#

#### Promise.all

---

주어진 모든 promise를 실행한 후 진행되는 히니의 promise를 반환한다. 추합하여 한방에 빰.  
각각의 promise가 언제 끝나는지에 상관없이 전부 끝났을 떄 그 api 데이터들을 순서에 맞춰 배열로 건네준다.  
\*단 받아진 순서대로가 아닌 요청훈 순서대로!
