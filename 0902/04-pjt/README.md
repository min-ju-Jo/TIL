## 04_pjt

#### 프레임워크 기반 웹 페이지 구현

###### 목표

- 데이터를 생성, 조회, 수정, 삭제할 수 있는 Web application 제작

- Django web framework를 사용한 데이터 처리

- Django Model과 ORM에 대한 이해

- 관리자 페이지를 통한 데이터 관리

###### 개발도구

- Visual2Studio Code

- Google Chrome

- Django 3.2+

###### 나의 웹 페이지

- Django 프로젝트 mypjt, 앱 movies

- Model 클래스 Movie
  
  - title(영화제목), audience(관객 수), release_date(개봉일), genre(장르), score(평점), poster_url(포스터 경로), description(줄거리)

- URL
  
  - /movies/ : 전체 영화 목록 페이지 조회
  
  - /movies/new/ : 새로운 영화 생성 페이지 조회
  
  - /movies/create/ : 단일 영화 데이터 저장
  
  - /movies/<pk>/ : 단일 영화 상세 페이지 조회
  
  - /movies/<pk>/edit/ : 기존 영화 수정 페이지 조회
  
  - /movies/<pk>/update/ : 단일 영화 데이터 수정
  
  - /movies/<pk>/delete/ : 단일 영화 데이터 삭제 

- View
  
  - index : 전체 영화 데이터 조회 및 index.html 렌더링
  
  - new : 장르 데이터 제공 및 new.html 렌더링
  
  - create : 새로운 영화 데이터 저장 및 detail 페이지로 리다이렉트
  
  - detail : 단일 영화 데이터 조회 및 detail.html 렌더링
  
  - edit : 수정 대상 영화 데이터 조회 및 edit.html 렌더링
  
  - update : 영화 데이터 수정 및 detail 페이지로 리다이렉트
  
  - delete : 단일 영화 데이터 삭제 및 index 페이지로 리다이렉트

- Template
  
  - base.html, index.html, detail.html, new.html, edit.html

###### 사전준비

- 가상환경
  
  - python -m venv venv
  
  - source venv/Scripts/activate

- Django 설치
  
  - pip install django==3.2.13

- 패키지 목록 생성
  
  - pip freeze > requirements.txt

- 프로젝트, 앱 생성 및 등록
  
  - django-admin startproject mypjt .
  
  - python manage.py startapp movies

###### Model

```python
# movies/models.py
from django.db import models

class Movie(models.Model):
    title = models.CharField(max_length=20)
    audience = models.IntegerField()
    release_date = models.DateField()
    genre = models.CharField(max_length=30)
    score = models.FloatField()
    poster_url = models.TextField()
    description = models.TextField()
```

- makemigrations 
  
  - python manage.py makemigrations
  
  - 테이블을 만들기 위한 설계도를 생성하는 것

- migrate 
  
  - python manage.py migrate
  
  - makemigrations로 만든 설계도를 실제 db.sqlite3 DB 파일에 반영하는 과정
  
  - 결과적으로 모델에서의 변경사항들과 DB의 스키마가 동기화를 이룸
  
  - 모델과 DB의 동기화

###### base.html 공통 부모 템플릿

- templates/base.html -> 모든 템플릿 파일은 base.html을 상속받아 사용

###### URL 분리 및 연결

- 앱의 url : movies/urls.py -> 앱네임 movies 지정
  
  ```python
  # movies/urls.py
  
  from django.urls import path
  from . import views
  
  app_name = 'movies'
  urlpatterns = [
      # path..
  ]
  ```

- 프로젝트의 url : mypjt/urls.py -> include import해서 movies의 urls 넘김
  
  ```python
  # mypjt/urls.py
  
  from django.contrib import admin
  from django.urls import path, include
  
  urlpatterns = [
   path('admin/', admin.site.urls),
   path('movies/', include('movies.urls')),
   ]
  ```

###### Admin site

- python manage.py createsuperuser

- 모델의 record 보기 위해 admin.py에 등록
  
  ```python
  # movies/admin.py
  from django.contrib import admin
  from .models import Movie
  
  admin.site.register(Movie)
  ```

- admin.py의 list_display
  
  ```python
  # movies/admin.py
  class MovieAdmin(admin.ModelAdmin):
      list_display = ('title', 'audience', 'release_date', 'genre', 'score', 'poster_url', 'description')
  admin.site.register(Movie, MovieAdmin)
  ```

###### 새롭게 알게 된 점

- 평점 : score -> 입력 받을 때
  
  - type="number" -> 숫자만 입력이 가능하게 할 수 있다
  
  - -> 소수점 뒤 한자리까지 입력 가능하게 하기 위해서
  
  - -> type="number" step="0.1"

- 관객 수 : audience = models.IntegerField() -> 입력 받을 때
  
  - type="number"
  
  - -> 숫자만 입력이 가능하게 할 수 있다, 텍스트 입력시 오류나게 만들 수 있다

###### 어려웠던 점

- 영화 상세정보 페이지(detail.html)에 이미지 불러오고 싶을 때 
  
  - img 태그에 src="{{ movie.poster_url}}" alt="img"

- 영화 수정 페이지(edit.html)에서 HTML input요소에 기존 데이터를 출력해야 할 때
  
  - release_date input태그에 value="{{movie.release_date|date:'Y-m-d'}}">
  
  - genre option태그에  value="{{ movie.genre }}" selected>{{ movie.genre }}
  
  - 위와 같이 하면 선택된 장르가 옵션에 두개가 생긴다
  
  - -> selected 뒤에 hidden을 붙여주어 해결한다
