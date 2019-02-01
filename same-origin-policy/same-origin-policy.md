# Same-Origin Policy
- javscript상의 Cross-Domain 이슈에 대한 근본적인 원인. <br>
브라우저단의 프로그래밍에서 보안상의 이유로 다른 사이트간에 스크립트를 막는 정책
- 다른 사이트는 Origin으로 구분한다.
  - Origin: HTML Document에서는 domain(x.x.x), protocol(http, https..), port(:xx)로 정의되어진다.
  
<img src="https://cdn-images-1.medium.com/max/1600/1*nu_PWLTvnP_JB-9qxQCptw.png"></img>

<br>

해결 방안
- 
1. document.domain property
   - 서로다른 window(or frame)을 같은 도메인으로 설정할 수 있다면 액세스 가능. 
   - orders.example.com 과 catalog.example.com 는 document.domain=example.cm으로 설정하면 서로 액세스 가능.
2. CORS (Cross-Origin resource sharing)
   - CORS는 웹 서버에게 보안 cross-domain 데이터 전송을 활성화하는 cross-domain 접근 제어권을 부여합니다. <br>
   모던 브라우저들은 cross-origin HTTP 요청의 위험성을 완화시키기 위해 (XMLHttpRequest와 같은) API 컨테이너 내에서 CORS를 사용합니다.
   - request에 Origin header를 추가하면, response에서 Access-Control-Allow-Origin header를 주면서 서로간의 액세스를 허용해주는 방식
   <br>
   만약 Access-Control-Allow-Origin header에 * 가 들어가 있으면, requeste origin 상관없이 허용해주는 것
   <br>
   <img src="https://www.securityninja.io/wp-content/uploads/2015/10/cors.png"/>
   
3. Cross document messaging
   - window.postMessage
   
4. JSONP, Proxy...


참고
- 
- http://charlie0301.blogspot.com/2013/12/jquery-ajax-same-origin-policy-jsonp.html
- https://youreme.blog.me/110161899272
- https://bcho.tistory.com/tag/Same%20origin%20policy
- https://developer.mozilla.org/ko/docs/Web/HTTP/Access_control_CORS
- https://developer.mozilla.org/ko/docs/Web/Security/Same-origin_policy