# Promise

#### Promise.all

---

주어진 모든 promise를 실행한 후 한번에 리턴된 promise 배열을 반환한다.  
각각의 promise가 언제 끝나는지에 상관없이 전부 끝났을 떄 그 api 데이터들을 순서에 맞춰 배열로 건네준다.

- 단 받아진 순서대로가 아닌 요청 후 순서대로!
- 하나라도 reject가 되면 error를 띄운다.
  (then, cathch 같은 것들을 더 이상 넣지 않고 제대로 작동되는지, 실제로 진행되는지 확인할 때 좋다)

#

```javascript
const p1 = new Promise((resolve) => {
  setTimeout(resolve, 10000, "first");
});

const p2 = new Promise((resolve) => {
  setTimeout(resolve, 1000, "second");
});

const p3 = new Promise((resolve) => {
  setTimeout(resolve, 3000, "third");
});

const motherPromise = Promise.all([p1, p2, p3]);

motherPromise.then((values) => console.log(values));
```

#

#### Promise.finally

---

Promise가 성공하거나 실패했을 떄 결과에 상관없이 뭔가 하고 싶을 떄 쓴다.

> then().catch().finally()

```javascript
const p1 = new Promise((resolve, reject) => {
  // js 비동기 처리에 사용되는 객체를 만들어 변수 p1에 담는다
  setTimeout(reject, 3000, "first");
})
  .then((value) => console.log(value))
  .catch((e) => console.log("e"))
  .finally(() => console.log("Im done"));

// 결과 : e / I'm done
```

#### Promise 실제 적용

---

```javascript
// "이 서버로 요청해줘"
fetch("https://yts.mx/api/v2/list_movies.json")
  // then : "요청 끝나고나서 이 할일(함수)을 해줘", promise 리턴하고 이행했을 때, 거부했을 떄를 위한 두 개의 콜백 함수를 인수로 받는다
  // response : API에서 요청으로 전달받은 값
  .then((response) => {
    console.log(response);
    return response.json();
  }) // 위 url에서 전달받은 값을 json 형식으로 받아 retrun 한다.
  .then((json) => console.log(json))
  .catch((e) => console.log(`${e}`));
```
