# OAuth 란? 
> OAuth 2.0은 다양한 플랫폼 환경에서 권한 부여를 위한 산업 표준 프로토콜입니다.
간단하게 인증(Authentication)과 권한(Authorization)을 획득하는 것으로 볼 수 있습니다.
- 인증: 시스템 접근을 확인하는 것 (로그인) -> 인증만 하는 것은 openID
- 권한: 행위의 권리를 검증하는 것

<br>

## OAuth의 배경
- 트위터 주도로 OAuth 1.0으로 시작
- OAuth 1.0a 부터 표준이됨. 
- 3rd party App 에 id/pw를 제공하지 않기 위함. (3rd party App을 못믿는것임)
- 또한, id/pw만 있으면 모든 권한을 가질 수 있고, pw 변경하면 앱은 동작도 안되고, 
권한 폐기하려면 pw변경해야함;

### OAuth 1.0은?
- 3-legged-auth 라고 해서, User/Consumer/Service Provider로 구성됨.

<img src="https://i2.wp.com/earlybird.kr/wp-content/uploads/2013/02/oauth2_triangle2.png?w=624"></img>


### OAuth 1.0의 단점? 
- 암호화가 필수가 아니라서 직접 암호화를 해야함
- 인증토큰(access token)이 만료가 안됨.
- User/Consumer/Service Provider의 구성으로는 대규모 서비스로의 확장이 어려움.
- 구현이 복잡하다고함..

<br>

## OAuth 2.0
- 구현 단순화
- 2.0부터 표준이됨.
- https가 필수라서 암호화는 https에 맡김.
- 1.0a는 인증방식이 1개였지만 얘는 다양함
- Resource Owner / Client / Resource Server / Authorization Server로 인증서버를 분리해서 가져감.. 

### 구성
- **Resource Owner** : 사용자! User!
- **Client** : Resource Server에서 제공하는 자원을 사용하는 앱
  (e.g. Facebook의 뉴스피드를 모아서 보여주는 앱)
- **Resouce Server (API Server)** : 자원을 제공하는 서버 
  (e.g. Facebook)
- **Authorization Server** : 사용자의 동의를 받아서 권한을 부여하는 서버. (access token을 제공해주는 서버)
  (e.g. Facebook (보통 Resource server와 같은 곳에 있다함.))

### 인증 타입
- Authorization Code Grant 
  - 인증코드를 통해 얻은 access token을 Client가 보관해서 Resource Server에 접근하는 방식
  - Client에 access token을 저장할 수 있는 환경이 되어있는 경우.. 
  - access token을 직접 Resource Owner에게 노출하지 않기 때문에 Implicit보단 상대적으로 보안이 좋다고볼수 있는..
  - (e.g. Web Application(일반적으로 서버파트까지 가지고있는 그런..)

<img src="https://developers.payco.com/static/img/@img_guide2.jpg"></img>

- Implicit Grant
  - access token을 보관할 수 있는 Client 환경이 안되서, Resource Owner에게 직접 access token을 전달하고,
    Resource Owner가 직접 그 token으로 Resource Server에 자원을 요청하는 방식
  - (e.g. Javascript Application / Mobile, Desktop의 Native App)
  - 약간 우리 ProZone Portal 같음.. token을 시스마스터에서 직접 받아와서 그걸 브라우저의 session storage에 저장하고 있기때문;

- Password Credentials Grant
  - Client에 id/password를 저장해놓고, 이걸로 직접 access token을 받아오는 거다.
  - 로그인은 Client를 통해서하고, Client는 이걸로 Authorization Server에서 직접 access token을 받아온다.
    (즉, id/pw를 Authorization Server에서 갖고 있는게 아니라는 것!)
  - (e.g. ?? ProIaaS가 IaaS서버로 로그인하고, 이 서버가 내부적으로 sysmaster 인증서버에 직접 접근해서 token받아온다 생각하면 될듯? )

- Client Credentials Grant
  - Resource Owner(사용자) = Client 라고 한다.. 
  - 뭔지 모르겠음.

<br>

## 우리가 구현한 방식
- Implicit Grant 방식을 사용했다고한다. (?)

### 사전 작업
- 서버에 resource owner를 미리 등록한다. (구글 로그인 계정을 만들어놓는다 생각하면됨.)
- client는(구글 로그인을 통해 로그인을 허용할 별도의 서비스) 구글에 client자신을 등록해서 client id를 받는다.
  그리고 등록할때, 구글 로그인 성공 후 redirect 될 url을 등록한다.
--> 즉, 우리 OAuth server에는, OAuth 용 계정이 미리 등록되어있고 (math@tmax.co.kr / 1234) 
     ProZone Portal 에 대한 client id와, 로그인 후 redirect될 ProZone Portal url이 저장되어있음.

### 로그인 과정
  1) client id를 query string에 추가하여, Authorization Server로 로그인 페이지를 요청
  2) 로그인 페이지에서는 로그인 클릭시 id/pw를 Authorization Server로 전송
  3) 만약 미동의한 사용자인 경우 동의 페이지로 이동
  4) 동의 페이지에서는 Authorization Server로 동의 서비스만 콜
  5) access token이 있는 query string과 함께 ProZone Portal로 redirect된다.
  6) ProZone Portal은 access token을 사용해서 Authorization Server에서 User와 관련된 정보를 가져온다. 

<br>

## TODO
- access token을 받아서 실제 Prozone Portal 용 계정을 새로 추가해야한다.
- 만약 이미 ProZone Portal 계정이 있는 상태면, access token으로 받아온 정보로
  ProZone Portal 계정을 조회해서, 그 계정을 식별할 수 있는 token(우리가 항상써오던 그것ㅎ)을 받아와서
  그걸로 원래 하던대로 하면됨...

<br>

## 결론
- 좀 아쉬운건 보통 OAuth를 사용한다는건, 뭐 구글 로그인을 쓰면 구글드라이브랑 뭘 연동한다던가, 이런식으로
그 서비스를 직접 사용할 수 있고 그 권한을 구글 OAuth를 통해 받는건데
아직 우리쪽에는 그런 설계는 안되어있는 것 같음.
- OAuth를 도입한다면 OAuth를 통해 ProIaaS, ProPaaS등의 서비스에 대한 접근 권한을 모두 관리해야할거 같고,
그러기 위해서는 우리가맨날쓰던 token대신 OAuth 의 access token을 사용해야할듯. 
 
