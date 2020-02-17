# NextJS Project 배포

1. NextJS project의 script 추가

    ```
    "scripts" : {
        ...
        "build" : "next build"
    } 
    ```
   - build script 를 저거말고 딴걸로 하면 에러남
   - zeit project setting의 build command를 같이 바꿔도 안됨.. 이유는 모르겠음
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
## 팁
- Deployments 탭
   - redeploy는 deploy 결과가 Error 인것만 가능하다. (근데, 상태가 Error였던 커밋에서 redeploy하는 거라서.. 똑같이 Error될 확률이 클듯.)
   - 커밋 별로 deploy 결과물을 확인할 수 있다. "Promote to Production"을 선택.
   - https://{GitHub repository명}.now.sh/ 에서는 가장 최근에 성공한 deploy 결과물을 확인
---

## 내가 막혔던 부분
1. root directory 설정을 잘못함.
    - 내 nodebird 앱은 front directory 가 next로 되어있고, front directory에서 build를 해야하기 때문에, root directory가 front였음.
    - zeit project settings에서 root directory 수정함.
2. redeploy를 수동으로 못해서 App import 되어있는 link를 끊고 다시 link 해서 자동으로 deploy 시작하게하는 삽질을 함
    - zeit는 link 되어있는 프로젝트의 메인 브랜치(나는 master)에 push event가 발생하면 자동으로 redeploy 해줌
    - redeploy가 안됐던 때가 있었는데 그 이후에 그게 재현이 안되서 원인 파악이 안됨
    - 현재는 Deployments 탭에서 상태가 Error인것만 수동으로 redeploy 가능


