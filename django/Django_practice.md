# Django

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



4 프로젝트 생성

```bash
$ django-admin startproject firstpjt .
# firstpjt is the name of project
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

我 urls.py import articles import views



## 요청과 응답

**urls.py**

<기본>

```python
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
]
```

<추가 후>

```python
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
    path('article'),
]
```



### App URL mapping

각 app에 urls.py를 작성하게 된다.

<원래 프로젝트의 urls.py>

```python
from django.contrib import admin
from django.urls import path
from articles import views

urlpatterns = [
    path('admin/', admin.site.urls),
    # path('주소/', view 함수)
    path('index/', views.index),
    path('greeting/', views.greeting),
    path('dinner/', views.dinner),
    path('dtl-practice/', views.dtl_practice),
    path('throw/', views.throw),
    path('catch/', views.catch),
    path('hello/<str:name>/', views.hello),
]
```

<프로젝트의 urls.py>

```python
from django.contrib import admin
from django.urls import path, include
from articles import views

urlpatterns = [
    path('admin/', admin.site.urls),
    # path('주소/', view 함수)
    path('articles', include('articles.urls'))
]
```

<application의 urls.py>

```python
from django.urls import path
from . import views

urlpatterns = [
    # path('주소/', view 함수)
    path('index/', views.index),
    path('greeting/', views.greeting),
    path('dinner/', views.dinner),
    path('dtl-practice/', views.dtl_practice),
    path('throw/', views.throw),
    path('catch/', views.catch),
    path('hello/<str:name>/', views.hello),
]
```

**throw catch의 경우 수정이 필요하다 **

throw.html

```python
{% extends 'base.html' %}

{% block content %}
  <h1>Throw</h1>
  <form action="/catch/" method="GET">
    <label for="message">Throw</label>
    <input type="text" id="message" name="message">
    <input type="submit">
  </form>
{% endblock content %}
```

```python
{% extends 'base.html' %}

{% block content %}
  <h1>Throw</h1>
  <form action="/articles/catch/" method="GET">
    <label for="message">Throw</label>
    <input type="text" id="message" name="message">
    <input type="submit">
  </form>
{% endblock content %}
```



### Naming URL patterns

링크에 url을 직접 작성하는 것이 아니라 path() 함수의 name인자를 정의해서 사용한다.

Django Template Tag 중 하나인 url 태그를 사용해서 path() 함수에 작성한 name을 사용할 수 있다.

url 설정에 정의된 특정한 경로들의 의존성을 제거할 수 있다.

articles의 urls.py **前**

```python
from django.urls import path
from . import views

urlpatterns = [
    # path('주소/', view 함수)
    path('index/', views.index),
    path('greeting/', views.greeting),
    path('dinner/', views.dinner),
    path('dtl-practice/', views.dtl_practice),
    path('throw/', views.throw),
    path('catch/', views.catch),
    path('hello/<str:name>/', views.hello),
]
```



articles의 urls.py **後**

```python
from django.urls import path
from . import views

urlpatterns = [
    # path('주소/', view 함수)
    path('index/', views.index, name='index'),
    path('greeting/', views.greeting, name='greeting'),
    path('dinner/', views.dinner, name='dinner'),
    path('dtl-practice/', views.dtl_practice, name='dtl_practice'),
    path('throw/', views.throw, name='throw'),
    path('catch/', views.catch, name='catch'),
    path('hello/<str:name>/', views.hello, name='hello'),
]
```



throw.html **前**

```python
{% extends 'base.html' %}

{% block content %}
  <h1>Throw</h1>
  <form action="/articles/catch/" method="GET">
    <label for="message">Throw</label>
    <input type="text" id="message" name="message">
    <input type="submit">
  </form>
{% endblock content %}
```

throw.html **後**

```python
{% extends 'base.html' %}

{% block content %}
  <h1>Throw</h1>
  <form action="{% url 'catch' %}" method="GET">
    <label for="message">Throw</label>
    <input type="text" id="message" name="message">
    <input type="submit">
  </form>
{% endblock content %}
```



catch.html **前**

```python
{% extends 'base.html' %}

{% block content %}
  <h1>Catch</h1>
  <h2>{{message}}를 받았다!</h2>
  <a href="/throw/">다시 던질게</a>
{% endblock content %}
```

catch.html **後**

```python
{% extends 'base.html' %}

{% block content %}
  <h1>Catch</h1>
  <h2>{{message}}를 받았다!</h2>
  <a href="{% url 'throw' %}">다시 던질게</a>
{% endblock content %}
```



venv는 git으로 관리하지 않는다.

* git init을 하고 add 하기 전에 .gitignore를 사용하여 관리하지 않겠다고 말해준다.

대신, requirements.txt를 사용하여 라이브러리 목록만 관리한다.

* pip freeze > requirements.txt

명령어를 사용하여 라이브러리 목록을 저장하고

* pip install -r requirements.txt

명령어를 사용하여 저장된 라이브러리들을 다운받는다.