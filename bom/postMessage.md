<br>

- BOM은 iframe에서 부모 페이지의 BOM에 접근하기 위한 window.parent를 제공한다.
- BOM은 window.open으로 열린 페이지에서 부모 페이지의 BOM에 접근하기 위한 window.opener를 제공한다.
- 그러나 위와 같이 하는 것은 Same-origin policy 를 위배하지 않는 선에서만 사용이 가능하다.<br>
(BOM에 접근할 때 기본적으로 Same-origin policy를 따르기 때문) <br>
var win = window.open('http://google.com', ''); <br>
win.document.getElementsByTagName('a')<br><br>
<b>Blocked a frame with origin "https://github.com" from accessing a cross-origin frame.</b> <br>


# window.postMessage()

- window.postMessage(data, [ports], targetOrigin)
  - data : 전달할 메시지
  - ports: 메세지 포트 (생략 가능)
  - targetOrigin : 메시지 수신받는 도메인. 제한하지않으려면 *로 지정
- safely enables cross-origin communication between Window objects; <br>
e.g., between a page and a pop-up that it spawned, or between a page and an iframe embedded within it.
- X-Document(알수 없는 문서)간의 통신에 대한 표준 API
- HTML5 스펙
- IE8 부터 지원

<img src="http://apress.jensimmons.com/v5/pro-html5-programming/images/ch6/fig6-1.jpg" width="90%"></img>

<br>

Security Concerns
- 
- targetOrigin을 *로 하지말고, 명확히 지정하라.
- 다른 사이트들에서 메시지를 받고싶지않으면 'message' 이벤트에 event listener를 등록하지말아야한다.
- 만약 메시지를 받아야한다면, 받은 메시지를 filtering하고, sender의 identity를 verify해야한다. 

<br>
<br>

참고 링크
- 
-  https://developer.mozilla.org/ko/docs/Web/API/Window/postMessage
- https://minukang.github.io/2017/11/29/x-document-messaging/
- https://jjeong.tistory.com/476
- https://www.hahwul.com/2016/08/web-hacking-html5-postmessage-api.html
