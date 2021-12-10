# Git & Github

## Brach

- #1 :Master 브랜치 생성(Main)
- #2 : 브랜치 2개 생성(happy ending& sad ending)
- #3 : syncronize(merge into happy and sad branch) - main 브랜치의 내용을 각 브랜치에 merge해준다.
- #4 : main 브랜치로 merge 하기.


#### Conflict

같은 라인의 변경이 이루어질 떄 merge 단계에서 conflict가 일어난다. 어떻게 해야할까?
친절하게도 VSC에서 conflict가 일어난 부분을 보여주고 어떤 branch의 내용을 쓸 지 선택의 기회를 준다. 

## Forking and Cloning

다른 repo를 내 품으로 가져오고 싶을 떄 쓴다.
Git page에서 가져오고 싶은 repo에 들어가 fork 버튼 클릭을 한다. 끝이다. 참 쉽다.
허나 여기서 끝이 아니다.
이걸 내 하드로 받아와야 물고씹고즐기고 뭐라도 할거아닌가. 하드로 받아오는 방법은 쉽다.
**Github Desktop > add > Clone repository**
가져온 그것을 내 맘대로 추가,변경 할 수 았게 되었다.

## Pull request

fork 해 온 작업물을 본 repo에 넣고 싶을 때 쓴다.
원본 repo에 들어간다.
**Pull request > New pull request
- fork 뜬 걸 기준(repository 단위라 해야 할 까?)으로 하겠다는 파란색 링크를 누른다.(- compare across forks : 설정하지 않을 시 해당 repo 내에 branch를 기준으로 compare chages가 일어난다.) 

- base repository(원본) 내에 수정을 일으킬 branch 와
head respositroty(내꺼) 내에 업데이트 할 내용이 들어있는 branch를 선택한다.

- Create puull request
