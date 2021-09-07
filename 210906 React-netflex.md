## Make a netflix \_\_React

#### yarn add styled-reset

모든 스타일값 0

#### withRouter

라우트가 없는 곳에서 history,match,location 값을 가져올 떄 사용.  
link 대신에 사용이 가능하다.

#### append_to_response

여러개의 api 데이터를 얻기위해 각각 url을 호출할 필요없이  
특정 데이터를 콕 찝어 함께 불러와준다.

#### container와 presenter 패턴

> **container** : state 와 data를 가지고 api를 호출하여 기타 모든 로직을 처리한다.
> (데이터를 받아와서 처리하는것을 담당)  
> **presenter** : contatiner가 처리한 데이터를 가져와서 화면에 뿌려주는 역할을 하는 함수형 컴포넌트. 스타일을 담당한다.

**Container(자스 역할) + Presenter(html 역할) => index.js 로 묶는다.**

index로 묶으면 다른 컴포넌트에서 import 시 최종 경로 폴더만 입력하면 자동으로 index를 찾는다.  
즉, ./src/components/home 까지만 입력해도 자동으로 home.js를 본다. 폴더를 임폴트 시킨다고 이해하면 된다!

### Router Props

브라우저와 router를 연결하게 되면 router가 history API 를 이용할 수 있게되며  
각각의 route에 연결된 components에 props로 match, history, location 객체를 건네준다.

> Match :  
> <Route path>와 URL이 매칭된 대한 정보가 담겨져있다.  
> 대표적으로 match.params로 **path에 설정한 파라미터값을 가져올 수 있다.**

> Location :  
> 현재 페이지의 정보를 갖는다.대표적으로 location.search 로 현재 url의 query를 가져올 수 있다.

> history :  
> history객체는 브라우저의 history와 유사하다.  
> stack 에 현재까지 이동한 경로가 담겨있어 stack에 쌓인 몇번쨰 포인트로 이동이나 앞,뒤 페이지로의 이동이 가능하게 해준다.
