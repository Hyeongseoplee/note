# Async Await

#

#### 정의

---

자바스크립트의 최신 **비동기 처리 패턴**.

#

#### 이점

---

- 기존의 콜백함수와 promise의 단점을 보완해준다
- 개발자가 코드를 읽기 쉽게 만들어준다.  
  이 말은 위에서 부터 아래로 순차적인 순서대로 읽을 수 있도록 코드를 만든다는 뜻이다.
- async와 await를 사용함으로써 여러개의 then 사용을 피할 수 있다.

#### 예제

---

> Before

- Promise의 객체를 새로 리턴하여 response에 담는 첫 번쨰 then을 만든다. json 형식으로 새로운 Promise 객체를 리턴하기 위해 또 then을 이어붙인다.

```javascript
const getMoviesPromise = () => {
  setTimeout(() => {
    fetch("https://yts.mx/api/v2/list_movies.json")
      .then((response) => {
        console.log(response);
        return response.json();
      })
      .then((json) => console.log(json))
      .catch((e) => console.log(e));
  }, 3000);
};

getMoviesPromise();
```

#

> After

- 함수 앞에 예약어 async 붙인다.
- 함수의 내부로직 중 http 통신을 하는 코드의 앞에 await를 붙여 변수에 담는다. 그 변수는 then()의 response와 똑같은 값을 갖는다.

```javascript
const getMoviesAsync = async () => {
  //await는 Promise(https:~)가 끝날 때까지 기다려준다. 요청이 완료되면 반환값을 response에 담는다.
  //!요청의 성패(resolve, reject)를 기다리는게 아니라 단지 Promise의 완료를 기다린다
  const response = await fetch("https://yts.mx/api/v2/list_movies.json");
  const json = await response.json();
  console.log(json);
};

getMoviesAsync();
```

#

#### 에러잡기 / catch

---

- response에 넣은 Promise 객체는 text 형식
- 결과적으로 5번쨰 줄에 response를 json 형식으로 변환하는 과정에서 에러를 띄운다. + 6번째 줄 에러메시지까지

```javascript
const getMoviesAsync = async () => {
  try {
    const response = await fetch("http://127.0.0.1:5500/Async-await.html");
    const json = await response.json();
    console.log(json); // 에러
    throw Error("Ay Caramba!"); // 에러!
  } catch (e) {
    console.log(e); //
  }
};

getMoviesAsync();
```

**catch 는 await 뿐아니라 try 안에 있는 에러를 모두
잡아낸다.**

#

#### finally

---

```javascript
const getMoviesAsync = async () => {
  try {
    const response = await fetch("http://127.0.0.1:5500/Async-await.html");
    const text = await response.text();
    console.log(text);
    throw Error("Ay Caramba!");
  } catch (e) {
    console.log(e);
  } finally {
    console.log("we are done");
  }
};

getMoviesAsync();
// 결과
// text 형식으로 변환한 Promise 객체 출력
// Error: Ay Caramba! at getMoviesAsync
// we are done
```

**finally는 결과에 상관없이 메시지를 띄운다.**
