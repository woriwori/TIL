# focusout 과 click event 의 충돌

- Create 페이지에서 input창에서 focusout할때와, Save 버튼을 클릭할 때 validation check를 하도록 해놨는데,
input 창에 값 입력 후 바로 Save 버튼을 클릭하면, focusout event만 불리고, click event가 불리지 않는다.
- 이유는 focus event가 click event보다 먼저 불리기 때문. 
- event bubbling 현상도 아니기 때문에 event.preventDefault 같은 건 의미가 없다. 

<br>

### 해결 방법
- mousedown event 활용
  - mousedown -> focusout -> click 순서로 event가 불리기 때문에 실제 mousedown에 click과 동일한 event handler를 등록해놓으면, 
    mousedown, focusout event만 불려서 해결이 된다.
    
<br>

### 다른 방법
- 검색할때 찾은 예시는, 자동완성이었다. 검색창에서 focusout시 자동완성 리스트가 사라져야하는데, 자동완성 리스트를 클릭하려할때, focusout 이벤트때문에 자동완성 리스트 클릭은 안되고 리스트만 사라져버리는게 이슈였다.
- 이에대한 해결 방법은, 3가지였다

<br>

1. focusout에 timeout 걸기
   - focusout되었을때 바로 자동완성 리스트를 사라지게 하지않는 것이다.
   - 하지만 이건 사용자별로 자동완성 리스트가 너무 늦게 사라진다 느낄 수도 있고, 실행 환경에 따라서 다른 결과가 나올 수도 있다고한다..
2. jquery event 순서 변경
   - 자동완성 리스트와 검색창을 포함한 부모 dom의 event list를 받아서 click 과 focusout event의 순서를 변경하는 것이란다...
3. 마우스 위치 이벤트
   - 마우스가 자동완성 리스트안에 있지 않을때만 자동완성 리스트를 사라지게 하는 것. 
4. mousedown event 활용
   - 내가 사용한 해결방법으로 해결이 가능하다.
  
<br>

### 결론
- 내 이슈를 mousedown event 로 해결한 이유는 아래와 같다.

<br>

1. focusout 에 timeout 걸기
   - 사용자가 불편해하지않을 타이밍을 찾기 어려워서 탈락.
2. jquery event 순서 변경
   - 번거로워서(?) 탈락.
3. 마우스 위치 이벤트
   - validation check 공통 로직을 쓰기 때문에 focusout event 핸들러 함수가 공통함수이다.
이 공통함수에서 마우스가 특정 dom 에 위치했는지를 명시하는건 이상하기 때문에(?) 탈락.
4. mousedown event 활용
   - TOP에서 onClick과 onMousePressed에 이벤트 핸들러를 같이 등록하면 해결되기 때문에 굉장히 깔끔!



- 참고
  - https://vnthf.github.io/blog/jquery-focusout%EA%B3%BCclick-event%EC%B6%A9%EB%8F%8C/
  - https://stackoverflow.com/questions/13980448/jquery-focusout-click-conflict

