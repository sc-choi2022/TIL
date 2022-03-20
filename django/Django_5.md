# Django 5

### CRUD with views

1. 프로젝트 이름 : crud
2. 앱 이름 : articles
3. 앱 등록



#### 실습

**1 base 템플릿 작성 및 추가 템플릿 경로 등록**

templates/base.html

project/settings.py에 TEMPLATES =[{'DIRS': [BASE_DIR / 'templates']}] 

**2 index 페이지 작성**

articles/urls.py

```python
from django.urls import path
from . import views

app_name = 'articles'
url_patterns =[
    path('index/', views.index, name='index'),
]
```

articles/views.py

```python
from django.shortcut import render

def index(request):
    
    return render(request, 'index.html')
```

articles/templates/articles/index.html

```django
{% extends 'base.html' %}
{% block %}
	<h1 class="text-center">Articles</h1>
{% endblock %}
```



#### READ 전체 게시글 조회

articles/views.py

```python
from django.shortcuts import render
from .models import Articles

def index(request):
    articles = Article.objects.all()
    context = {
        'articles' : articles,
    }
    
    return render(request, 'articles/index.html', context)
```

articles/templates/articles/index.html

```django
{% extends 'base.html' %}
{% block %}
  <h1 class="text-center">Articles</h1>
  <hr>
  {% for article in articles %}
	<p>{{ article.pk }}</p>
	<p>{{ article.title }}</p>
	<p>{{ article.content }}</p>
  <hr>
  {% endfor %}
{% endblock %}
```

##### 게시글 정렬 순서 변경

articles/views.py

```python
def index(request):
    # 1. DB로부터 받은 쿼리셋을 이후에 파이썬이 변경(Python이 조작)
    article = Article.objects.all()[::-1]
    
    # 2. 처음부터 내림차순 쿼리센으로 받음 (DB가 조작)
    article = Article.objects.order_by('-pk')
    article = Article.objects.order_by('pk').reverse()
```



#### CREATE (New, Create)

##### New

articles/urls.py

```python
from django.urls import path
from . import views

app_name = "articles"
urlpatterns = [
    path('new/', views.new, name='new'),
]
```

articles/views.py

```python
from django.shortcuts import render

def new(request):
    
    return render(request, 'articles/new.html',)
```

templates/articles/new.html

```django
{% extends 'base.html' %}
{% block %}
  <h1 class="text-center">New</h1>
  <hr>
  <form action="#" method="GET">
      <label for="title">Title: </label>
      <input type="text" name="title"><br>
      <label for="content">Content: </label>
      <textarea name="content" cols="30" rows="5"></textarea><br>
      <input tyep="submit">
  </form>
  <hr>
  <a href={% url 'articles:index'%}>[back]</a>
{% endblock %}
```

articles/templates/articles/index.html

```django
{% extends 'base.html' %}
{% block %}
  <h1 class="text-center">Articles</h1>
  <a href="{% url 'articles:new' %}">NEW</a>
  <hr>
  {% for article in articles %}
	<p>{{ article.pk }}</p>
	<p>{{ article.title }}</p>
	<p>{{ article.content }}</p>
  <hr>
  {% endfor %}
{% endblock %}
```



##### Create

articles/views.py

```python
from django.shortcuts import render
from .models import Articles
def create(request):
    title = request.GET.get('title')
    content = request.GET.get('content')
    
    article = Article.objects.create(title=title, content=content)
    article.save()
    return render(request, 'articles/create.html')
```

templates/articles/new.html

```django
{% extends 'base.html' %}
{% block %}
  <h1 class="text-center">New</h1>
  <hr>
  <form action="{% url 'articles:create'%}" method="GET">
      <label for="title">Title: </label>
      <input type="text" name="title"><br>
      <label for="content">Content: </label>
      <textarea name="content" cols="30" rows="5"></textarea><br>
      <input tyep="submit">
  </form>
  <hr>
  <a href={% url 'articles:index'%}>[back]</a>
{% endblock %}
```

templates/articles/create.html

```django
{% extends 'base.html' %}
{% block %}
  <h1 class="text-center">글 작성 완료</h1>
{% endblock %}
```



#### HTTP method

##### GET

특정 리소스를 가져오도록 요청할 때 사용한다.

반드시 데이터를 가져올 때만 사용해야 한다.

DB에 변화를 주지 않는다.

CRUD에서 R 역할을 담당한다.



##### POST

서버로 데이터를 전송할 때 사용한다.

리소스를 생성/변경하기 위해 데이터를 HTTP body에 담아 전송한다.

서버에 변경사항을 만든다.

CRUD에서 C/U/D 역할을 담당한다.



#### 사이트 간 요청 위조 (Cross-site request forgery)

웹 애플리케이션 취약점 중 하나로 사용자가 자신의 의지와 무관하게 공격자가 의도한 행동을 하여 특정 웹페이지를 보안에 취약하게 하거나 수정, 삭제등의 작업을 하게 만드는 공격 방법이다.

Django는 CSRF에 대항하여 middleware와 template tag를 제공한다.

CSRF라고도 한다.



#### CSRF 공격 방어

Security Token 사용방식(CSRF Token)

* 사용자의 데이터에 임의의 난수 값을 부여해, 매 요청마다 해당 난수 값을 포함시켜 전송 시키도록 한다.
* 이후 서버에서 요청을 받을 때마다 전달된 token 값이 유효한지 검증한다.

일반적으로는 데이터 변경이 가능한 POST, PATCH, DELETE Method등에 적용한다.(GET 제외)

Django는 CSRF token 템플릿 태그를 제공한다.



#### csrf_token template tag

```django
{% csrf_token %}
```

CSRF 보호에 사용한다.

input type이 hidden으로 작성되며 value는 Django에서 생성한 hash 값으로 설정된다.

해당 태그 없이 요청을 보낸다면 Django 서버는 403 forbidden을 응답한다.



#### CsrfViewMiddleware

CSRF 공격 관련 보안 설정은 setting.py에서 MIDDLEWARE에 작성되어 있다.

실제로 **요청 과정**에서 urls.py 이전에 Middleware의 설정 사항들을 순차적으로 거치며 **응답**은 반대로 하단에서 상단으로 미들웨어를 적용시킨다.



#### [참고] Middleware

공통 서비스 및 기능을 애플리케이션에 제공하는 소프트웨어

데이터 관리, 애플리케이션 서비스, 메시징, 인증 및 API 관리를 미들웨어를 통해 처리한다.

개발자들이 애플리케이션을 보다 효율적으로 구축할 수 있도록 지원하며, 애플리케이션, 데이터 및 사요앚 사이를 연결하는 요소처럼 작동한다.



**new의 로직을 수정한다.**

articles/templates/articles/new.html

```django
{% extends 'base.html' %}
{% block %}
  <h1 class="text-center">New</h1>
  <hr>
  <form action="{% url 'articles:create'%}" method="POST">
    {% csrf_token %}
    <label for="title">Title: </label>
    <input type="text" name="title"><br>
    <label for="content">Content: </label>
    <textarea name="content" cols="30" rows="5"></textarea><br>
    <input tyep="submit">
  </form>
  <hr>
  <a href={% url 'articles:index'%}>[back]</a>
{% endblock %}
```

articles/views.py

```python
from django.shortcuts import render
from .models import Article

def create(request):
    title = request.POST.get('title')
    content = request.POST.get('content')
    
    article = Article.objects.create(title=title, content=content)
    article.save()
    return render(request, 'articles/create.html')
```

\+ POST 데이터 확인



#### 게시글 작성 후 index 페이지로 이동하기

articles/views.py

```python
from django.shortcuts import render
from .models import Article

def create(request):
    title = request.POST.get('title')
    content = request.POST.get('content')
    
    article = Article.objects.create(title=title, content=content)
    article.save()
    return render(request, 'articles/index.html')
```



**2가지 문제 발생**

1. 글을 작성 후 index 페이지가 출력되지만 게시글이 조회되지 않는다.
2. URL은 여전히 create에 머물러 있다.

단순히 index 페이지만 render 되었을 뿐이다.

* create view 함수에서 다루고 있는 데이터로 index 페이지가 render 된다.



#### Django shortcut function - 'redirect()'

새 URL로 요청을 다시 보낸다.

인자에 따라 HttpResponseRedirect를 반환한다.

브라우저는 현재 경로에 따라 전체 URL자체를 재구성한다.(reconstruct)

사용 가능한 인자

1. model
2. <u>view name</u>: viewname can be **URL pattern name** or callable **view object**
3. absolute or relative URL

articles/views.py

redirect 함수 적용

```python
from django.shortcuts import render, redirect
from .models import Article

def create(request):
    title = request.POST.get('title')
    content = request.POST.get('content')
    
    article = Article.objects.create(title=title, content=content)
    article.save()
    # return render(request, 'articles/index.html')
    return redirect('articles:index')
```



#### DETAIL

articles/urls.py

```python
from django.urls import path
from . import views

url_patterns = [
    path('int:<pk>/', views, name='detail'),
]
```

개별 게시글 상세 페이지

글의 번호(pk)를 활용해서 각각의 페이지를 구현해야한다.

**Variable Routing**을 활용한다.

articles/views.py

```python
from django.shortcuts import render
from .models import Article

def detail(request, pk):
    article = Article.objects.get(pk=pk)
    context ={
        'article' : article,
    }
    return render(request, 'articles/detail.html', context)
```

**article = Article.objects.get(pk=pk)**

오른쪽 pk는 variable routing을 통해 받은 pk

왼쪽 pk는 DB에 저장된 레코드의 pk(id)



**Detail 페이지 및 링크 작성**

articles/templates/articles/detail.html

```django
{% extends 'base.html' %}
{% block %}
  <h1 class="text-center">Detail</h1>
  <h3>{{ article.pk }}</h3>
  <hr>
  <p>{{ article.title }}</p>
  <p>{{ article.content }}</p>
  <p>{{ article.created_at }}</p>
  <p>{{ article.updated_at }}</p>
  <hr>
  <a href={% url 'articles:index'%}>[back]</a>
{% endblock %}
```

articles/templates/articles/index.html

```django
{% extends 'base.html' %}
{% block %}
  <h1 class="text-center">Articles</h1>
  <a href="{% url 'articles:new' %}">NEW</a>
  <hr>
  {% for article in articles %}
	<p>{{ article.pk }}</p>
	<p>{{ article.title }}</p>
	<p>{{ article.content }}</p>
    <a href={% url 'articles:detail' article.pk %}>detail</a>
  <hr>
  {% endfor %}
{% endblock %}
```



articles/views.py

redirect인자 변경

```python
from django.shortcuts import redirect

def create(request):
    
    return redirect('articlse:detail', article.pk)
```



#### DELETE

모든 글을 삭제하는 것이 아니라 삭제하고자 하는 특정 글을 삭제해야한다.

articles/urls.py

```python
from django.urls import path
url_patterns = [
    path('<int:pk>/delete', views.delete, name="delete"),
]
```

articles/views.py

```python
from django.shortcuts import redirect
def delete(request, pk):
    article = Article.objects.get(pk=pk)
    article.delete()
    return redirect('articles:index')
```

articles/templates/articles/detail.html

```django
{% extends 'base.html' %}
{% block %}
  <h1 class="text-center">Detail</h1>
  <h3>{{ article.pk }}</h3>
  <hr>
  <p>{{ article.title }}</p>
  <p>{{ article.content }}</p>
  <p>{{ article.created_at }}</p>
  <p>{{ article.updated_at }}</p>
  <hr>
  <form action="{% url 'articles:delete' article.pk %}" method="POST">
    {% csrf_token %}
    <button class="btn btn-danger">DELETE</button>
  </form>
  <a href={% url 'articles:index'%}>[back]</a>
{% endblock %}
```



HTTP Method POST시에만 삭제될 수 있도록 조건을 작성한다.

articles/views.py

```python
from django.shortcuts import redirect

def delete(request, pk):
    article = Article.objects.get(pk=pk)
    if request.method == "POST":
        article.delete()
        return redirect('articles:index')
    else:
        return redirect('articles:detail', article.pk)
```



#### EDIT

수정은 기존에 입력되어 있던 데이터를 보여주는 것이 좋기 때문에 html태그의 value속성을 사용한다.

(textarea 태그는 value 속성이 없으므로 태그 내부 값으로 작성한다.)



**edit**

articles/urls.py

```python
from django.urls import path

url_patterns = [
    path('<int:pk>/edit/', views.edit, name="edit"),
]
```

articles/views.py

```python
from django.shortcuts import redirect

def edit(request, pk):
    article = Article.objects.get(pk=pk)
    context = {
        'article' : article,
    }
    return render(request, 'articles/edit.html', context)
```

articles/templates/articles/edit.html

```django
{% extends 'base.html' %}
{% block %}
  <h1 class="text-center">EDIT</h1>
  <hr>
  <form action="#" method="POST">
    {% csrf_token %}
    <label for="title">Title: </label>
    <input type="text" name="title" value="{{ article.title }}"><br>
    <label for="content">Content: </label>
    <textarea name="content" cols="30" rows="5" value="{{ article.content }}"></textarea><br>
    <input tyep="submit">
  </form>
  <hr>
  <a href={% url 'articles:index'%}>[back]</a>
{% endblock %}
```

articles/templates/articles/detail.html

detail.html에 edit 링크 작성

```django
{% extends 'base.html' %}
{% block %}
  <h1 class="text-center">Detail</h1>
  <h3>{{ article.pk }}</h3>
  <hr>
  <p>{{ article.title }}</p>
  <p>{{ article.content }}</p>
  <p>{{ article.created_at }}</p>
  <p>{{ article.updated_at }}</p>
  <hr>
  <a href="{% url 'articles:edit' article.pk %}" class="btn btn-primary">EDIT</a>
  <form action="{% url 'articles:delete'article.pk %}" method="POST">
    {% csrf_token %}
    <button class="btn btn-danger">DELETE</button>
  </form>
  <a href={% url 'articles:index'%}>[back]</a>
{% endblock %}
```



**UPDATE**

create와 마찬가지로 별도의 '글이 수정되었습니다.'라는 메시지를 출력하는 template는 필요하지 않다.

articles/urls.py

```python
from django.urls import path

url_patterns = [
    path('<int:pk>/update/', views.update, name="update"),
]
```

articles/views.py

```python
from django.shortcuts import redirect

def update(request, pk):
    article = Article.objects.get(pk=pk)
    article.title = request.POST.get('title')
    article.content = request.POST.get('content')
    article.save()
    return redirect('articles:detail', article.pk)
```

articles/templates/articles/edit.html

```django
{% extends 'base.html' %}
{% block %}
  <h1 class="text-center">EDIT</h1>
  <hr>
  <form action="{% url 'articles:update' article.pk %}" method="POST">
    {% csrf_token %}
    <label for="title">Title: </label>
    <input type="text" name="title" value="{{ article.title }}"><br>
    <label for="content">Content: </label>
    <textarea name="content" cols="30" rows="5" value="{{ article.content }}"></textarea><br>
    <input tyep="submit">
  </form>
  <hr>
  <a href={% url 'articles:index'%}>[back]</a>
{% endblock %}
```



### 마무리

Model

* 웹 애플리케이션의 데이터를 구조화하고 조작하기 위한 도구



Database

* 체계화된 데이터의 모입(집합)



Migrations

* Django가 model에 생긴 변화(필드를 추가, 수정, 삭제)를 반영하는 방법



ORM

* OOP 언어를 사용하여 데이터베이스와 OOP언어간의 호환되지 않는 데이터를 변환하는 프로그래밍 기법



Database API

* DB를 조작하기 위한 도구(QuerySet API, CRUD)



Admin Site

* 사용자가 아닌 서버의 관리자가 활용하기 위한 페이지