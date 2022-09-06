## 0906_django

### 04_django

#### Django Form

###### 개요

- 지금까지 HTML form, input 태그를 통해서 사용자로부터 데이터를 받았다

- 현재 우리 Django 서버는 들어오는 요청 모두 수용하고 있는데, 이러한 요청 중에 비정상적인 혹은 악의적인 요청이 있다는 것을 생각해야한다

- 사용자가 입력한 데이터가 우리가 원하는 데이터 형식에 맞는지에 대한 유효성 검증이 반드시 필요

- Django Form은 이 과정에서 과중한 작업과 반복 코드를 줄여줌으로써 훨씬 쉽게 유효성 검증을 진행할 수 있도록 만들어 준다

###### Form에 대한 Django의 역할

- Form은 Django의 유효성 검사 도구 중 하나로 외부의 악의적 공격 및 데이터 손상에 대한 중요한 방어 수단

- Django는 Form과 관련한 유효성 검사를 단순화하고 자동화 할 수 있는 기능을 제공하여, 개발자가 직접 작성하는 코드보다 더 안전하고 빠르게 수행하는 코드를 작성할 수 있다 -> 개발자가 필요한 핵심 부분만 집중할 수 있도록 돕는 프레임워크의 특성

###### Django는 Form에 관련된 작업의 세 부분을 처리

1. 렌더링을 위한 데이터 준비 및 재구성

2. 데이터에 대한 HTML forms 생성

3. 클라이언트로부터 받은 데이터 수신 및 처리

###### The Django Form Class

###### Form Class

- Django form 관리 시스템의 핵심

###### Form Class 선언

- Form Class 선언하는 것은 Model Class를 선언하는 것과 비슷

- Model과 마찬가지로 상속을 통해 선언(forms라이브러리의 Form 클래스를 상속받음)

- 앱 폴더에 forms.py 생성 후 ArticleForm Class 선언

```python
# articles/forms.py -> form class 선언
from django import forms

class ArticleForm(forms.Form):
    title = forms.CharField(max_length=10)
    content = forms.CharField()
```

- form에는 model field와 달리 TextField가 존재하지 않음

- 모델의 TextField처럼 사용하려면 어떻게 작성 할 수 있을까

###### new view 함수 업데이트

```python
# articles/view.py -> new함수
from .forms import ArticleForm

def new(request):
    form = ArticleForm()
    context = {
        'form' : form,
    }
    return render(request, 'articles/new.html', context)
```

###### new 템플릿 업데이트

```python
# articles/new.html
{% extends 'base.html' %}

{% block content %}
  <h1>NEW</h1>
  <form action="{% url 'articles:create' %}" method="POST">
    {% csrf_token %}
    {{ forms.as_p}}
    <input type="submit">
  </form>
  <hr>
  <a href="{% url 'articles:index' %}">뒤로가기</a>
{% endblock content %}
```

`->articles/new페이지`

-> 아래 네 줄 대신 {{ form }}

->lable, input, label, textarea 태그

-> 위 네줄이 필요없어진다.

-> 두가지 바꾸고싶다

-> title과 content 띄워쓰기-> 줄바꿈 -> as_p메소드, content textarea

-> {{ form as_p }}

-> 표현을 바꾸는 것 -> Widgets

-> articles/forms.py -> Testarea위젯

```python
# articles/forms.py -> Testarea위젯

class ArticleForm(forms.Form):
    title = forms.CharField(max_length=10)
    content = forms.CharField(widget=forms.Textarea)
```

-> content = forms.CharField(widget=forms.Textarea)

지금까지는 new페이지에 한줄한줄 이제 하나의 인스턴스로 출력 -> form클래스에서 컨트롤 해야 한다.

###### 업데이트 후 출력 확인

- view 함수에서 정의한 ArticleForm의 인스턴스(form) 하나로 input과 label 태그가 모두 렌더링 되는 것을 확인하기

- 각 태그의 속성 값들 또한 자동으로 설정 되어있다

###### Django의 2가지 HTML input 요소 표현

1. Form fields
   
   - 입력에 대한 유효성 검사 로직을 처리
   
   - 탬플릿에서 직접 사용됨

2. Widgets
   
   - 웹 페이지의 HTML input 요소 렌더링을 담당(input 요소의 단순한 출력 부분 담당)
   
   - Widgets은 반드시 form fields에 할당 됨

###### Widgets

- Django의 HTML input element의 표현을 담당

- 단순히 HTML 렌더링을 처리하는 것이며 유효성 검증과 아무런 관계가 없음

###### Form field와 widget 응용하기 -> 드랍다운

#### Django ModelForm

###### ModelForm Class

- Model을 통해 Form Class를 만들 수 있는 helper class

- ModelForm은 Form과 똑같은 방식으로 View함수에서 사용

###### ModelForm 선언

- forms 라이브러리에서 파생된 ModelForm클래스 상속받음

- 정의한 ModelForm 클래스 안에 Meta클래스를 선언

- 어떤 모델을 기반으로 form을 작성할 것인지에 대한 정보를 Meta클래스에 지정

```python
# articles/forms.py
from django import forms
form .models import Article

class ArticleForm(forms.ModelForm):

    class Meta:
        model = Article       # 어떤 모델을 기반으로 할지
        fields = '__all__'    # 어떤 모델 필드 중 어떤 것을 출력할지
```

-> runserver new 확인 -> TextField를 알아서 textarea로 바꾸어줌

###### modelform 에서의 Meta Class

- ModelForm의 정보를 작성하는 곳

- ModelForm을 사용할 경우 참조 할 모델이 있어야 하는데, Meta class의 model속성이 이를 구성함(참조하는 모델에 정의된 field 정보를 Form에 적용한다)

- fields속성에 --all-- 를 사용하여 모델의 모든 필드를 포함할 수 있다

- 또는 exclude 속성을 사용하여 모델에서 포함하지 않을 필드를 지정할 수 있다

```python
class ArticleForm(forms.ModelForm):

    class Meta:
        model = Article     
        fields = ('title',)
```

#### modelform with view functions CRUD

- ModelForm으로 인한 view함수의 구조 변화 알아보기

###### CREATE

- 유효성 검사를 통과하면 데이터 저장 후 상세 페이지로 리다이렉트

- 통과하지 못하면 작성 페이지로 리다이렉트

```python
# articles/views.py
def create(request):
    form = ArticleForm(request.POST)
    if form.is_valid():
        article = form.save()
        return redirect('articles:detail', article.pk)
    return redirect('articles:new')
```

###### "is_valid" 메소드

- 유효성 검사를 실행하고, 데이터가 유효한지 여부를 boolean으로 반환

- 데이터 유효성 검사를 보장하기 위한 많은 테스트에 대해 Django는 is_valid() 를 제공하여 개발자의 편의를 돕는다

###### The "save()" 메소드

- form 인스턴스에 바인딩 된 데이터를 통해 데이터베이스 객체를 만들고 저장

- ModelForm의 하위 클래스는 키워드 인자 instance 여부를 통해 생성할 지, 수정할 지를 결정함
  
  - 제공되지 않은 경우 save()는 지정된 모델의 새 인스턴스를 만듦(CREATE)
  
  - 제공되면 save()는 해당 인스턴스를 수정(UPDATE)

###### form 인스턴스의 errors속성

- is_valid()의 반환 값이 False인 경우 form 인스턴스의 errors속성에 값이 작성되는데, 유효성 검증을 실패한 원인이 딕셔너리 형태로 저장됨

- articles/views.py -> print(f'에러: {form.errors}')

- -> title 공백, content 적고 확인 

- 이 같은 특징을 통해 다음과 같은 구조로 코드를 작성하면 유효성 검증을 실패했을 때 사용자에게 실패 결과 메세지를 출력해줄 수 있음

```python
# articles/views.py
def create(request):
    form = ArticleForm(request.POST)
    if form.is_valid():
        article = form.save()
        return redirect('articles:detail', article.pk)
    context = {
        'form' : form,
    }
    return render(request, 'articles/new.html', context)
```

###### UPDATE

- ModelForm의 인자 instance는 수정 대상이 되는 객체(기존 객체)를 지정
1. request.POST
   
   - 사용자가 form을 통해 전송한 데이터(새로운 데이터)

2. instance
   
   - 수정이 되는 대상

###### edit view수정

```python
# articles/views.py
def edit(request, pk):
    article = Article.objects.get(pk=pk)
    form = ArticleForm(instance=article)
    context = {
        'article' : article,
        'form' : form,
    }
    return render(request, 'articles/edit.html', context)
```

###### edit 템플릿수정

```python
# articles/edit.html
{% extends 'base.html' %}

{% block content %}
  <h1>EDIT</h1>
  <form action="{% url 'articles:update' article.pk %}" method="POST">
    {% csrf_token %}
    {{ form.as_p }}
    <input type="submit">
  </form>
  <hr>
  <a href="{% url 'articles:detail' article.pk %}">뒤로가기</a>
{% endblock content %}
```

###### view 수정

```python
# articles/views.py
def update(request, pk):
    article = Article.objects.get(pk=pk)
    form = ArticleForm(request.POST, instance=article)
    if form.is_valid():
        form.save()
        return redirect('articles:detail', article.pk)
    context = {
        'form' : form,
    }
    return render(request, 'articles/new.html', context)
```

###### Form과 ModelForm

- ModelForm이 Form보다 더 좋은 것이 아니라 각자 역할이 다른 것

- Form
  
  - 사용자로부터 받는 데이터가 DB와 연관되어 있지 않는 경우에 사용
  
  - DB에 영향을 미치지 않고 단순 데이터만 사용하는 경우
  
  - 예 -> 로그인, 사용자의 데이터를 받아 인증 과정에서만 사용 후 별도로 DB에 저장하지 않음

- ModelForm
  
  - 사용자로부터 받는 데이터가 DB와 연관되어 있는 경우에 사용
  - 데이터의 유효성 검사가 끝나면 데이터를 각각 어떤 레코드에 맵핑해야 할지 이미 알고 있기 때문에 곧바로 save() 호출이 가능

#### Widgets활용하기

###### 위젯을 작성하는 2가지 방법

![]($(filename)_assets/2022-09-06-17-12-25-image.png)

###### 위젯을 활용하기

```python
# articles/forms.py
class ArticleForm(form.ModelForm):
    title = 
```



![]($(filename)_assets/2022-09-06-17-11-48-image.png)

![]($(filename)_assets/2022-09-06-17-11-59-image.png)

#### Handling HTTP requests

###### 개요

- HTTP requests 처리에 따른 view함수 구조 변화

- new-create, edit-update 의 view 함수 역할을 잘 살펴보면 하나의 공통점과 하느이 차이점이 있다

- 공통점
  
  - new-create 는 모두 CREATE 로직을 구현하기 위한 공통 목적
  
  - edit-update는 모두 UPDATE 로직을 구현하기 위한 공통 목적

- 차이점
  
  - new와 edit는 GET 요청에 대한 처리만을, create와 update는 POST 요청에 대한 처리만을 진행

- 이 공통점과 차이점을 기반으로, 하나의 view함수에서 method에 따라 로직이 분리되도록 변경

###### Create

- new와 create view 함수를 합침

- 각각의 역할을 request.method 값을 기준으로 나뉨

- 코드 작성 순서
  
  ```python
  def create(request):
      if request.method == 'POST':
          pass # 작성2
      else:
          pass # 작성1
  ```

```python
# articles/views.py
def create(request):
    if request.method == 'POST':
        # create
        form = ArticleForm(request.POST)
        if form.is_valid():
            article = form.save()
            return redirect('articles:detail', article.pk)
    else:
        # new
        form = ArticleForm()
    context = {              # if form.is_valid():에서 false로 평가 받았을 때
        'form' : form,       # 에러 정보가 담긴 form 인스턴스가 context로 넘어감
    }
    return render(request, 'articles/new.html', context)
```

- 이제 불필요해진 new의 view함수와 url path를 삭제
  
  - articles/views.py -> new 함수 삭제
  
  - articles/urls.py -> new path 삭제

![]($(filename)_assets/2022-09-06-17-37-34-image.png)

- new.html -> create.html 이름 변경 및 action 속성 값 수정

![]($(filename)_assets/2022-09-06-17-40-30-image.png)

- new.html -> create.html 이름변경으로 인한 템플릿 경로 수정

![]($(filename)_assets/2022-09-06-17-41-08-image.png)

- index 페이지에 있던 new 관련 링크 수정

![]($(filename)_assets/2022-09-06-17-41-40-image.png)

###### UPDATE

- edit과 update view 함수를 함침

```python
# articles/views.py
def update(request, pk):
    article = Article.objects.get(pk=pk)
    if request.method == 'POST':
        form = ArticleForm(request.POST, instance=article)
        if form.is_valid():
            form.save()
            return redirect('articles:detail', article.pk)
    else:
        form = ArticleForm(instance=article)
    context = {
        'form' : form,
        'article' : article,
    }
    return render(request, 'articles/update.html', context)
```

- new와 마찬가지로 불필요해진 edit의 view 함수와 url path를 삭제

![]($(filename)_assets/2022-09-06-17-47-53-image.png)

- edit.html -> update.html 이름 변경으로 인한 관련 정보 수정

![]($(filename)_assets/2022-09-06-17-48-43-image.png)

- edit.html -> update.html 이름 변경으로 인한 관련 정보 수정

![]($(filename)_assets/2022-09-06-17-49-05-image.png)

- POST 요청에 대해서만 삭제가 가능하도록 수정

![]($(filename)_assets/2022-09-06-17-49-30-image.png)

###### Delete

- 메소드가 POST일때만 삭제 

![]($(filename)_assets/2022-09-06-18-03-26-image.png)

###### ModelForm 으로 CRUD

- new/edit 없어짐

#### View decorators

###### 개요

- View decorators 를 사용해 view 함수를 단단하게 만들기

###### 데코레이터(Decorator)

- 기존에 작성된 함수에 기능을 추가하고 싶을 때, 해당 함수를 수정하지 않고 기능을 추가해주는 함수

- Django는 다양한 HTTP 기능을 지원하기 위해 view 함수에 적용 할 수 있는 여러 데코레이터를 제공

- 데코레이터 동작 예시

#### Allowed HTTP methods

###### 개요

- django.views.decorators.http의 데코레이터를 사용하여 요청 메서드를 기반으로 접근을 제한할 수 있음

- 일치하지 않는 메서드 요청이라면 405 Method Not Allowed를 반환

- 메서드 목록
  
  1.  require_http_methods()
  
  2.  require_POST()
  
  3.  require_safe()

###### require_http_methods()

- View 함수가 특정한 요청 method만 허용하도록 하는 데코레이터

![]($(filename)_assets/2022-09-06-18-27-18-image.png)

###### require_POST()

- View 함수가 POST 요청 method만 허용하도록 하는 데코레이터

![]($(filename)_assets/2022-09-06-18-28-06-image.png)

- url로 delete 시도 후 서버 로그에서 405 http status code 확인 해보기

![]($(filename)_assets/2022-09-06-18-29-11-image.png)

###### require_safe()

- require_GET이 있지만 Django에서는 require_safe를 사용하는 것을 권장

![]($(filename)_assets/2022-09-06-18-30-29-image.png)

#### Rendering fields manually

- django form 검색 -> Working with forms - Django documentation

- 목차 Working with form templates -> Rendering fields manually

- 수동으로 form 작성

![]($(filename)_assets/2022-09-06-18-56-28-image.png)

- Looping over the form's fields

![]($(filename)_assets/2022-09-06-18-57-54-image.png)

![]($(filename)_assets/2022-09-06-18-59-07-image.png)

#### 마무리

- Django Form Class
  
  - Django 프로젝트의 주요 유효성 검사 도구
  
  - 공격 및 데이터 손상에 대한 중요한 방어 수단
  
  - 유효성 검사에 대해 개발자에게 강력한 편의를 제공

- View 함수 구조 변화
  
  - HTTP requests 처리에 따른 구조 변화


