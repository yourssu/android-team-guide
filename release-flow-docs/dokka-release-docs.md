### 현재 Handy Docs Link

[Handy](https://yourssu.github.io/Handy-Android/docs/0.x/)

---

### Dokka 배포 방법
Handy에서 Dokka를 통한 코드 문서화 진행 과정 시의 기록입니다. 참고해주세요.

1. **gradle 세팅**

```yaml
  jetbrains-dokka = { id = "org.jetbrains.dokka", version = "1.9.20" }
    
  plugins {
        alias(libs.plugins.jetbrains.dokka)
  }
```

2. **yml 파일 생성**

```yaml
- .github
    - workflow
       -release.yml
```

3. **yml 코드 작성 Workflow file (release.yml)**

```yaml
# workflow 파일명입니다.
name: release

# 워크플로우가 언제 실행될지 시점
on:
  push:
    branches:
      - main # main branch에 merge 또는 push될 때 실행

jobs:
  release:
     # 실행 환경
     runs-on: ubuntu-latest
     
     # steps: 작업 수행 단계입니다.
     
     steps:
          
          # echo
        - run: echo "Starting Release"
        
        
        # 현재 사용 중인 Java 버전은 11 그러나 
        # Android Gradle Plugin(com.android.application 버전 8.5.0)은 Java 17 이상을 필요
        
          name: set up JDK 17
        - uses: actions/setup-java@v4
          with:
            java-version: "17"
            distribution: "temurin" #JDK 배포판(distribution)을 temurin로
             
             # gradlew은 파일의 루트 디렉토리에 위치해야 함
             # checkout을 하지 않으면 gradlew을 찾지 못할 수 있음
          name: checkout
        - uses: actions/checkout@v4 # v4 사용
        
        # 파일 실행 권한 부여
          name: permissions
        - run: chmod +x gradlew
        
        # Dokka를 사용하여 HTML 파일을 생성
          name: Build Documentation
        - run: ./gradlew dokkaHtml
        
        # 생성된 HTML 파일을 gh-pages 브랜치에 배포
          name: Deploy Documentation to GitHub Pages
        - uses: JamesIves/github-pages-deploy-action@v4
        
          with:
            token: ${{ secrets.GITHUB_TOKEN }}
            branch: gh-pages # 배포 브랜치
            folder: compose/build/dokka/html # 배포하고자 하는 모듈의 html주소
            target-folder: docs/0.x/ # 배포될 파일이 저장될 위치
```

4. **배포**

    [참고자료](https://velog.io/@cmsong111/Dokka%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%9C-%EC%BD%94%EB%93%9C-%EB%AC%B8%EC%84%9C%ED%99%94-with-%EB%B0%B0%ED%8F%AC)