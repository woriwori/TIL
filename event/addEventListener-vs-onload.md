# 자바스크립트에서 이벤트 다루는 방법

1. HTML에 inline 등록 <br>
   -  \<div onclick="alert('hi')>Click!\</div>
   - html은 document만 표시하고, 핸들러는 js에서 처리하도록하기 위해,
     2,3번 방법이 더 자주 사용됨.
2. onload 속성 사용
   - document.getElementById('id').onclick = function(){}
   - 같은 dom에 onclick을 여러번 등록하면, 가장 마지막에 등록된 핸들러만 실행된다.
   - 외부에서 dom element에 직접 접근해서 수정하면(개발자도구로) 로직으로 등록해놓은 핸들러에 덮어씌워지는 것..
      
3. addEventListener/attachEvent 이용한 등록
   - document.getElementById('id').addEventListener('click', function(){})
   - 같은 dom에 onclick을 여러번 등록하면, 등록한 모든 핸들러가 등록 순서대로 실행된다.
   - 3번째 인자로 상위 ele에서 이벤트 캐치하느냐, 하위 ele부터 타고올라오냐를 설정 가능.
 
 
 
 - 참고 링크
    - https://unikys.tistory.com/312
 
