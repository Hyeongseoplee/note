## Javascript 에서 Instance 란?

요즘 리액트 공부를 하다보니 자바스크립트에 대한 이해가 얼마나 중요한지 깨닫고 있다.
모호한 instance의 개념과 class, prototype의 정의에 대하여 간단히 정리해본다.

## instance

비슷한 성질에 여러개의 객체를 만들려면 생성자 함수(constructor)을 이용하여 찍어내는데 이 떄 만들어지는 것이 instance라고 할 수 있다.  
요런거.

```javascript
User = function (name, age) {
  //생성자 함수 User
  this.name = name;
  this.age = age;
};

const user = new User("venny", "20"); // instance
```

객체지향언어에서 흔히 사용되는 class가 javascript 에서는 prototype이며 생성자 함수가 사용된다.  
즉, 클래스나 프로토타입을 이용해 만들어진 결과물(복제품)을 instance라고 할 수 있다.

## Class? Prototype?

class는 객체지향언어에서 정말 중요한 부분 중 하나로 다른 객체를 만드는 틀이라고 할 수 있다. javascript도 객체지향언어이지만 class 방식을 쓰지않고 prototype 방식을 쓴다.  
**즉, instance를 만드는 방법이 class만 사용하지 않는 다는 것만 빼고 똑같다!**

그래 알겠어. :)  
그런데 instance를 javascript에서 사용하는 이유가 뭘까? 왜?!
그 이유는 이렇다.
기본적으로 생성된 instance는 원래의 class나 prototype에서 쓰는 **메서드**나 **프로퍼티**를 상속 받기 떄문이다.

**상속(inheritance)은 뭘까.**  
javascript만 공부하던 때엔 상속에 대해서 단순히 어떤 값을 가져온다 라고만 알고 넘어갔었는데, 상속은 객체지향에서 정말 중요한 개념이라고 한다.  
상속을 통해 객체가 가지고 있는 메소드와 프로퍼티를 인스턴스에서도 사용할 수 있게된다.
물론 이떄 인스턴스는 기존 객체에서 확장하여 추가된 다른 개별 속성을 가질 수 도 있다.  
예를 들어 '쿠키'라는 객체로부터 만들어진 인스턴스 '쿠키1'의 속성은 초코쿠키가 될 수도, 버터쿠키가 될 수도 있다는 말이다.  
예제 코드

```javascript
Cookie = function(color){
    this.color = color;
}

const cookie1 = new Cookie('chocolate;);
const cookie2 = new Cookie('butter');

```
