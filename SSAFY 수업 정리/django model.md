# Django model 생성

1. 프로젝트 생성 crud

2. 애플리캐이션 생성 articles

   settings 에 articles 등록

3. 애플리케이션/models.py 에서 클래스 생성 -> 모델 변경사항 발생

   ```python
   from django.db import models
   
   # Create your models here.
   
   # model 상속
   class Article(models.Model):
   
       # 글자 수 제한 (한글 50글자)  # string
       title = models.CharField(max_length=100)
   
       # 글자 수 제한이 없음
       content = models.TextField() # string
   
       # 생성시간 확인 (자동으로 현재 시간을 추가한다.) # datetime 객체
       created_at = models.DateTimeField(auto_now_add=True)
   
       # 글 수정할 때마다 그 시간을 저장	# datetime 객체
       updated_at = models.DateTimeField(auto_now=True)
   
   ```

   

4. python manage.py makemigrations 로 설계. (조건이 바뀔 때 마다 반복해줘야 한다.)

    -> migrations 파일 생성

5. python manage.py migrate 로 설계대로 생성. -> DB 적용 (테이블)

   > 5번 을 안해주면 테이블이 없기 때문에 값을 입력해도 변동이 없다.
   
6. ctrl shift p -> sqlite open database 입력하면 오니쪽 하단에 SQLITE EXPLORER 생성(db.squlite3 우클릭 으로 하는 것과 같다.)

7. articles_article 로 class가 넘어왔는지 확인한다.



## 편리한 기능 제공

pip install ipython django-extensions 설치!

django_extensions를 settings.py INSTALLD_APPS 에 등록



커맨드에 : python manage.py shell

곧바로 python shell 생성되고 직접 모델들을 입력해줘야함

나갈 때는 exit() 입력



> pip install ipython django-extensions pandas  : 주피터로 넘어가는 설치
>
> vs 코드에서 주피터 노트북으로 넘어가는 방법
>
> **주피터 파일을 manage.py의 같은 위치에 옮겨놓는다.**
>
> python manage.py shell_plus --notebook 입력하면
>
> 주피터 창이 열린다.
>
> 나중에 열어볼 때도 이러한 방법을 이용해야한다.





## DB 에 값 저장하기



커맨드에 : python manage.py shell_plus 

장고에 필요한 모델들이 import가 자동으로 된다.



## Create

​	**첫번째 방법**



1. Article.objects.all()

   > 데이터 조회

models.py 을 DB에 요청 (SQL)

QuerySet으로 응답을 받는다.



2. 글을 작성 (create) / 모델 클래스로부터 인스턴스 생성
   article = Article()

3.  article 

   객체가 만들어짐 (DB에 저장되어 있지 않음.) = pk 값이 None

4. 글의 제목 작성

   article.title = 'first'

5. 인스턴스로 클래스 변수 접근 . 인스턴스변수 변경

   article.content = 'django!'

6. 저장 (DB 테이블에 한 줄이 작성된다.)

   article.save()

7. pk 값이 1이 됨.

   article

   

   **두번째 방법**

8. 값을 바로 입력해보자.

   article = Article(title='second', content='django!')  = 키워드 인자 함께 작성

9. 저장

   article.save()

   

   **세번째 방법**

10. Article.objects.create(title='thrid', content='django!!')  = 곧바로 save 됨 (처음으로 return이 나옴)

    ### 출력해보기

    models.py 에 함수 만들기

    

    ```python
class Article(models.Model):
        
        ~~
        
        def __str__(self):
            #return self.title
            return f'{self.pk}번 글의 제목은 {self.title} 입니다.
        
    ```
    
    함수는 makemigrations을 안해도 된다.

    

    #### 명령어

    - Article.objects.all()

      - objects == manager
    
      ​       class <=> DB API를 연결해줌 따라서 objects 앞에는 class가 와야한다.
    
    - Article.objects.get(pk=1)
    
    - article = Article.objects.get(pk=1)
    
    - article
    
    - python manage.py createsuperuser : 아이디와 비밀번호를 작성하면 보안단계를 검사한다.
    
    - runserver 후 admin에 아이디 패스워드를 입력해본다.



### READ

`all()`

- QuerySet return
- 리스트는 아니지만 리스트와 거의 비슷하게 동작한다. (조작이 가능)



`get(pk=)`

- 객체가 없으면 `DoesNotExit` 에러가 발생
- 객체가 여러 개일 경우 `MultipleObjectReturned` 에러 발생
- 객체가 반환



`filter(pk=)`

- 지정된 조회 매개변수와 일치하는 객체를 포함하는 QuerySet을 return
- pk가 없으면 빈 Query Set 반환



`order_by()`

- 오름차순(`pk`) / 내림차순(`-pk`) or `.all()[::-1]` 으로 정렬 가능



### Update

> 몇번 글을 수정할 것인가? -> `.get()`으로 선택해야 함.
>
> `.save()` 필수!



### Delete

`.delete()` 입력하면 지워진 값이 리턴된다.



## 관리자 사이트에 모델 등록

admin.py 에 입력

```python
# 명시적 상대경로 표현
from .models import Article

admin.site.register(모델명)
```













