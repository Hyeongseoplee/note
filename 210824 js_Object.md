## Object

---

one of the Javascript's data types.
a collection of related data and/ or functionality.  
Nearly all object in Javascript are instances of Object.

#

### 1. listerals and properties

> - 객체를 만드는 방법엔 2가지가 있다.
>   직접 중괄호로 묶어 객체를 만드는 방법과 class로 객체를 만드는 방법이다.

```javascript
const obj1 = {}; // 'object literal' syntax
const obj2 = new Obj(); // 'object constructor' syntax
```

아래는 object관리의 이점을 알려주는 코드이다.

```javascript
// object 사용 전
function draw(heis, age) {
  console.log(heis);
  console.log(age);
}

const heis = "venny";
const age = 29;
draw(heis, age); // venny 29

const sheis = "chloe";
const herage = 25;
draw(sheis, herage); // james 25

// object 사용 후

const venny = { name: "venny", age: 29 };
const james = { name: "james", age: 25 };
function print(user) {
  console.log(user.name, user.age);
}

print(venny); // venny 29
print(james); // james 25
```

obj는 property 와 value로 이루어져 있다.

#

#### with Javascript magic (dynamiclly typed language)

```javascript
// can add properties later

venny.hasjob = true;
console.log(venny.hasjob); // true

// can delete properties later

delete venny.hasjob; //
console.log(venny.hasjob); // undefined
```

### 2. Computed properties

> - key값을 변수로 처리할 떄 쓴다.
> - \*key should be always string

```javascript
console.log(venny.name);
console.log(venny["name"]);
venny["hasJob"] = true;
console.log(venny.hasJob);

function printValue(obj, key) {
  console.log(obj.key); // undefiend 를 출력한다.
}

function printValue(obj, key) {
  console.log(obj[key]); // venny , 29
}

printValue(venny, "name");
printValue(venny, "age");
```

### 3. Property value shorthnad

```javascript
const person1 = { name: "bob", age: 2 };
const person2 = { name: "chanel", age: 3 };
const person3 = { name: "gucci", age: 4 };

function person(name, age) {
  return {
    name,
    age,
  };
}

console.log(person(person1.name, person1.age));
console.log(person(person2.name, person2.age));
console.log(person(person3.name, person3.age));
```

### 4. Constructor function

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
}

const bob = new Person("bob", 2);
const chanel = new Person("chanel", 2);
const gucci = new Person("gucci", 2);

console.log(bob);
console.log(chanel);
console.log(gucci);
```

함수로 객체를 만든다.

### 5. in operator : property existence check (key in obj)

> - obj 안에 key값이 있는지 확인한다. 있으면 true, 없으면 false를 반환.

```javascript
console.log("name" in venny); // true
console.log("age" in venny); // true
console.log("handsome" in venny); // false
```

### 6. for .. in vs for..of

> - for (key in obj)
> - obj 안에 모든 key값을 받아온다.

```javascript
console.clear();
for (key in venny) {
    console.log(key); // name, age, hasjob
```

> - for (value of iterable)
> - array 안에 모든 value를 받아온다.

```javascript
const array = [1, 2, 3, 4, 5];

for (value of array) {
  console.log(value);
}
```

### 7. Cloning

> - Object.assign(Target Object(will copy), [obj1, obj2...(will be copied])

```javascript
const redFruit = { name: "apple", rating: 9 };
const redFruit2 = redFruit;
console.log(redFruit2); // { name : 'apple', rating : 9}
// redFruit2은 redFruit 객체의 ref를 그대로 복사하여 같은 데이터를 가져온다.
```

```javascript
// old way
const redFruit3 = {};
for(key in redFruit){
    redFruit3[key] = redFruit[key];
}
console.log(redFruit3.name); // apple
console.log(redFruit3.rating); // 9

// new way
const redFruit4 = {};
Object.assign(redFruit4, redFruit); // 합친 데이터를 가져온다
console.log(redFruit4.name); // apple
console.log(redFruit4.rating); // 9

=

const redFruit4 = Object.assign({}, redFruit);
console.log(redFruit4.name); // apple
console.log(redFruit4.rating); // 9
```

Object.assign의 카피를 받을 때 공통 부분이 있다면 맨 뒤에 있는 객체에 의해 덮어씌워진다.

```javascript
// another example
const fruit1 = { color: "red" };
const fruit2 = { color: "blue", size: "big" };
const mixed = Object.assign({}, fruit1, fruit2);
console.log(mixed.color); // blue
console.log(mixed.size); // big
```

'color'라는 propery가 겹친다.  
이때 가장 뒤에 있는 obj의 값인 fruit2 의 color의 value인 'blue'가 mixed의 key값으로 덮어씌워진다.

## 오늘 배운 것

### HTTP

---

- 웹상에서 클라이언트와 서버 간에 데이터를 주고 받을 수 있는 프로토콜(통신 규약, 약속)
- HTTP 메소드에는 2가지 방식이 있는데, GET방식과 POST방식이다.

_메소드 : form과 backend 사이의 정보 전송에 관한 방식_

#

#### 1. GET

---

URL에 파라미터를 포함시켜 **요청**하는 방식이다.  
데이터가 노출되기 때문에 보안에 취약하며, 개인정보가 포함되지 않는 상황에서 캐싱을 하여 페이지 로딩 속도를 높일 때 사용된다.  
즉, 그냥 데이터를 받는게 목적일 떄
_e.g. 검색할 때_

#

#### 2. POST

---

파일을 보내거나, database에 있는 값을 바꾸는 뭔가를 보낼 때 사용.  
BODY에 데이터를 넣어 전송하고 GET과는 달리 길이의 제한이 없다. BODY에 데이터가 들어가기 때문에 GET보다는 보안상 유리하지만 민감한 데이터는 꼭 암호화해줘야 한다.  
즉, 무언가를 수정하고 추가하고 삭제하고 싶을 때.
_e.g. 로그인_

##### action

> <form method="POST" action= "데이터가 도착하게 될 URL"></form>

쓰면 해당 URL로 POST request를 보내준다.
쓰지않으면 똑같은(속해있는 URL에 request를 보낸다.

---

#### req.params

: 만들어진 url router 안에 있는 파라미터값을 받아온다.

```javascript
export const watch = (req, res) => {
  const { id } = req.params; // { id : ??}
  const video = videos[id - 1];
  return res.render("watch", { pageTitle: `Watching ${video.title}`, video });
};
```

#

#### req.body

: form에서 받아온 value의 javascript represtation.  
하지만 이를 사용하기 위해선 express 가 form을 이해할 수 있도록 만들어야한다.  
**(+ input의 name도 반드시 정의해주어야한다!)**

> app.use(express.urlencoded({ extended : true}))

우리가 사용할 수 있는 javascript object 형식으로 통역 해준다. 단, middleware에서 미리 사용을 해야한다
