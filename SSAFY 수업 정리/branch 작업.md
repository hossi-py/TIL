# branch 작업



git branch feature/(맡은 부분)

git branch  : 생성 확인

git switch 로 branch 이동

git push origin feature/(맡은 부분)

머지 리퀘스트가 나오는 것을 확인할 수 있다. 

비교 버튼을 눌러보면 코드 수정 확인 가능하다

머지 리퀘스트 만들기 누르면 수정사항 작성하고 만들기 누르면

master 요청으로 병합하자는 의견이 나오고 merge 버튼이 활성화 된다.(소스브런치 제거도 가능)

이후

git branch 치면 두 가지 나오고 git swich로 master 다시 이동

git pull origin master로 최신 버전을 다시 가져오고

이후 git branch -d feature/(맡은 부분)으로 지워준다.

git log --oneline 으로 수정사항 확인 가능하다. 



+++

작업 순서

`A(프로젝트 매니저) 와 B`

A가 ~/Desktop/ssafy4 위치에서 git init을 하면

 ~/Desktop/ssafy4 (master) 로 해당 폴더를 .git으로 관리하게 된다.

git push origin master로 git 프로젝트(pjt)에 업로드한다.

그리고 관리자는 B에게 권한을 주어야 한다.



B는 작업할 공간(폴더)에서 clone을 받는다.

A는 네비게이터 부분을 수정하고 B는 footer 부분을 수정하려고 한다.



수정을 하기 위해 master 아닌 본인의 branch로 이동해야한다.

A는

git branch feature/nav	(네비게이션 바를 수정할 것이다.)로 브랜치를 생성하고 (feature는 기능별 수정을 한다고 가정을 했기 때문에 임의로 작성해준 것이다.)

git branch로 생성 확인해준다.

git switch feature/nav 로 이동한다.

코드를 수정한 후

git add . 와 git commit을 한다.



B는

git branch feature/footer 로 브랜치를 생성하고

git switch feature/footer로 이동하여 코드를 수정한다.

git add.와 git commit를 한다.



A, B 수정이 모두 완료됐으면 master 브런치에서 최종 병합이 되어야한다.

gitlab이 가지고 있는 기능을 사용하려고 한다. (merge requset 보내기)



A와 B 모두 본인의 branch에서 push를 할 것이다.

A

```bash
$ git push origin feature/nav
```

해당 상태에서 gitlab에 들어가보면 2 Branch로 바뀐 것을 볼 수있다.

이 링크를 누르면 feature/nav 브런치 커밋을 확인할 수 있다.



B

```bash
$ git push origin feature/footer
```

하면 3 Branch로 바뀐 것을 볼 수 있다.



`비교`를 눌러보면 master branch와 비교하여 어떤 변화가 생겼는 지 확인할 수 있다.

비교 된 브라우저 창에서 `머지 리퀘스트(MR) 만들기` 를 누르면 

Description 부분에 어떤 부분을 수정했는지 작성을 하고, Submit 머지 리퀘스트를 누르면 병합 요청을 한다.

이때 초록색 merge 버튼이 활성화 되며 해당 기능을 완벽히 구현한 브런치라면 Remove source branch로 해당 branch를 제거해주어야 한다.

프로젝트 메인 페이지로 가면 merge 된 것을 확인 할 수 있다.



새로 생성한 branch가 해야할 일을 다했다면

A는

git switch master 로 이동하고

git pull origin master로 최신 정보를 받아온다. 최신 정보를 받아 온 후

git branch -d feature/nav 로 브런치를 삭제한다. 



B도

git switch master 로 이동하고

git pull origin master로 최신 정보를 받아온다. 최신 정보를 받아 온 후

git branch -d feature/footer 로 브런치를 삭제한다. 





+++

머지 충돌??

동일한 곳을 바꿔줬기 때문이다.

충돌 해결 버튼 누르고 커밋 누르면 된다.

머지를 마지막으로 누르면 된다.



+++

참고

rm -rf .git ( 커밋 지우기 ) = (master) 가 없어진다.

+++

python manage.py loaddata movies.json ( 제이슨 파일 불러오기)