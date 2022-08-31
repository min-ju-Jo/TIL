## 0830_django

mkdir django-intro

cd django-intro/

###### 가상환경

python -m venv venv

source venv/Scripts/activate

ctrl+shipt+p -> python:select interpreter -> 추천

###### Django 설치

pip install django==3.2.13

###### 패키지 목록 생성

pip freeze > requirements.txt

pip install -r requirements.txt

###### 프로젝트 생성

django-admin startproject {프로젝트 이름(firstpjt)} . (뒤에 . 쩜)

```
프로젝트 구조
firstpjt
-__init__.py
-asgi.py
-settings.py     # Django 프로젝트 설정을 관리.
-urls.py         # 사이트의 url과 적절한 views의 연결을 지정.
-wsgi.py
-manange.py
```

###### 서버 실행

python manage.py runserver

확인 -> ctrl+클릭 -> 메인페이지 확인(로켓)

###### Django Ap

###### plication 어플리케이션 생성

python manage.py startapp {나의 어플리케이션(articles)}

어플리케이션 이름은 복수형으로 작성 권장

```
어플리케이션 구조
articles
>migrations
-__init__.py
-admin.py
-apps.py
-models.py
-test.py
-views.py        # view 함수들이 정의 되는 곳. MTV패턴의 V에 해당.
```

###### 어플리케이션 등록 (주의1.반드시 생성 후 등록 2.순서(Local apps, Third party apps, Django apps)

프로젝트에서 앱을 사용하기 위해서는 반드시 INSTALLED_APPS 리스트에 반드시 추가해야함.

firstpjt -> settings.py -> 

```python
INSTALLED_APPS = [
'나의 어플리케이션(articles)',
# Django installation에 활성화 된 모든 앱을 지정하는 문자열 목록.
]
```

###### Project & Application

Project

- collection of apps

- 프로젝트는 앱의 집합

- 프로젝트에는 여러 앱이 포함될 수 있음

- 앱은 여러 프로젝트에 있을 수 있음

Application

- 앱은 실제 요청을 처리하고 페이지를 보여주는 등의 역할을 담당

- 일반적으로 앱은 하나의 역할 및 기능 단위로 작성하는 것을 권장함

#### 

#### 요청과 응답

- URL - VIEW - TEMPLATE 순의 작성 순서로 코드 작성, 데이터의 흐름 이해하기.

###### 데이터의 흐름 순서

```
URL         path('index/', views.index)
View        def index(request):
                return render(request, 'index.html')
Template    articles/templates/index.html
```

###### URLs

firstpjt -> url.py -> 

```python
# 가져올거
from {나의 어플리케이션} import views

urlpatterns = [
    path('admin/', admin.site.urls),
    # view 함수 실행시킬거  
    path('index/', views.index),      
```

###### View

articles -> views.py ->

```python
def index(request):    # HTTP 요청을 수신하고 HTTP 응답을 반환하는 함수 작성.
    return render(request, 'index.html') # Template에게 HTTP응답 서식맡김.
```

- render(request, template_name, context)

- 주어진 템플릿을 주어진 컨텍스트 데이터와 결합하고 렌더링 된 텍스트와 함께 응답객체를 반환하는 함수.

- 1.request : 응답을 생성하는 데 사용되는 요청 객체

- 2.template_name : 템플릿의 전체이름 또는 템플릿 이름의 경로

- 3.context : 템플릿에서 사용할 데이터(딕셔너리 타입으로 작성)

###### Templates

articles 안에 templates폴더 생성(폴더이름 반드시 templates라고 지정해야 함.) -> index.html파일 생성 -> ! 탭 

```python
<body>            # 실제 내용을 보여주는데 사용되는 파일.
    <hl>장고</hl> 
</body>
```

터미널 -> python manage.py runserver -> ctrl+클릭 -> /index/ 내가 입력한 장고 

#### 

#### Django Template

###### Django Template

- 데이터 표현을 제어하는 도구이자 표현에 관련된 로직

- Django Template 을 이용한 HTML 정적 부분과 동적 컨텐츠 삽입

###### Django Template System

- 데이터 표현을 제어하는 도구이자 표현에 관련된 로직 담당

###### Django Template Language(DTL)

- Django template에서 사용하는 built-in template system

- pythin 코드로 실행되는 것이 아님

- 프로그래밍적 로직이 아니라 프레젠테이션을 표현하기 위한 것임

###### DTL Syntax

- Variable

- Filters

- Tags

- Comments

#### Template inheritance

템플릿 상속

templates폴더 -> base.html ->

```python
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=0, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <p>네비게이션 바</p>
  <a href="/index/">처음으로<a/>
  {% block content %}

  {% endblock content%}
  <p>푸타</p>
</body>
</html>
```

index 템플릿에서 base 템플릿을 상속받음

index.html ->

```python
{% extends 'base.html' %}

{% block content %}
  <hl>장고</hl>
  <a href="/dtl/">dtl로 이동</a>
{% endblock content %}
```

추가 템플릿 경로 추가하기

firstpjt -> settings.py -> 'DIRS': [BASE_DIR / 'templates',], 코드 작성

```python
EMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates',],
        'APP_DIRS': True,
        'OPTIONS': {
```

#### Sending and Retrieving form data

#### Sending form data (Client)

###### form, input

firstpjt -> urls.py -> path('throw/', views.throw), 

articles -> views.py -> 

```python
def throw(request):
    return render(request, 'throw.html')
```

templates -> throw.html 파일생성-> 

```python
{% extends 'base.html' %}

{% block content %}
  <form action="" method="">
    <label for="search">search:</label>            # for="search"
    <input type="text" name="search" id="search">  # id="search"->serch:를 누르면 
    <input type="submit">
  </form>

  <form action="https://search.naver.com/search.naver">
    <input type="text" name="query">
    <input type="submit">
  </form>
  {% endblock  %}
```

###### GET, catch

throw.html ->

```python
{% extends 'base.html' %}

{% block content %}
  <form action="/catch/" method="GET">
    <label for="search">search:</label>
    <input type="text" name="search" id="search">
    <input type="submit">
  </form>

{% endblock content %}
```

views.py ->

```python
def catch(request):
#    print(request.GET.get('search')) # 모든 요청데이터는 view함수의 첫번째 인자
    value = request.GET.get('search') # request에 들어있다.
    context = {
        'value' : value,
    }
#    return render(request, 'catch.html')
    return render(request, 'catch.html', context)
```

templates -> catch.html ->

```python
{% extends 'base.html' %}

{% block content %}
  <p>{{ value }}를 받았어!</p>
  <p> 고맙다 {{ name }}민수야</p>
{% endblock  %}
```

->결과 확인 python manage.py runserver -> /throw/ -> search: 100만원입력->제출

```
네비게이션 바

처음으로
100만원를 받았어!

고맙다 민수야

푸타
```

#### Django URLs

#### Trailing URL Slashes

#### Variable routing

###### Variable routing 작성

- 변수는 <>에 정의하며 view 함수의 인자로 할당됨.

- 기본타입 : str, int

firstpjt -> urls.py ->  path('hello/<str:name>/', views.hello),

views.py ->

```python
def hello(request, name): # variable routing으로 할당된 변수 인자로 받고
    context = {           # 템플릿 변수로 사용할 수 있다.
        'name' : name,
    }
    return render(request, 'hello.html', context)
```

hello.html 생성 ->

```python
{% extends 'base.html' %}

{% block content %}
  <hl>만나서 반가워요{{ name }}님!</hl>
{% endblock  %}
```

->결과 확인 python manage.py runserver -> /hello/<주우재>/

```
네비게이션 바

처음으로 만나서 반가워요<주우재>님!
푸타
```

#### App URL mapping

앱이 많아졌을 때  urls.py 를 각 app에 매핑하는 방법

- 두번째 app인 pages를 생성 -> python manage.py startapp pages

- 등록 firstpjt -> settings.py -> 

하나의 프로젝트의 여러 앱이 존재한다면, 각각의 앱 안에 urls.py을 만들고 프로젝트 urls.py에서 각 앱의 urls.py파일로 URL 매핑 위탁할 수 있음

- 각각의 app폴더 안에 urls.py를 작성하고 아래와 같이 수정 진행

- articles -> urls.py 생성, pages -> urls.py 생성

articles -> urls.py ->

```python
from django.urls import path
from . import views

urlpatterns = [
    path('index/', views.index),
    path('dtl/', views.dtl),
    path('greeting/', views.greeting),
    path('throw/', views.throw),
    path('catch/', views.catch),
    path('hello/<str:name>/', views.hello),
]
```

pages -> urls.py

```python
from django.urls import path

urlpatterns = [

]
```

###### Including other URLconfs

- urlpattern은 언제든지 다른 URLconf 모듈을 포함(include)할 수 있음

- include되는 앱의 url.py에 urlpatterns가 작성되어 있지 않다면 에러 발생

- pages 앱의 urlpatterns가 빈 리스트라도 작성되어 있어야 함

fistpjt -> urls.py ->

```python
from django.contrib import admin
from django.urls import path, include  # include 

urlpatterns = [
    path('admin/', admin.site.urls),
    path('articles/', include('articles.urls')),
    path('pages/', include('pages.urls')),
]
```

- 이제 메인페이지의 주소 아래와 같이 바뀜

- /index/  ->  /articles/index/ 후자로 해야 열린다.

###### include()

- 다른 URLconf(app1/urls.py)들을 참조할 수 있도록 돕는 함수

- 함수 include()를 만나게 되면 URL의 그 시점까지 일치하는 부분을 잘라내고, 남은 문자열 부분을 후속 처리를 위해 include된 URLconf로 전달

###### URL 구조의 변화

- 앱의 URL을 project의 urls.py에서 관리

- 복수 개의 앱의 URL을 project의 urls.py에서 관리

- 각각의 앱에서 URL을 관리

#### Naming URL patterns

###### Naming URL patterns의 필요성

- index/ 의 문자여 주소 -> new-index/로 바꿔야 한다 가정

- index/ 주소를 사용했던 모든 곳 찾아서 변경해야 하는 번거로움 발생

###### URL태그 사용 Naming URL patterns

- 링크에 URL을 직접 작성하는 것이 아니라 path()함수의 name인자를 정의해서 사용

- DTL의 Tag 중 하나인 URL태그를 사용해서 path()함수에 작성한 name을 사용할 수 있음

- Django는 URL에 이름을 지정하는 방법을 제공함으로써 view 함수와 템플릿에서 특정 주소를 쉽게 참조할 수 있도록 도움

articles -> urls.py

```python
urlpatterns = [
    path('index/', views.index, name = 'index'),
    path('dtl/', views.dtl, name = 'dtl'),
    path('greeting/', views.greeting),
    path('throw/', views.throw, name = 'throw'),
    path('catch/', views.catch),
    path('hello/<str:name>/', views.hello),
]
```

###### Built-in tag -"url"

{% url ' ' %}

- 주어진 URL 패턴 이름 및 선택적 매개 변수와 일치하는 절대 경로 주소를 반환

- 템플릿에 URL을 하드 코딩하지 않고도 DRY(Don't Repeat Yourself) 원칙 위반하지 않으면서 링크 출력하는 방법
