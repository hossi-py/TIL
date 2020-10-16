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

머지 충돌??

동일한 곳을 바꿔줬기 때문이다.

충돌 해결 버튼 누르고 커밋 누르면 된다.

머지를 마지막으로 누르면 된다.



+++

참고

rm -rf .git ( 커밋 지우기 )

+++

python manage.py loaddata movies.json ( 제이슨 파일 불러오기)