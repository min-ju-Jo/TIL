## 0831_django

###### 가상환경

python -m venv venv

source venv/Scripts/activate

ctrl+shipt+p -> python:select interpreter -> 추천

pip list -> 확인

###### Django 설치

pip install django==3.2.13

###### 패키지 목록 생성

pip freeze > requirements.txt

###### 프로젝트 생성

django-admin startproject {프로젝트 이름} . (뒤에 . 쩜)

-> django-admin startproject crud .

###### 어플리케이션 생성

python manage.py startapp {나의 어플리케이션}

-> python manage.py startapp articles

#### Django Model

###### Model

- Django는 Model을 통해 데이터에 접속하고 관리

- 단일한 데이터에 대한 정보를 가짐

- 사용자가 저장하는 데이터들의 필수적인 필드들과 동작들을 포함

- 저장된 데이터베이스의 구조

- 일반적으로 각각의 모델은 하나의 데이터베이스를 테이블에 매핑
  
  - 모델클래스 1개 == 데이터베이스 테이블 1개

###### Model을 통해 데이터 관리

![]($(filename)_assets/2022-08-31-11-34-04-image.png)

###### Model 작성하기

새 프로젝트(crud), 앱(articles) 작성 및 등록

![]($(filename)_assets/2022-08-31-11-35-29-image.png)

models.py 작성

- 모델클래스를 작성하는 것은 데이터베이스 테이블의 스키마를 정의하는 것

- 모델 크래스 == 테이블 스키마

<img title="" src="$(filename)_assets/2022-08-31-11-37-17-image.png" alt="" width="467">

- id컬럼은 테이블 생성시 Django가 자동으로 생성

- 각 모델은 django.models.Model 클래스의 서브 클래스로 표현됨
  
  - 즉, 각 모델은 django.db.modles 모듈의 Model 클래스를 상속받아 구성됨
  
  - 클래스 상속 기반 형태의 Django 프레임워크 개발

- models 모듈을 통해 어떠한 타입의 DB 필드(컬럼)을 정의할 것인지 정의
  
  - 클래스 변수 title과 content은 DB필드를 나타냄

- title, content : 클래스 변수(속성)명 
  
  - DB 필드의 이름

- 클래스 변수 값(models 모듈의 Field 클래스)
  
  - DB 필드의 데이터 타입

사용한 모델 필드

- CharField(max_lengt=None, **options)
  
  - 길이의 제한이 있는 문자열을 넣을 때 사용
  
  - max_length : 필드의 최대길이(문자), CharField의 필수 인자, 데이터베이스와 Django의 유효성 검사(값을 검증하는 것)에서 활용됨

- TextField(**options)
  
  - 글자의 수가 많을 때 사용
  
  - max_length 옵션 작성 시 사용자 입력 단계에서는 반영 되지만, 모델과 데이터베이스 단계에서는 적용되지 않음 (CharField를 사용해야 함)
  
  - 실제로 저장될 때 길이에 대한 유효성을 검증하지 않음

데이터베이스 스키마

- 지금까지 작성한 models.py는 다음과 같은 데이터베이스 스키마를 설계한 것

- 이제 데이터베이스에 테이블을 생성하기 위한 설계도 작성이 필요함

#### Migrations

- 모델에 대한 청사진을 만들고 이를 통해 테이블을 생성하는 일련의 과정

- Django가 모델에 생긴 변화(필드 추가, 모델 삭제 등)를 DB에 반영하는 방법

###### 주요 명령어

- makemigrations

- migrate

###### makemigrations - > python manage.py makemigrations

- 테이블을 만들기 위한 설계도를 생성하는 것

- python manage.py makemigrations

- 명령어 실행 후 migrations/0001_initial.py가 생성된 것을 확인

<img src="$(filename)_assets/2022-08-31-12-41-46-image.png" title="" alt="" width="454">

###### migrate - > python manage.py migrate

- makemigrations로 만든 설계도를 실제 db.sqlite3 DB 파일에 반영하는 과정

- 결과적으로 모델에서의 변경사항들과 DB의 스키마가 동기화를 이룸

- 모델과 DB의 동기화

- python manage.py migrate

- 설게도(migration)를 실제 db.sqlite3 DB 파일에 반영

<img src="$(filename)_assets/2022-08-31-12-44-11-image.png" title="" alt="" width="606">

- 확인 : SQLite EXTENSIONS 설치 후 db.sqlite3 우클릭 Open Database -> 좌측 아래 SQLITE EXPLORER -> 내가 만든 거: articles_article ( 앱_클래스_)

#### ORM

- makemigrations로 인해 만들어진 설계도는 파이썬으로 작성되어있음 -> 그런데 SQL만 알아 들을 수 있다는 DB가 어떻게 이 설계도를 이해하고 동기화를 이룰 수 있을까? -> 바로 이 과정에서 중간에 해석을 담당하는 것이 ORM

- Object-Relational-Mapping

- 객체 지향 프로그래밍 언어를 사용하여 Django <-> SQL 데이터를 변환하는 프로그래밍기술

- Django는 내장 Django ORM을 사용

###### ORM 사용하는 이유

- 생산성 -> DB를 객체로 조작하기 위해 ORM을 사용할 것

#### 추가 필드 정의

###### Model 변경사항 반영하기

- models.py에 변경사항이 생겼을 때 어떤 과정의 migration이 필요할까?

- 추가 모델 필드 작성 후 다시 한번 makemigrations 진행 
  
  -> python manage.py makemigrations

<img src="$(filename)_assets/2022-08-31-12-59-31-image.png" title="" alt="" width="600">

- 기존에 id, title, content 컬럼을 가진 테이블에 2개의 컬럼이 추가되는 상황

- Django 입장에서는 이미 존재하는 테이블에 새로운 컬럼이 추가되는 요구 사항을 받았는데, 이 컬럼들은 기본적으로 빈 값으로 추가될 수 없음 -> 그래서 Django는 우리에게 추가된는 컬럼에 대한 기본 값을 설정해야 하니 어떻게 어떤 값을 설정할 것인지를 물어보는 과정을 진행

![]($(filename)_assets/2022-08-31-13-03-16-image.png)

- 각 보기 번호의 의미
  
  1. 다음 화면으로 넘어가서 새 컬럼의 기본 값을 직접 입력하는 방법
  
  2. 현재 과정에서 나가고 모델 필드에 default 속성을 직접 작성하는 방법

- "1"을 입력후 Enter (created_at 필드에 대한 default 값 설정)

![]($(filename)_assets/2022-08-31-13-04-57-image.png)

- 다음 화면에서 아무것도 입력하지 않고 Enter를 입력하면 Django에서 기본적으로 파이썬의 timezone모듈의 now 메서드 변환 값을 기본 값으로 사용하도록 해줌

![]($(filename)_assets/2022-08-31-13-06-25-image.png)

- 새로운 설계도(migrations/0002_auto_20220831_1546.py)가 만들어진 것을 확인
- 1번 설계도에 의존 (1번에 추가된 것이므로)

<img src="$(filename)_assets/2022-08-31-15-51-30-image.png" title="" alt="" width="630">

- 새로운 설계도를 생성했기 때문에 DB와 동기화를 진행해야 함(아직 DB에는 변경사항이 반영되지 않았기 때문) -> python manage.py migrate
- db확인 -> 스키마 확인 -> 컬럼 추가되었다.

<img title="" src="$(filename)_assets/2022-08-31-15-57-07-image.png" alt="" width="620">

###### 반드시 기억해야 할 migration 3단계

1. models.py에서 변경사항이 발생하면

2. migrations 파일 생성 (설계도 생성) : makemigrations

3. DB반영 (모델과 DB의 동기화) : migrate

###### DateTimeField()

- Python의 datetime.datetime 인스턴스로 표시되는 날짜 및 시간을 값으로 사용하는 필드

- DataField를 상속받는 클래스

- 선택인자
  
  1. auto_now_add : 최초 생성 일자, 데이터가 실제로 만들어질 때 자동으로 초기화됨
  
  2. auto_now : 최종 수정 일자, 데이터가 수정될 때마다 자동으로 갱신됨

###### Model 정리

- 웹 애플리케이션의 데이터를 구조화하고 조작하기 위한 도구

#### QuerySet API

###### 사전준비

외부 라이브러리 설치 및 설정

pip install ipython

pip install django-extensions -> 설치할 땐 하이픈, 등록할 땐 언더바 주의하자

![]($(filename)_assets/2022-08-31-13-17-55-image.png)

패키지 목록 업데이트

pip freeze > requirements.txt

<img src="$(filename)_assets/2022-08-31-13-18-35-image.png" title="" alt="" width="481">

Django shell 실행 -> django-extension이 제공하는 더 강력한 shell_plus로 진행

python manage.py shell_plus

첫 ORM명령어 사용

Article.objects.all()

![]($(filename)_assets/2022-08-31-19-15-34-image.png)

###### QuerySet API

- "QuerySet과 상호작용하기 위해 사용하는 도구 (메서드, 연산자 등)"

<img src="$(filename)_assets/2022-08-31-19-18-03-image.png" title="" alt="" width="549">

###### Database API 구문

<img src="$(filename)_assets/2022-08-31-19-15-56-image.png" title="" alt="" width="385">

- "objects" manager 
  
  - Django 모델이 데이터베이스 쿼리 작업을 가능하게 하는 인터페이스
  
  - Django는 기본적으로 모든 Django 모델 클래스에 대해 objects라는 Manager 객체를 자동으로 추가함
  
  - 이 Manager(objects)를 통해 특정 데이터를 조작(메서드)할 수 있음
  
  - DB를 Python class로 조작할 수 있도록 여러 메서드를 제공하는 manager

- Query
  
  - 데이터베이스에 특정한 데이터를 보여 달라는 요청
  
  - 이때, 파이썬으로 작성한 코드가 ORM의 의해 SQL로 변환되어 데이터베이스에 전달되며, 데이터베이스의 응답 데이터를 ORM이 QuerySet이라는 자료 형태로 변환하여 우리에게 전달

- QuerySet
  
  - 데이터베이스에게 전달 받은 객체 목록(데이터 모음)
  
  - Django ORM을 통해 만들어진 자료형이며, 필터를 걸거나 정렬 등을 수행할 수 있음
  
  - "object"manager를 사용하여 복수의 데이터를 가져오는 queryset method를 사용할 때 반환되는 객체
  
  - 단, 데이터베이스가 단일한 객체를 반환 할 때는 QuerySet이 아닌 모델(Class)의 인스턴스로 반환됨

#### CRUD

- Create / Read / Update / Delete : 생성 / 조회 / 수정 / 삭제

###### Queryset API를 활용해 데이터를 생성하고, 읽고, 수정하고 삭제해보기

###### CREATE

1 첫번째 방법

- article = Article() : 클래스를 통한 인스턴스 생성

- article.title = 'first' : 클래스 변수명과 같은 이름의 인스턴스 변수를 생성 후 값 할당

- article.content = 'django!'

- article.save() : 인스턴스로 save메서드 호출 -> DB에 데이터가 저장된다

<img title="" src="$(filename)_assets/2022-08-31-19-57-59-image.png" alt="" width="764">

<img src="$(filename)_assets/2022-08-31-19-37-31-image.png" title="" alt="" width="571"> 

<img src="$(filename)_assets/2022-08-31-16-26-10-image.png" title="" alt="" width="598">

2 두번째 방법

- 인스턴스 생성 시 초기 값을 함께 작성하여 생성

- article = Article(title='second', content='django!' )

- article.save()

![]($(filename)_assets/2022-08-31-19-39-30-image.png)

<img src="$(filename)_assets/2022-08-31-16-26-25-image.png" title="" alt="" width="595">

3 세번째 방법

- QuerySet API 중 create() 메서드 활용

- Article.objects.create(title='third', content='django!')

- save하지 않아도 return -> create()메서드가 save까지  

![]($(filename)_assets/2022-08-31-19-40-18-image.png)

<img src="$(filename)_assets/2022-08-31-16-28-56-image.png" title="" alt="" width="585">

###### 메서드 .save()

- Saving object

- 객체를 데이터베이스에 저장함

- 데이터 생성 시 save를 호출하기 전에는 객체의 id값은 None
  
  - id 값은 Django가 아니라 데이터베이스에서 계산되기 때문

- 단순히 모델 클래스를 통해 인스턴스를 생성하는 것은 DB에 영향을 미치지 않기 때문에 반드시 save를 호출해야 테이블에 레코드가 생성됨

###### READ

- QuerySet API method는 크게 2가지로 구분됨
  
  - Methods that "return new querysets"
  
  - Methods that "do not return querysets"

- all()
  
  - QuerySet return
  
  - 전체 데이터 조회

![]($(filename)_assets/2022-08-31-19-53-11-image.png)

- get()
  
  - 단일 데이터 조회
  
  - 객체를 찾을 수 없으면 DoesNotExist 예외를 발생시키고, 둘 이상의 객체를 찾으면 MultipleObjectsReturned 예외를 발생시킴
  
  - 위와 같은 특징을 가지고 있기 때문에 primary key와 같이 고유성(uniqueness)을 보장하는 조회에서 사용해야 함

![]($(filename)_assets/2022-08-31-19-55-02-image.png)

- filter()
  
  - 지정된 조회 매개 변수와 일치하는 객체를 포함하는 새 QuerySet을 반환
  
  - 없어도 빈 QuerySet으로 하나여도 QuerySet으로 반환
  
  - pk값을 조회할 때 적합 한 Queryset API 가 아니다. pk값 조회할 때는 get으로 ( 1. QuerySet으로 반환하기 때문, 2. 없으면 오류가 나와야 하지만 없어도 빈 QueySet을 반환되기 때문)

![]($(filename)_assets/2022-08-31-19-55-47-image.png)

- Field lookups
  
  - 특정 레코드에 대한 조건을 설정하는 방법
  
  - 수많은 것 중 하나 예로 보면 __contains

![]($(filename)_assets/2022-08-31-20-08-36-image.png)

###### UPDATE

- 수정하고자 하는 article 인스턴스 객체를 조회 후 반환 값을 저장

- article 인스턴스 객체의 인스턴스 변수 값을 새로운 값으로 할당 

- save() 인스턴스 메서드 호출 

![]($(filename)_assets/2022-08-31-20-10-45-image.png)

- 두가지 (title값과 updated_at) 바뀐다.

<img src="$(filename)_assets/2022-08-31-20-15-37-image.png" title="" alt="" width="592">

###### DELETE

- 삭제하고자 하는 article 인스턴스 객체를 조회 후 반환 값을 저장

- delete() 인스턴스 메서드 호출

![]($(filename)_assets/2022-08-31-20-11-58-image.png)

<img title="" src="$(filename)_assets/2022-08-31-20-19-01-image.png" alt="" width="584">

- 1번이 지워진 상태에서 다음을 넣으면? -> 4번이 생성된다
  
  - Django에서는 삭제 -> 불필요 -> 재사용하지 않는다

#### CRUD with view functions

###### QuerySet API 를 통해 view 함수에서 직접 CRUD 구현하기

###### 사전준비

base 템플릿 작성 : bootstrap CDN 및 템플릿 추가 경로 작성

![]($(filename)_assets/2022-08-31-20-23-12-image.png)

![]($(filename)_assets/2022-08-31-20-23-19-image.png)

url 분리 및 연결

![]($(filename)_assets/2022-08-31-20-23-48-image.png)

index 페이지 작성

![]($(filename)_assets/2022-08-31-20-25-40-image.png)

###### READ 1 (index page)

###### 전체 게시글 조회

- index 페이지에서는 전체 게시글을 조회해서 출력한다

![]($(filename)_assets/2022-08-31-20-29-34-image.png)

-> python manage.py runserver

<img src="$(filename)_assets/2022-08-31-21-21-17-image.png" title="" alt="" width="581">

-> DB로 부터 조회를 해서 가져온 것

###### CREATE

CREATE 로직을 구현하기 위해서는 몇 개의 view 함수가 필요할까?

- 사용자의 입력을 받을 페이지를 렌더링 하는 함수 1개
  
  - "new" view function

- 사용자가 입력한 데이터를 전송 받아 DB에 저장하는 함수 1개
  
  - "create" view function

New(첫 번째 함수)

<img src="$(filename)_assets/2022-08-31-21-40-58-image.png" title="" alt="" width="411">

기본틀

![]($(filename)_assets/2022-08-31-21-40-07-image.png)

<img src="$(filename)_assets/2022-08-31-21-41-29-image.png" title="" alt="" width="476">

--> 사용자가 입력한 값에 키 값이 필요 -> input -> name이 키의 역할

-->Title클릭시 창으로 연결 -> input -> id

![]($(filename)_assets/2022-08-31-21-49-06-image.png)

<img src="$(filename)_assets/2022-08-31-21-49-27-image.png" title="" alt="" width="290">

--> 제출을 누르면

![]($(filename)_assets/2022-08-31-21-50-28-image.png)

/articles/new/?title=제목&content=내용#

--> 뒤로가기 만들기 -> 메인페이지로 갈 수 있도록(index.html)

--> 메인페이지에서 NEW페이지로 갈 수 있도록

![]($(filename)_assets/2022-08-31-21-55-35-image.png)

![]($(filename)_assets/2022-08-31-21-56-29-image.png)

Create(두번째 함수)

<img src="$(filename)_assets/2022-09-01-00-20-34-image.png" title="" alt="" width="455">

<img title="" src="$(filename)_assets/2022-09-01-00-16-42-image.png" alt="" width="491">

-> 데이터 생성하는 방법 3가지

- 2번째 생성 방식을 사용하는 이유
  
  - create 메서드가 더 간단해 보이지만 추후 데이터가 저장되기 전에 유효성 검사 과정을 거치게 될예정
  
  - 유효성 검사가 진행된 후에 save메서드가 호출되는 구조를 택하기 위함

<img title="" src="$(filename)_assets/2022-09-01-00-21-12-image.png" alt="" width="514">

-> 확인 -> 제목!!, 내용!! 입력하고 제출을 눌러본다

![]($(filename)_assets/2022-09-01-00-24-56-image.png)

-> 제출을 눌렀는데 바뀌지 않음 -> 제출을 누를 때 어디로 보낼지 아직 작성하지 않았기때문

-> action에 제출을 누르고 보내질 create 작성해준다

![]($(filename)_assets/2022-09-01-00-33-43-image.png)

-> 테이블 확인 , 또는 메인페이지 /articles/ 에서도 확인 가능

<img src="$(filename)_assets/2022-09-01-00-37-09-image.png" title="" alt="" width="514">

###### 2가지 문제점 바생

1. create템플릿을 만들긴 했지만 의미가 없다 -> create를 렌더링하는 것

2. GET방식 -> 데이터 노출 -> GET은 조회할 때만 사용하여야 하지만 이거 써줘라고 하는 것 -> GET의 방식이 목적에 맞지 않다 -> POST->조작






