# Django manual

## Git

New repository

* Repository name

* Public / Private

* Create repository



Clone

```bash
$ git clone https://github.com/sc-choi2022/Django.git .
```

```bash
$ git remote -v
```

```bash
$ git push -u origin master
```



## 가상환경, Django

첫 add를 하기 전에 .ignore 생성

https://www.toptal.com/developers/gitignore

* Django
* Python
* venv
* VisualStudioCode
* Windows



1 가상환경 만들기

```bash
$ python -m venv venv
```

2 활성화

```bash
$ source venv/Scripts/activate
```

3 django 설치

```bash
$ pip install django==3.2.12
```

```bash
$ pip install -r requirements.txt
```

```bash
$ pip freeze > requirements.txt
```



4 프로젝트 생성

```bash
$ django-admin startproject crud .
# crud is the name of project
```

5 Django 시작하기

```bash
$ python manage.py runserver
```

`http://127.0.0.1:8000/`  ctrl + click



6 로켓 확인

**The install worked successfully! Congratulations!**



7 Application 생성

* 일반적으로 Application명은 **복수형**으로 하는 것을 권장

```bash
$ python manage.py startapp articles
# articles is the name of Application
```



8 Application 등록

firstpjt > settings.py

```python
INSTALLED_APPS = [
    'articles',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

<u>**반드시 앱 생성 후 등록!**</u>



## DB

#### models.py 작성

```python
from django.db import models

class Article(models.Model):
    title = models.CharField(max_length=10)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add = True)
    updated_at = models.DateTimeField(auto_now = True)
```

models 모듈을 통해 어떠한 타입의 DB 컬럼을 정의할 것인지 정의한다.

* title과 content은 모델의 필드를 나타낸다.
* 각 필드는 크래스 속성으로 지정되어 있으며, 각 속성은 각 데이터베이스의 열에 매핑한다.

**CharField(max_length=, \*\*options)**

* <u>길이의 제한이 있는 문자열</u>을 넣을 때 사용한다.
* CharField의 max_length는 필수 인자
* **필드의 최대 길이(문자),** 데이터베이스 레벨과 Django의 <u>유효성 검사</u>(값을 검증하는 것)에서 활용한다.

**TextField(\*\*options)**

* 글자의 수가 많을 때 사용한다.
* max_length 옵션 작성시 자동 양식 필드인 <u>textarea 위젯에 반영은 되지만 모델과 데이터베이스 수준에는 적용되지 않는다</u>.
  * max_length 사용은 CharField에서 사용해야한다.



## Migrations

makemigrations

```bash
$ python manage.py makemigrations
```

'migrations/0001_initial.py' 생성 확인

* db.sqlite3 우클릭 Open Database하면 SQLITE EXPLORER에 아무것도 없다.

migrate

```bash
$ python manage.py migrate
```

0001_initial.py 설계도를 실제 DB에 반영

* db.sqlite3 우클릭 Open Database하면 SQLITE EXPLORER에 반영된다.
* articles/models.py의 적성 내용이 articles.article에 반영되어 있다.

#### 반드시 기억해야 할 migration 3단계

1. models.py
   * model 변경사항 발생 시
2. $ python manage.py makemigrations
   * migration 파일 생성
3. $ python manage.py migrate
   * DB 반영(모델과 DB의 동기화)

**cf)**

sqlmigrate

해당 migrations 설계도가 SQL문으로 어떻게 해석되어서 동작할지 미리 확인 가능

```bash
$ python manage.py sqlmigrate app_name 0001
```



showmigrations

```bash
$ python manage.py showmigrations
```

migrations 설계도들이 migrate 됐는지 안됐는지 여부 확인 가능

설계도들의 목록을 볼 수 있다.

**model 수정**

```python
# articles/models.py
class Article(models.Model):
    title = models.CharField(max_lenght=10)
    content = models.TextField()
    created_at = models.DataTimeField(auto_now_add=True)
    updated_at = models.DataTimeField(auto_now=True)
```

추가 모델 필드 작성 후 makemigrations 진행



created_at 필드에 대한 default 값 설정

```bash
You are trying to add the field 'created_at' with 'auto_now_add=True' to article without a defalut; the database need something to populate exiting rows.
1) Probide a one-off default now (will be set on all existing rows)
2) Quit, and let me add a default in models.py
Select an option: 1
```

created_at 필드에 대한 default 값 설정

=> 1 입력 후 enter



```bash
Please enter the default value now, as valid Python
You can accept the default 'timezone.now' by presing 'Enter' or you can provide another value.
The datetime and django.utils.timezone modules are available, so you can do e.g. timezone.now Type 'exit' to exit this prompt
[default: timezone.now] >>>
```

timezone.now 함수 값 자동 설정

=>빈 값 상태에서 enter 클릭

=>migrate를 통해 models.py 수정사항 반영



## Form

forms.py를 생성하고 코드르 작성한다.

#### Form class

```python
from django import forms
from .models import Article

class ArticleForm(forms.Form):
    title = forms.CharField(max_length=10)
    content = forms.CharField(widget=forms.Textarea)
    REGION_A = "sl"
    REGION_B = "dj"
    REGION_C = "gj"
    REGIONS_CHOICES = [
        (REGION_A, '서울'),
        (REGION_B, '대전'),
        (REGION_C, '광주'),
    ]
    region = forms.ChoiceField(choices=REGIONS_CHOICES,widget=forms.Select())
```



#### ModelForm class

Django Form을 사용하다 보면 Model에 정의한 필드를 유저로부터 입력받기 위해 Form에서 Model 필드를 재정의하는 행위가 중복 될 수 있다.

Django는 Model을 통해 Form Class를 만들 수 있는 ModelForm이라는 Helper를 제공한다.

##### ModelForm이 쉽게 해주는 것

* Model로 만들어지 테이블 필드 속성에 맞는 html element를 만들어 준다.
* 이를 통해 받은 데이터를 view함수에서 유효성 검사를 할 수  있도록 한다.

##### 왜 ModelForm을 쓰는가?

* DB에 저장된 구조를 그대로 Form에서 사용하기 위해

**ModelForm과 Form은 역할이 다르다**

* ModelForm: Form으로 받아서 DB에 저장
* Form: DB와 관련 없이 사용자의 입력을 받아 처리

```python
from django import forms
from .models import Article

class ArticleForm(forms.ModelForm):
    class Meta:
        model = Article
        fields = '__all__'
        # exclude = ('title',)
```

정의한 클래스 안에 Meta 클래스를 선언하고, 어떤 모델을 기반으로 Form을 작성할 것인지에 대한 정보를 Meta클래스에 지정한다.

* 클래스 변수 fields와 exclude는 동시에 사용할 수 없다.

#### Meta class

Model의 정보를 작성하는 곳

ModelForm을 사용하기 위해서는 사용할 모델이 있어야하는데 Meta Class가 이를 구성한다.

- 해당 Model에 정의한 field 정보를 Form에 적용하기 위한 것



##### class, placeholder등을 설정하는 방법

```python
from django import forms
from .models import Article

class ArticleForm(forms.ModelForm):
    title = forms.CharField(
        label = '제목:',
        widget = forms.TextInput(
            attrs={
                'class' : 'title',
                'placeholder' : 'Enter the title',
            }
        ),
    )
    content = forms.CharField(
        label = 'Content:',
        widget = forms.Textarea(
            attrs = {
                'class' : 'content',
                'rows' : 10,
                'cols' : 50,
            }
        ),
        error_messages={
            'required' : 'Please enter your content',
        }
    )

    class Meta:
        model = Article
        fields = '__all__'
```

## Admin Site

#### admin 생성

```bash
$ python manage.py createsuperuser
```

관리자 계정 생성 후 서버를 실행한 다음 '/admin'으로 가서 관리자 페이지 로그인

* 계정만 만든 경우 Django 관리자 화면에서 아무 것도 보이지 않는다.

내가 만든 Model을 보기 위해서는 admin.py에 작성하여 Django 서버에 등록한다.

**주의** auth에 관련된 기본 테이블이 생성되지 않으면 관리자 계정을 생성할 수 없다.



#### admin 등록

```python
# articles/admin.py

from django.contrib import admin
from .models import Article

# admin site에 register하겠다.
admin.site.register(Article)
```

admin.py는 관리자 사이트에 Article 객체가 관리자 인터페이스를 가지고 있다는 것을 알려주는 것

models.py에 정의한 \_\_str\_\_의 형태로 객체가 표현된다.



#### ModelAdmin options

```python
# articles/admin.py

from django.contrib import admin
from .models import Article

class ArticleAdmin(admin.ModelAdmin):
    list_display = ('pk', 'title', 'content', 'created_at', 'updated_at')
    
admin.site.register(Article, ArticleAdmin)    
```

**list_display**

* models.py 정의한 각각의 속성(컬럼)들의 값(레코드)을 admin 페이지에 출력하도록 설정



list_filter, list_display_links 등 다양한 ModelAdmin options 참고

## CRUD

### Base.html

templates 폴더 생성, base.html 내부에 생성

base.html

**bootstrap 추가 & block 설정**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
</head>
<body>
  <div class="container">
    {% block content %}
    {% endblock content %}
  </div>
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script>
</body>
</html>

```



setting.py에 등록

```python
# crud > settings.py
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates',],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```



### CREATE

```python
# articles/urls.py
from django.urls import path
from . import views

app_name = 'articles'
urlpatterns = [
    path('create/', views.create, name='create'),
]
```

```python
# articles/views.py
from django.shortcuts import render
from .forms import ArticleForm

def create(request):
    if request.method == 'POST':
        # create
        form = ArticleForm(request.POST)
        # validation
        if form.is_valid():
            article = form.save()
            return
    else:
        form = ArticleForm()
    context = {
        'form' : form,
    }
    return render(request, 'articles/create.html', context)
```

```html
{% extends 'base.html' %}

{% block content %}
  <h1>CREATE</h1>
  <hr>
  <form action="{% url 'articles:create' %}" method="POST">
    {% csrf_token %}
    <div>
      {{ form.title.errors}}
      {{ form.title.label_tag }}
      {{ form.title }}
    </div>
    <div>
      {{ form.content.errors}}
      {{ form.content.label_tag }}
      <br>
      {{ form.content }}
    </div>
    <input type="submit" value="submit">
  </form>
{% endblock content %}
```



### READ

#### index

```python
# articles/urls.py
from django.urls import path
from . import views

app_name = 'articles'
urlpatterns = [
    path('', views.index, name="index"),
    path('create/', views.create, name='create'),
]
```

```python
# articles/views.py
from django.shortcuts import render
from .models import Article

def index(request):
    articles = Article.objects.order_by('-pk')
    context = {
        'articles' : articles,
    }
    return render(request, 'articles/index.html', context)
```

```html
{% extends 'base.html' %}

{% block content %}
  <h1>Articles</h1>
  <a href="{% url 'articles:create' %}">CREATE</a>
  <hr>
  {% for article in articles %}
    <p>글 번호: {{ article.pk }}</p>  
    <p>글 제목: {{ article.title }}</p>
    <p>글 내용: {{ article.content }}</p>
    <hr>
  {% endfor %}
  {% comment %} <a href="{% url 'articles:detail' %}">CREATE</a> {% endcomment %}
{% endblock content %}
```

#### detail

```python
# articles/urls.py
from django.urls import path
from . import views

app_name = 'articles'
urlpatterns = [
    path('', views.index, name="index"),
    path('create/', views.create, name='create'),
    path('<int:pk>/', views.detail, name='detail'),
]
```

```python
# articles/views.py
from django.shortcuts import render
from .models import Article

def detail(request, pk):
    article = Article.objects.get(pk=pk)
    context = {
        'article' : article
    }
    return render(request, 'articles/detail.html', context)
```

+

```python
def create(request):
    if request.method == 'POST':
        # create
        form = ArticleForm(request.POST)
        # validation
        if form.is_valid():
            article = form.save()
            return redirect('articles:detail')
```

```html
{% extends 'base.html' %}

{% block content %}
  <h1>Detail</h1>
  <h1>{{ article.title }}</h1>
  <p>{{ article.content }}</p>
  <p>작성일: {{ article.created_at }}</p>
  <p>수정일: {{ article.updated_at }}</p>
  <hr>
  <a href="{% url 'articles:index' %}">back</a>
{% endblock content %}
```

+index.html

```html
{% extends 'base.html' %}

{% block content %}
  <h1>Articles</h1>
  <a href="{% url 'articles:create' %}">CREATE</a>
  <hr>
  {% for article in articles %}
    <p>글 번호: {{ article.pk }}</p>  
    <p>글 제목: {{ article.title }}</p>
    <p>글 내용: {{ article.content }}</p>
    <a href="{% url 'articles:detail' article.pk %}">DETAIL</a>
    <hr>
  {% endfor %}
{% endblock content %}
```



### UPDATE

```python
# articles/urls.py
from django.urls import path
from . import views

app_name = 'articles'
urlpatterns = [
    path('', views.index, name="index"),
    path('create/', views.create, name='create'), # GET / POST
    path('<int:pk>/', views.detail, name='detail'),
    path('<int:pk>/update/', views.update, name='update'), # GET / POST
]
```

```python
# articles/views.py
from django.shortcuts import render, redirect
from .models import Article
from .forms import ArticleForm

def update(request, pk):
    article = Article.objects.get(pk=pk)
    if request.method == 'POST':
        form = ArticleForm(request.POST, instance=article)
        if form.is_valid():
            article = form.save()
            return redirect('articles:detail', article.pk)
    else:
        form = ArticleForm(instance=article)
    context = {
        'article' : article,
        'form' : form,
    }
    return render(request, 'articles/update.html', context)
```

```html
{% extends 'base.html' %}
{% block content %}
<h1>UPDATE</h1>
<hr>
<form action="{% url 'articles:update' article.pk %}" method="POST">
  {% csrf_token %}
  {{ form.as_p }}
  <input type="submit">
</form>
{% endblock content %}
```

+detail.html

```html
{% extends 'base.html' %}

{% block content %}
  <h1>Detail</h1>
  <h1>{{ article.title }}</h1>
  <p>{{ article.content }}</p>
  <p>작성일: {{ article.created_at }}</p>
  <p>수정일: {{ article.updated_at }}</p>
  <hr>
  <a href="{% url 'articles:index' %}">BACK</a>
  <a href="{% url 'articles:update' article.pk %}">UPDATE</a>
{% endblock content %}
```



### DELETE

```python
# articles/urls.py
from django.urls import path
from . import views

app_name = 'articles'
urlpatterns = [
    path('', views.index, name="index"),
    path('create/', views.create, name='create'), # GET / POST
    path('<int:pk>/', views.detail, name='detail'),
    path('<int:pk>/update/', views.update, name='update'), # GET / POST
    path('<int:pk>/delete/', views.delete, name='delete'),
]
```

```python
# articles/views.py
from django.shortcuts import redirect
from .models import Article

def delete(request, pk):
    article = Article.objects.get(pk=pk)
    if request.method == 'POST':
        article.delete()
        return redirect('articles:index')
    else:
        return redirect('articels:detail', article.pk)
```

+detail.html

```html
{% extends 'base.html' %}

{% block content %}
  <h1>Detail</h1>
  <h1>{{ article.title }}</h1>
  <p>{{ article.content }}</p>
  <p>작성일: {{ article.created_at }}</p>
  <p>수정일: {{ article.updated_at }}</p>
  <hr>
  <a href="{% url 'articles:index' %}">BACK</a>
  <form action="{% url 'articles:delete' article.pk %}" method="POST">
    {% csrf_token %}
    <input type="submit" value="DELETE">
  </form>
  <a href="{% url 'articles:update' article.pk %}">UPDATE</a>
{% endblock content %}
```

