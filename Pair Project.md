# Pair Project

> branch : 가지, 분기 / 기능별

1. git init  => master(메인)
2. README.md 파일 생성
3. git commit
4. git log --oneline : 상태 확인
5. git log --all --oneline : HEAD의 위치에 상관없이 모든 commit을 보여줌
6. git log --all --oneline --graph



git branch => 현재 가지들의 목록을 보여줌

(init) 상태여서 메인 줄기만 보임

새로운 branch를 생성하면 메인 줄기(master)와 다른 줄기가 보임

git switch로 줄기 변경 가능 ( `*` 로 구분 가능)



commit의 흐름



​      (master)			(master) 줄기 - add command

Readme - add-<

​								 (crud) 줄기 (add라는 commit을 남기고 master branch로 이동)

따라서 줄기마다 작성된 코드가 다르다





+++

로그인 기능 branch 생성

login branch로 이동하여 코드 작성 ( 초록색 라인으로 구분 가능 )

다 작성되면 add,  commit해주기

사용자가 보는 것은  master

따라서 login이 master 코드에 반영이 되어야 한다. (**master 기준으로!**)

`merge`  : branch를 붙인다.

`git merge (branch name)`  : master가 가장 최근 commit으로 이동

(Fast-forward)

git log one line으로 HEAD에 master와 login을 가르킨다.

할 일이 끝난 branch는 삭제한다



+++

새로운 branch를 생성하고 commit을 해준 상태

master로 이동하고 main branch를 수정한다면?

수정 위치와 추가된 branch 코드의 위치가 다르다

merge 작업을 하려했는데 새로운 branch 위치와 동일한 곳에 master commit이 존재한다.

단 line by line으로 구분하는 것이 아니다.

이 상태에서 merge 하면

(Fast-forward) 가 아닌 (recursive)로 병합이 된다. => 코드 위치 충돌이 없을 때 정상 작동(Auto merge)



충돌이 일어났을 때:

```bash
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

```master|MERGING``` 현재 merging이 완료가 되지 않은 상태로 된다.

원하는 코드를 선택하면 된다.

다시 add와 commit을 하면 `master` 상태로 된다.



+++

가이드

1. 명세를 처음부터 끝까지 꼼꼼하게 읽는다.
2. 네비게이터 / 드라이버 서로 협업
3. 시간 or 기능 or 요청으로 역할 변경
4. README작성으로 끝



<방장>

A : 드라이버

장고 프로젝트 생성

.gitignore 생성

git init

git add .

git commit

git 사이트에 프로젝트 생성 (README 파일 체크 하지않기)

git remote

git push origin master

멤버 추가(팀원 / maintainer)

코드 작성 후 add commit push 깃랩에 업로드



B : 네비게이터

코드 가져오기

git pull

코드 수정

프로젝트 모두 끝나고 새로운 프로젝트 생성

git remote 하되  origin을 다른 이름으로 변경

git init

`git remote` A랑 연결된것과 본인이 연결된 것 나옴 