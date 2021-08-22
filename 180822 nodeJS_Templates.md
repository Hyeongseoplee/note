# Templates

### HTML 로드하기

HTML을 화면에 로드하는 방법은 2가지가 있다.
하나는 controller에 필요한 html태그들을 직접 작성하는 것이다.  
하지만 그렇게 된다면 페이지별로 작성할 것이 너무나 많아지고 그런 페이지가 수십개라면 어떤 공통부분을 수정해야한 다는 것은 수십개의 태그를 하나하나 바꿔주어야 한다는 말이다.

#

그러한 불편함을 없애기 위해 '퍼그'라는 템플릿 엔진이 등장했다.  
템플릿을 이용해서 뷰를 만드는걸 돕는다.

### pug 사용하기

```
1단계) npm i pug
2단계) express에게 view 엔진으로 pug를 사용하겠다고 알린다. : app.set("view engine", "pug")
3단계) src 파일안에 views 디렉토리를 생성하여 pug 파일을 만든다.
4단계) render(pug 파일 이름)
*express가 views 디렉토리에서 pug파일을 찾도록 설정되어 있어서 따로 import 할 필요가 없다. express는 views 디렉토리에서 모든 view를 본다(참고한다?)*
```

```javascript
doctype html
html(lang="ko")
    head
        title Wetube
    body
        h1 Welcome to Wetube !!!
        footer 2021 wetube all rights reserved
```

완성

#

### express가 pug 파일을 찾는 법

---

```javascript
res.render(<pug 파일명>);
```

하지만 이대로 페이지를 render 하면 views 디렉토리를 찾는데 실패했다는 에러가 뜬다.
pug파일을 찾는 경로에 src 페이지가 빠져있기 떄문.

> cwd + /views  
> _cwd : current working directory_  
> -> node.js(서버)를 실행(기동)하는 디렉토리

이를 해결하려면 cwd를 wetuve/src로 바꿔주면 된다.  
즉, default valu를 바꿔주면 된다.

```
방법1) views 디렉토리를 src 바깥으로 빼준다. // bad
방법2) root 파일로 돌아와 app.set("views",  process.cwd() + "/src/views")) 를 입력해 cwd default를 /src로 바꿔준다. // good
```

render 성공.

### Partials

---

그런데 이때 한 가지 문제는
바로 pug 파일 내 태그들을 모두 복붙해서 다른 곳에도 붙여주기 때문에 반복되는 코드들이 있어 하나를 수정을 하려면 매우 번거로워 지는 것이다.
partials가 수정할 부분 하나만 바꾸면 모두 바뀌게 도와준다.

#### 방법

src내에 partials 디렉토리를 새로 만들고 그 안에 반복되는 코드(footer 따위)가 들어가있는 pug 파일을 새로 만들어 include 해준다.

```javascript
doctype html
html(lang="ko")
    head
        title Wetube
    body
        h1 Welcome to Wetube !!!
        include ./partials/footer.pug
```

#

### Extends

---

#### inheritance(상속)

: 레이아웃의 베이스를 만들어주고 각 파일에 extends 시켜준다.

#### blcok

:템플리의 창문역할.  
extends된 base를 기반으로 각각의 다른 contents를 넣을 수 있게 한다.

방법

1.  base.pug를 만든다.
2.  반복되는 코드를 넣는다.
3.  코드 내에서 각기 다른 내용을 넣어야하는 코드를 찾아 블록을 만들어 준다.  
     head @@@ -> block head (=다른 내용을 넣기 위해
    구멍을 뚫어 줌)
4.  각각의 파일들에  
    extends base.pug  
    입력
5.  block 을 채워준다.

### Conditional, Iteration, Each

---

pug는 자바스크립트 이므로 자바스크립트에서 쓰는 조건문, 반복문을 똑같이 쓸 수 있다.  
다만 형식만 다를 뿐이다.
공홈에서 확인하자.

Conditional link : https://pugjs.org/language/conditionals.html  
Iteration link : https://pugjs.org/language/iteration.html

### Variable

```
tag ${변수명} // 텍스트와 함께 쓸 수 있다.
tag =변수명 // 텍스트와 함께 쓸 수 없다.
```

### Mixin

---

코드 복붙을 피하기 위해 사용한 partial의 똑똑한 버전이라 할 수 있다.
여러 개의 단순한 코드 문자열을 표현하기 위해 쓴 partial와 mixin은 데이터를 넣으면 읽을 수 있기 때문에 페이지가 바뀔 때마다 같은 구조 안에서도 데이터를 바꿔줄 수 있다.
