# 콜백함수(Callback Function)

#

#### 정의

---

다른 코드의 인자로 넘겨주는 함수.  
쉽게 말하면 되돌아 호출해달라는 명령이다.  
어떤 함수 X를 호출하면서 '특정 조건일 떄 함수 Y를 실행해서 나에게 알려달라'는 요청을 보냅니다.
이 요청을 받은 함수 X의 입장에서는 해당 조건이 갖춰졌는지 여부를 스스로 판단하고 Y를 직접 호출합니다.

> **이처럼 콜백 함수는 다른 코드(홈수 또는 메서드)에게 인자로 넘겨줌으로써 그 '제어권'도 함께 위임한 함수이다.**

```javascript
let count = 0;
let cbFunc = function () {
  console.log(count);
  if (++count > 4) clearInterval(timer);
};

const timer = setInterval(cbFunc, 1000);
```

#

해석 : 위 코드에서 setInterval에 전달한 첫 번쨰 인자인 cbFunc 함수(이 함수가 곧 콜백 함수이다)는 0.3초마다 자동으로 시행됩니다. 콜백함 수 내부에서는 count 값을 출력하고 count를 1만큼 증가시킨 다음, 그 값이 4보다 크면 반복 시행을 종료하라고 합니다.

#

#### 콜백함수의 예

---

setTimeout(), setInterval(), forEach(), map() 등의 함수들은
첫번째 인자로 콜백함수를 받아 원하는 조건에서 직접 호출한다.
