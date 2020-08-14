# Django Project 만들기

> django mtv mdn 문서로 구체적인 내용을 확인할 수 있다.
>
> ```
> 이 칸에 있는 코드가
> 터미널 혹은 입력창에 쓰는 지 확인할 것!!
> ```



0. 작업 위치 확인

   

1. 프로젝트 생성

- ```bash
  $ django-admin startproject #firtst_webex 
  # 이후 : 만들고 싶은 프로젝트 이름
  # python, django 명령어들을 사용하면 안된다.
  ```

- master로 되어있지 않아도 상관없다. (git으로 관리를 하지 않는다는 뜻.)

- 프로젝트 이름과 같은 폴더와 manage.py 파일이 만들어진다.

- **manage 파일과 폴더가 있는 곳에서 vs 코드로 열기를 한다.**

- `ls` 명령어로 manage.py가 있는 곳으로 들어와있는지 확인한다.



2. 어플리케이션 생성

- ```bash
  $ python manage.py startapp articles
  ```

- 프로젝트 폴더의 **settings.py**로 들어간다.

- 33번째 줄 INSTALLED_APPS의 맨 위에 `'articles'` 를 입력한다.

- 최하단에 
  - LANGUAGE_CODE를       'ko-kr'
  - TIME_ZONE 을				 'Asia/Seoul'     로 바꾸어준다.



3. django sever 생성

> 터미널에서 ctrl + c 로 서버를 닫을 수 있다.
>
> `사이트에 연결할수 없음` 이라고 뜨면, 서버가 닫혀있거나, 서버를 닫고, 다시 켜준다.

```bash
$ python manage.py runserver
```

- 입력 후 https 주소창을 ctrl + click 하고, 성공적으로 설치되었는 지 확인한다.

  

- 프로젝트 이름 폴더의 **urls.py** 파일로 들어가고, urlpatterns 안에 index로 들어가게 하는 명령어를 import 하단에 입력한다. **주소로 가기 위한 `/` 를 입력해야한다.**

  - ```python
    path('index/', views.index)
    ```

    

  - articles의 views.py 에 접근 할 수 있도록 하는 명렁어를 **urls.py** 내에서 입력한다.

  - ```python
    from articles import views
    ```

    

  - **views.py** 안에서 index 함수를 만들어준다.

  - ```python
    def index(request):
    
        return render(request, 'index.html')
    
    #request 는 필수로 작성한다.
    # render 함수를 통해 html에서 작업이 완료된 것을 사용자에게 넘겨준다.
    ```

    

  - **articles 폴더 내에 templates 폴더를 만들고 그 안에 index.html 파일을 만들어 작성한다.**

    

  - 작성된 내용을 확인하기 위해 server 주소창 뒤에 `/index`를 입력한다.



## menu 리스트 만들어보기

1. **views.py** 안에서 메뉴 리스트 함수를 만든다.

```python
import random

def menu(request):

    menus = ['족발', '김치볶음밥', '치킨', '떡볶이']
    pick = random.choice(menus)
    context = {
        'pick': pick

    }
    return render(request, 'menu.html', context)
```

> context 는 딕셔너리이기 때문에 다음 변수를 지정할 때 `,`를 꼭 써야한다.

random.choice 를 위해 random을 import 해주어야한다.!

**이때 랜덤함수는 최상단에 입력해야한다.**



2. **templates** 폴더 안에 menu.html 을 만들어주고

pick 값을 받기 위해

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <h1>오늘의 저녁 메뉴는 {{ pick }}입니다.</h1>
</body>
</html>
```

**중괄호 2개**로 pick을 받는다. (변수 받는 방법)



## Variable routing 는 무엇일까?

> url 주소 자체를 변수로 사용하는 것을 의미한다. 변수값에 따라 다른 페이지를 연결 시킬 수 있다.



**urls.py** 파일에서 작성한다.

```python
path('<str:name>/dinner/', views.dinner),
```

```python
path('<str:name>/dinner/<int:people>/', views.dinner),
```

> **int 값**을 넣어주면 people에는 **숫자만** 들어와야한다.



## Throw Catch 만들어보기

> form 형식에 데이터를 작성하고 그 데이터를 받는 url 설정하기.

1. **urls.py** 에 throw path 작성하기

```python
path('throw/', views.throw),
```



2. **views.py** 에 throw 함수 만들기

```python
def throw(request):
    return render(request, 'throw.html')
```



3. **throw.html** 파일 만들어서 아래 코드 입력.

```html
<body>
  <h1>THROW 페이지 입니다.</h1>
  <form action="/catch/" method="GET">
    <label for="title">제목을 입력해주세요.</label>
    <!-- input 태그에 제목1 이라고 작성을 하면 어딘가에 title='제목1' 데이터를 catch에 전송-->
    <input type="text" id="title" name="title">
    <input type="submit">
  </form>
</body>
</html>
```



4. **urls.py**에 catch path 작성하기

```python
path('catch/', views.catch),
```



5. **views.py**에 catch 함수 만들기 (print 는 어떤 data를 갖고 있는 지 확인하기 위함. 안적어도 무방)

```python
def catch(request):
    print(request)
    print('*'*30)
    print(request.GET)
    print('*'*30)
    print(request.method)
    print('*'*30)
    print(dir(request))
    
    #GET : 요청이 get 방식임을 말함
    #get : 딕셔너리에서 키값 받아오는 명령어
    data = request.GET.get('title')
    context = {
        'data':data
    }
    return render(request, 'catch.html', context)

```

```python
print(request)

<WSGIRequest: GET '/catch/'>
```

```python
print(request.GET)

<QueryDict: {}>
```

```python
print(request.method)

GET
```

```python
print(dir(request))

['COOKIES', 'FILES', 'GET', 'META', 'POST', '__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', '_current_scheme_host', '_encoding', '_get_full_path', '_get_post', '_get_raw_host', '_get_scheme', '_initialize_handlers', '_load_post_and_files', '_mark_post_parse_error', '_messages', '_read_started', '_set_content_type_params', '_set_post', '_stream', '_upload_handlers', 'accepted_types', 'accepts', 'body', 'build_absolute_uri', 'close', 'content_params', 'content_type', 'csrf_processing_done', 'encoding', 'environ', 'get_full_path', 'get_full_path_info', 'get_host', 'get_port', 'get_raw_uri', 'get_signed_cookie', 'headers', 'is_ajax', 'is_secure', 'method', 'parse_file_upload', 'path', 'path_info', 'read', 'readline', 'readlines', 'resolver_match', 'scheme', 'session', 'upload_handlers', 'user']

이 중 GET 과 POST만 기억해주면 좋다.
```



6. **catch.html** 만들고 아래 코드작성

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <h1>CATCH 페이지 입니다.</h1>
  <hr>
  <h3>제목 : {{data}}</h3>
</body>
</html>
```





## dtl 만들어보기

1. urls.py

```python
path('dtl/', views.dtl),
```



2. views.py

```python
def dtl(request):
    hws = ['homework', 'workshop', 'practice']
    context = {
        'hws' = hws
    }
    return render(request, 'dtl.html', context)
```



3. dtl.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <h1>Django Template Language</h1>
  <hr>
  <h3>For</h3>
  <ul>
    {% for item in hws%}
    <li>{{item}}</li>
    {% endfor %}
  </ul>
</body>
</html>
```

> views.py에서 hws 리스트를 만들어 줬기 때문에, ul 태그를 이용한다.!!!

endfor : dtl은 python 코드로 작동하는게 아니라 identation으로 구분되지 않기 때문에, 처음과 끝을 구분해야한다.







## Django Template Language(DTL)

> 프로그래밍 logic이 아닌 프레젠테이션을 표현하기 위한 것이다.

python 처럼 `if`, `for` 를 사용할 수 있지만, 단순히 **python code로 실행되는 것이 아니다.**



### syntax

1 ) variable : `{{ }}`

2 ) filter : `{{ variable|filter }}`

3 ) tags :  `{% tag %}`







