## React basic

#### Object destructing

```javascript
import React from "react";

function DestructingObj() {
  const human = {
    name: "venny",
    age: 29,
    natiopnality: "Kor",
    favFood: {
      breakfast: "hambuger",
      lunch: "taco",
      dinner: "steak",
    },
  };

  const {
    name,
    age: difAge,
    favFood: { breakfast, lunch, dinner },
  } = human; // human object로 가서 anme, age라는 변수 값을 가져온다
  console.log(name, difAge, breakfast, lunch, dinner); // const age = human.age;
  return <h1>Nothing</h1>;
}

export default DestructingObj;
```

age를 다른 이름으로 만들어 주고 싶을 떄

> { age : 다른 변수명 }

객체안에 객체 값을 가져오고 싶을 떄

> favFood : {key1, key2, key3}  
> // human 객체 안에 favFood라는 객체 안에 들어가서 객체들을 뽑아온다.

```javascript
const {
  name,
  age: difAge,
  favFood: { breakfast, lunch, dinner },
} = human;
```

#### Spread Operator

---

배열을 펼쳐서(unpack) 하나로 만들어 준다.(on Array)

```javascript
import React from "react";

function Practice() {
  const day = ["Mon", "Tue", "Wed"];
  const otherDay = ["Thu", "Fri", "Sat"];

  const allDay = [...day, ...otherDay, "Sun"];
  // ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
  console.log(allDay);
  return <h1>Hey there.</h1>;
}

export default Practice;
```

객체를 펼쳐서 역시 하나로 만들어 준다.(on Obj)
어떤 컨텐츠를 다른 배열에 넣거나 두 개의 object를 합치거나, 복사본을 만들고 싶을 때 등 많은 경우에 사용한다.

#### map, filter, forEach, push, includes

---

map, filter, forEach, push 는 아는 내용이니 생략

> Array.includes() : 해당 string이 array에 있는지 체크한다.
