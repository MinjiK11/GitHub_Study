# 토큰 생성

- 인증
- 생성한 토큰은 안전한 곳에 보관 (유출 주의)
- 권한 지정 후 토큰 생성 (생성 후 권한 변경 가능)
- 비밀번호 대신 사용

# 소스트리 사용해보기

**clone → 업로드할 파일 선택, add → commit → push**

### Clone

- 원격 저장소의 내용 → 내 컴퓨터 복사

**Source Tree를 통해 저장소 클론**

- Clone or 복제/생성 메뉴 → github에서 생성한 저장소(Repository) 클론
    
    내 문서 아래 같은 이름의 디렉터리 생성
    

### Add (스테이지에 올리기)

- 커밋하기 전에 저장을 원하는 파일들을 묶는 것 → 커밋

### Commit

- 스테이지에 올라온 파일을 내 컴퓨터에 저장
    
    게임의 세이브 (언제든지 커밋한 시점으로 돌아갈 수 있음)
    
- 저장을 원하는 파일들을 묶어서 커밋 명령 수행

주의 사항

- 반드시 한 번에 하나의 논리적 작업만 커밋
    
    여러 작업 →여러 번 커밋
  
### Push (Github에 업로드)

- github에 커밋 업로드 → 공유, 복구 가능

- ❗Source Tree Push 오류
    
    [오류 메시지]
    
    git -c diff.mnemonicprefix=false -c core.quotepath=false --no-optional-locks push -v --tags origin main:main
    
    remote: Support for password authentication was removed on August 13, 2021.
    
    remote: Please see
    
    https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls
    
    for information on currently recommended modes of authentication.
    
    fatal: Authentication failed for '
    
    https://github.com/lemonaS2/github_test.git/'
    
    Pushing to
    
    https://github.com/lemonaS2/github_test.git
    
    오류가 나면서 완료됨.
    
    [오류 해결]
    
    인증 수단으로 비밀번호가 아닌 토큰 이용
    
    [[Git/GitHub] - 소스트리(Sourcetree)에서 push시 토근 인증 요구[remote: Support for password authentication was removed on August 13, 2021.] 오류 해결 방법](https://pingfanzhilu.tistory.com/entry/GitGitHub-소스트리Sourcetree에서-push시-토근-인증-요구remote-Support-for-password-authentication-was-removed-on-August-13-2021-오류-해결-방법)
    
    소스트리 우측 상단 설정 클릭
    
    저장소 설정 → 원격 경로 주소 부분 더블 클릭
    
    URL/경로 부분에 깃허브에서 생성한 “개인토큰@” 추가
    
    (기존: https://github.com/abc/a.git -> 변경: [https://토큰값@github.com/abc/a.git](https://%ED%86%A0%ED%81%B0%EA%B0%92@github.com/abc/a.git))
    

### 코드 뭉치 버리기

- 저장하지 않은 변경 내용 취소하기
- 마지막 커밋(세이브)으로 돌아가기

### checkout

- 특정 브랜치 (or 커밋)으로 돌아가기

### branch

- 가상의 작업 환경
- 기존 내용 유지한 채 새로운 내용 추가하고 싶을 때 사용
    기존 내용은 그대로 보존하면서 새로운 작업 환경 생성
- 최종본은 main 브랜치에
- 한 번에 하나의 브랜치에서만 작업 가능 (헤드 브랜치)
  
### merge

[Learn Git Branching](https://learngitbranching.js.org/)

- 하나의 브랜치를 현재 브랜치와 합치는 것
- merge 후에는 타겟 브랜치 삭제 가능

**Fast Forward**

- 헤드 브랜치에 변경 사항 X
- 병합 대상 브랜치가 헤드로부터 시작

**가지가 생겨난 경우**

![image](https://github.com/MinjiK11/hello-world/assets/97442492/f9f23da4-2b50-47b9-90af-7570025cabdf)


- 과거의 커밋으로부터 브랜치를 생성해서 작업
- 새로운 브랜치 작업 이후 헤드에 새 커밋
- 여러 브랜치 동시에 작업하면서 병합
- 여러 브랜치에서 동시에 변경한 파일 존재 → 충돌 발생 가능
    
    가장 최신의 내용 하나만 선택 (보통 타겟 브랜치에 존재)

## 충돌 해결하기, pull 
**pull**
- 서버의 내용이 최신일 경우
  깃헙의 마스터가 로컬의 마스터보다 앞서 있는 경우
- pull = fetch + merge
  
- ❗Sourcetree pull 오류
    
  [오류 메시지]
    
  ****Need to specify how to reconcile divergent branches****
    
    - merge의 방식을 명시하라는 에러
    
    [오류 해결]
  ![image](https://github.com/MinjiK11/hello-world/assets/97442492/f24166af-5a12-48dd-a8ed-19d88c055598)

**충돌**
- 주로 두 커밋이 같은 파일 동시에 편집할 경우 발생
- 수동으로 해결 (에디터 이용)
- Sourcetree 충돌 해결하기 → 저장소 것(타겟의 내용) 이용 or 내 것(헤드 브랜치의 내용)

**이전 커밋으로 되돌리기**

### reset (비추천)

- ‘이 커밋까지 현재 브랜치를 초기화’ Hard
    
    커밋 되돌리기
    
- push 하지 않은 커밋은 사라짐
- 강제 push 필요
      Sourcetree에서는 지원 X, 터미널 push --force 명령어 이용

**브랜치 만들어서 되돌리기**

- 되돌릴 커밋 대상으로 브랜치 생성
- checkout
- 변경 사항 수정 후 commit → main에 merge (충돌 해결; 저장소 것을 사용)
- 트리가 지저분해짐
**revert**

- Sourcetree ‘커밋 되돌리기’ (되돌릴 커밋 선택)
- revert 대상 커밋은 사라지지 않음
- revert 대상 커밋의 내용을 되돌린 새로운 커밋이 생겨남
- 충돌 발생 가능성 多
- 여러 커밋 되돌리기; 최신부터 순서대로 revert 반복 적용

**임시 저장 - Commit - -amend, Stash**
**브랜치 변경하기**

- 마지막 커밋과 현재 작업 디렉터리의 내용 다를 경우, 브랜치 변경 X
    
    (커밋하지 않은 변경 사항이 존재)
    

**작업 중인 내용의 임시 저장**

1. 브랜치1에서 임시 커밋을 함
2. 브랜치2로 체크아웃
3. 다시 브랜치1으로 돌아와서 작업을 이어서 마무리 짓기
4. 커밋 덮어쓰기 (commit - -amend); Sourcetree ‘마지막 커밋 정정’
    
    이전 커밋의 내용 기록 X
    
    push - -force (이전 커밋을 push 했을 경우)
    

**Stash**

- 다른 브랜치로 체크아웃하기 전에 현재 작업 내용을 저장하는 임시 저장소
1. Stash 생성
    
    새로운 파일 (add되지 않은 파일) → add 후 Stash 생성
    
2. 체크아웃 후, 원래 브랜치로 돌아오기
3. Stash를 Pop 하기
    
    Sourcetree ‘스태시 적용’
   
### Rebase

- 두 브랜치를 합칠 때 사용
    
    Source tree ‘재배치’
    현재 브랜치가 대상 브랜치 위로 올라감
    
- 커밋 히스토리가 깔끔하게 정리됨
- 이미 원격 저장소에 올라간 경우, 협업 하는 경우 위험함
  이미 원격에 있는 브랜치 rebase X

### 기타 주의사항

- 코드를 남기려고 주석 달지 말기
- 좋은 커밋의 단위
    
    원자적으로 쪼갤 수 없는 단위 (주로 함수)의 개발을 했다면 커밋
    
- 커밋 메시지
    
    첫 줄에 요약
    
    한 줄 띄우고 자세한 내용
