# Github Convention
유어슈 안드로이드 팀 협업 컨벤션

## Branch

- 개인 개발 브랜치

> feature/{nickname}/{feature-name}
>
예시) feature/comet/home

- 공용 개발 브랜치

> feature/{feature-name}
> 
예시) feature/home


## Commit
### Commit title
>  <타입> : <내용>
-  내용은 최대 50글자 정도로만 입력
-  1 Action 1 Commit

### Commit type
- chore: 자잘한 수정
- docs: README나 WIKI 등의 문서 개정
- feat: 새로운 기능 구현
- fix: 버그, 오류 해결
- refactor: 리팩토링

## Issue
### Issue template
- bug report
```
---
name: Bug Report
about: 버그 리포트
title: "[bug]"
labels: fix
assignees: ''

---

**어떤 버그인가요?**
> 어떤 버그인지 간결하게 설명해주세요

**어떤 상황에서 발생한 버그인가요?**
 - Device: [e.g. Android Emulator]
 - OS: [e.g. Android 13]
 - 숨쉴때 버전 [e.g. debug/release 1.3.5]

**버그 재현 방법**
1. Go to '...'
2. Click on '....'
3. Scroll down to '....'
4. See error

**스크린샷(선택)**

**이슈 체크리스트**
> 사이즈가 S 미만인 이슈는 따로 등록되지 않아도 괜찮아요
- [ ] 노션 이슈의 속성 설정하기 (우선순위, 사이즈, 태그(선택))
- [ ] 태스크를 시작하기 전, 노션에 예상 마감일자를 등록해주세요
```
- feature issue
```
 ---
name: Feature Issue Template
about: 기능 추가, 개선
title: "[feat]"
labels: feat
assignees: ''

---

**어떤 기능 또는 개선인가요?**
> 추가하려는 기능 또는 개선에 대해 간결하게 설명해주세요

**참고 자료(선택)**
> 피그마, 노션, 슬랙 링크 등

**작업 상세 내용**
- [ ] TODO
- [ ] TODO

**체크리스트**
> 사이즈가 S 미만인 이슈는 따로 등록되지 않아도 괜찮아요
- [ ] 노션 이슈의 속성 설정하기 (우선순위, 사이즈, 태그(선택))
- [ ] 태스크를 시작하기 전, 노션에 예상 마감일자를 등록해주세요
```

## Pull Request

### PR title

> [<레포 이름>-#<이슈 번호>] <내용>
> 
- <레포 이름> : Soomsil, YDS

### PR label
- chore: 코드 수정, 내부 파일 수정
- docs: README나 WIKI 등의 문서 개정
- feat: 새로운 기능 구현
- fix: 버그, 오류 해결
- help: draft PR시 사용
- refactor: 리팩토링

### PR review rule

- 기존 코드 수정 → 해당 코드 오너
- 새로운 파일 추가 → 랜덤지정
- approve 2개 이상 받으면 알아서 merge 하기

### PR template

```
## Summary
<!-- 무슨 이유로 코드를 변경했는지 -->
<!-- 테스트 계획 또는 완료 사항 -->

## Describe your changes
<!-- 변경 또는 추가된 코드, 관련 스크린샷 -->

## Issue

- close #{Issue number}

## To reviewers
<!-- 어떤 위험이나 장애가 발견되었는지 -->
<!-- 어떤 부분에 리뷰어가 집중하면 좋을지 -->

<!-- android-maintainer(안드로이드팀 액티브 멤버)를 멘션해요. 
     리뷰어를 여러 명 등록할 수 없어서 이렇게 하고 있어요. 
     알림을 보내고 싶지 않다면 아래 줄을 지워주세요. -->
@yourssu/android-maintainer 
```

### PR merge

- feature → develop : 스쿼시(squash) merge
- develop → main : 일반(with merge commit) merge
- hotfix → main : 일반 merge
