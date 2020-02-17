# NextJS Project 배포

1. NextJS project의 script 추가

    ```
    "scripts" : {
        ...
        "build" : "next build",
        "export": "next export"
    } 
    ```
   - build script 를 변경하면, zeit project setting의 build command도 같이 바꿔야할듯. 둘이 다르면 deploy fail 됨
2. ZEIT 연동
   1. ZEIT 가입 [링크](https://zeit.co/onboarding)
   2. 새 프로젝트 생성 [링크](https://zeit.co/new) 
       - 이미 존재하는 프로젝트를 사용한다면 GitHub, GitLab, BitBucket에서 가져올 수 있음
   3. 2번에서의 프로젝트에서 Next.js App을 import
   4. deploy가 자동으로 실행됨
3. 배포된 화면 확인하고 끝!!!!

- 참고 링크
  - https://nextjs.org/docs/deployment

---

## 내가 막혔던 부분
1. root directory 설정을 잘못함.
    - 내 nodebird 앱은 front directory 가 next로 되어있고, front directory에서 build를 해야하기 때문에, root directory가 front였음.
    - zeit project settings에서 root directory 수정함.
2. redeploy를 수동으로 못해서 App import 되어있는 link를 끊고 다시 link 해서 자동으로 deploy 시작하게하는 삽질을 함
    - zeit는 link 되어있는 프로젝트의 메인 브랜치(나는 master)에 push event가 발생하면 자동으로 redeploy 해줌
    - 매번 redeploy하는게 싫으면 설정으로 바꿀수있을거같긴함. (안해봄)
    - 수동 redeploy도 있을 수는 있는데,, 아직 안찾아봄


