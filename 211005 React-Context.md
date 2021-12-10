## context and State management

#### 필요성

- 각각의 component에 필요한 데이터들을 최상단 부모의 state에 저장 후 props로 전달 받아 가져오는 것이 아닌, 필요한 데이터를 한 공간에 넣어 두고 component들이 필요할 때만 그 데이터를 찾게끔 한다.
- 즉, 값을 찾기 위헤 component의 할아버지의 고조할아버지까지 찾아 볼 필요가 없다.
- 데이터를 별개의 분리된 object에 보관한다.  
  => Reduc나 Usecontext를 사용하는 이유

---

#### context

: 내 어플리케이션의 데이터 저장소

```javascript
const { name } = useContext(가져 올 context)
```

context를 사용하기 위해 위와 같은 코드를 추가하면, react는 **입력된 context로 부터 provider를 자동으로 찾는다.**

#### provider

: context를 가져올 수 있게 하기위한 부모 같은 역할을 한다.

provider 안에 children(최상위 컴포넌트가 들어올 예정) 을 넣어서 provider가 provider 내에 속한 컴포넌트들의 부모가 되게끔 만든다.

```javascript
return (
  <UserContext.Provider value={{ user, logUserIn }}>
    {children}
  </UserContext.Provider>
);
```

children에 속한 컴포넌트는 provider로 부터 어떤 데이터도 가져올 수 있게 되었다~ :) 야호!

#### createContext

: context 객체를 생성한다.

> createContext(defaultValue)
> => provider, consumer 반환

---

#### 써보면 괜찮을 것 같은 곳

: 현재 진행중인 'kafuncha'프로젝트에서 fetch api 코드들을 전부 provider에 넣어서 하위 컴포넌트 들에서 쓸수 있게끔 하면 좋을 거 것 같다.

연습한 codesandbox link : https://codesandbox.io/s/nooks-forked-445m6

## Visitor

- [x] Venny
