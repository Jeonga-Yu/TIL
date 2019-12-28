## Git
여러명의 개발자가 함께 프로그램을 개발하려면 누가 소스코드의 어떤 부분을 수정했는지, 어떤 부분을 수정해야 할 지 등을 관리해야한다. 이를 프로그램 버전 관리라고 하는데, 이러한 프로그램 버전을 관리할 수 있는 도구가 Git이다.
개발자에게는 필수적인 도구이다.

## GitHub(깃허브)
깃허브는 Git기능과 SNS기능을 함께 제공하는 웹 서비스로 GitGub 사가 운영하고 있다.

===

### git init
git 저장소 생성

### git status
현재 파일들의 상태 확인

### .gitignore
Project에 git을 관리하기를 원하지않는 파일을 설정
항상 최상위 dir에 존재

### git add [filename]
tracked파일로 commit 대기

### git add .
모든 파일을 tracked 상태로

### git rm [파일명]
untracked 으로 되돌리기

### git commit
git commit -m "커밋메세지"

### 로그인을 하지않은 경우
git config —global [user.email](http://user.email) "이메일"
git config —global [user.name](http://user.name) "이름" 

### git commit -am "메세지"
add와 commit을 동시에 진행

### git log
commit 내용 확인

### git remote add origin [원격저장소주소]
origin이라는 이름으로 원격 저장소 주소 등록

### git remote remove origin
origin 원격 저장소 삭제

### git push origin master
git push
원격 저장소에 commit 내용 저장

### git pull origin master
git pull
원격 저장소의 변경 내용이 로컬 작업 디렉토리에 받아지고(fetch), 병합(merge)된다

### git merge [branch 이름]
다른 branch에 있는 변경 내용을 현재 branch(예, master)에 병합 할 때

### git clone [저장소 주소]
클라이언트의 로컬 디렉토리가 비어있어야한다.
원격 저장소를 복제한다
저장소의 내용을 다운로드 받고 자동으로 init도 된다

### git branch
branch 목록 확인
* branch : 가지치기, 안전하게 격리된 상태에서 무언가를 만들 때 사용

### git branch [브랜치명]
브랜치 추가

### git checkout [브랜치명]
해당 브랜치상태(?)로 돌아가며, HEAD가 가리키는 브랜치가 변경된다. 그래프를 확인할 수 있는데 익숙해 져야해

### git checkout -- [파일이름]
로컬 변경 내용 되돌리기

### 기타
#### 콘솔에서 git output을 컬러로 출력하기
    git config color.ui true