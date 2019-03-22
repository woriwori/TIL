# Client Type

OAuth 2.0 은 2가지로 Client type을 나눈다. 

- **Confidential** : client passowrd를 안전하게 보관할 수 있는 client다. 
- **Public** : client password를 안전하게 보관할 수 없는 client다.
   
<br>   
   
# Client Profile

OAuth 2.0은 client profile 종류를 명세하고 있으며, 각 profile은 client type에 매핑될 수 있다.

- Web Application
  - web server를 통해 동작하며, 웹 브라우저에서 실행된다.
  - 일반적으로 브라우저 파트와 서버 파트를 가지고 있다. 
  - client password를 서버에 저장할 수 있기 때문에 Confidential client type이다.
  
  <img src="http://tutorials.jenkov.com/images/oauth2/overview-client-types-1.png" width="90%"></img>
  
- User Agent Application
  - 브라우저에서 실행되는 javascript application 
  - 여기서 브라우저가 user agent다. 
  - 이 어플리케이션은 아마 웹 서버에 저장되어 있을테지만, 실행은 user agent가 한번 다운로드한 이후에 된다.
  - 예를 들어, 브라우저를 통해서 실행되는 javascript 게임이다.
  - 아마.. html5를 통해 만들어진 게임을 스팀에서 다운받았다고하면, 그것도 여기에 속하지않을까? 서버를 통해서 게임 내용을 저장하지않으니까..
  - client password를 서버에 저장할 수 없기 때문에 Public client type이다.
  
  <img src="http://tutorials.jenkov.com/images/oauth2/overview-client-types-2.png" width="90%"></img>
  
- Native Application
  - 사용자의 데스크탑 또는 모바일에 직접 설치되는 application 이다.
  - client password가 사용자 device에 직접 저장되야하므로 Puiblic client type이다.
  
  <img src="http://tutorials.jenkov.com/images/oauth2/overview-client-types-3.png" width="90%"></img>
  
- Hybrid Application
  - Native App이 server 파트를 가지고 있어서, data를 server에 저장할 수 있는 앱들을 말할 수 있다.
  - 즉, web app의 속성과 native app 속성이 공존하는 application이 예다.
  - 얘는 oauth 2.0에서 말하는 profile에 속하지는 않는다.
  
