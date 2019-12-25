git init
git 저장소 생성

git status
현재 파일들의 상태 확인

.gitignore
Project에 git을 관리하기를 원하지않는 파일을 설정
항상 최상위 dir에 존재

git add [filename]
tracked파일로 commit 대기

git add .
모든 파일을 tracked 상태로

git rm [파일명]
untracked 으로 되돌리기

git commit
git commit -m "커밋메세지"

로그인을 하지않은 경우
git config —global [user.email](http://user.email) "이메일"
git config —global [user.name](http://user.name) "이름" 

git commit -am "메세지"
add와 commit을 동시에 진행

git log
commit 내용 확인