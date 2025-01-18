## Android 팀 배포 플로우



### 개요

Android 팀의 배포 프로세스를 효율적으로 관리하고 모든 팀원이 일관되게 작업할 수 있도록, 배포 플로우를 정리한 문서입니다.

### 1. 브랜치 전략

- `main` branch: 안정된 코드를 유지하며, 최종 배포를 위한 branch



- `develop` branch: 개발 중인 기능을 통합하는 branch



- `feature` branch: 각 기능별로 분리된 branch
  - 명명 규칙 :  github convention 참고 //TODO 파일 위치 링킹



### 2. 버전 관리

`Semantic Versioning` (SemVer) 규칙 사용 

`MAJOR`: 주요 변경 사항, 이전 버전과 호환되지 않는 큰 변경이 있을 때 증가 (예: API 변경, 큰 디자인 개편)

`MINOR`: 새로운 기능이 추가되었지만, 이전 버전과 호환이 유지될 때 증가

`PATCH`: 버그 수정이나 사소한 변경 등, 호환성을 해치지 않는 수정 사항에 대해 증가

```
1.0.0 → 첫 번째 정식 출시 버전.

1.1.0 → 새로운 기능이 추가되었을 때.

1.1.1 → 버그가 수정되었을 때.
```


`versionCode`라는 정수 값을 사용하여 각 버전을 고유하게 식별한다.

이는 Play Store에서 업데이트를 관리하는 데 사용되며, 항상 증가해야 한다.

```
versionCode=1 (초기 릴리스)

versionCode=2 (첫 번째 업데이트)
```
version.properties 또는 build.gradle 파일에서 관리된다.

```
versionCode 2
versionName "1.1.0"
```


자세한 설명은 [공식문서](https://developer.android.com/studio/publish/versioning?hl=ko#versioningsettings)를 참고해주세요.



### 3. 배포 준비



1. Develop 브랜치에서 Release 브랜치 생성

2. 릴리스 관련 설정 업데이트 (버전 이름, 버전 코드 등)

3. Release 브랜치에서 서명된 APK 생성 및 빌드 확인

4. 스토어 등록 정보 수정

5. versionName 및 version properties 파일에서 버전 정보 수정

6. 스토어 업로드 및 Github Actions 실행

    6.1. `스토어 업로드 및 Github Actions 실행`은 수동으로도 가능하며, 자동으로 관리를 원한다면 [Soomsil 배포 플로우](./release-flow-docs./Soomsil) 확인

7. 스토어 등록 후 Main 브랜치에 병합

8. Main 브랜치에서 태그 생성 및 푸시

9. GitHub Release 태그 생성 및 관리



#### GitHub Release 태그 생성 시 과정



1. **Tag version**: v버전명 형식으로 작성 (예: v1.2.3)



2. **Target**: 릴리스할 브랜치나 커밋 선택 (보통 main)



3. **Release title**: 릴리스 이름 작성 (예: Release v1.2.3)



4. **Description**: 변경 사항 및 릴리스 노트 추가







### 4. 배포 후 모니터링



배포 후 Google Play Console 및 Crashlytics를 통해 에러 모니터링할 수 있습니다.