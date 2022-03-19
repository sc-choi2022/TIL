# Django 1

Python Web framework

you can focus on writing your app without needing to reinvent the wheel



### Web framework

Web: World Wide Web



#### Static web  page(정적 웹 페이지)

서버에 미리 저장된 파일이 사용자에게 그대로 전달되는 웹 페이지

서버가 정적 웹 페이지에 대한 요청을 받은 경우 서버는 추가적인 처리 과정 없이 클라이언트에게 응담을 보낸다.

**<u>모든 상황에서 모든 사용자에게 동일한 정보를 표시</u>** 정적 웹 페이지의 큰 특징

일반적으로 HTML, CSS, JavaScript로 작성된다.

flat page라고도 한다.



#### Dynamic web page(동적 웹 페이지)

웹 페이지에 대한 요청을 받은 경우 서버는 <u>추가적인 처리 과정</u> 이후 클라이언트에게 응답을 보낸다.

동적 웹 페이지는 <u>방문자와 상호작용하기 때문에 페이지 내용은 그때그때 다르다</u>.

<u>서버 사이드 프로그래밍 언어</u>(Python, Java, C++등 )가 사용되며, 파일을 처리하고 데이터베이스와의 상호작용이 이루어진다.



#### Framework

프로그래밍에서 특정 운영 체제를 위한 응용 프로그램 표준 구조를 구현하는 <u>클래스와 라이브러리 모임</u>

<u>재사용할 수 있는 수많은 코드</u>를 프레임워크로 통합함으로써 개발자가 새로운 애플리케이션을 위한 표준 코드를 다시 작성하지 않아도 같이 사용할 수 있도록 돕는다.

(tool과 환경을 제공한다.)

Application framework라고도 한다.



#### Web Framework

**웹 페이지를 개발하는 과정에서 겪는 어려움을 줄이는 것이 주 목적**으로 데이터베이스 연동, 템플릿 형태의 표준, 세션 관리, 코드 재사용 등의 기능을 포함한다.

동적인 웹 페이지나, 웹 애플리케이션, 웹 서비스 개발 보조용으로 만들어지는 Application Framework의 일종이다.



(Python web framework는 python으로 작성된 web framework)

(Django를 사용할 때 내부적으로 다시 python코드를 작성하게 된다.)



#### Django를 사용해야 하는 이유

검증된 Python 언어 기반 Web framework

대규모 서비스에도 안정적이며 오랫동안 세계적인 기업들에 의해 사용되었다.



#### Framework Architecture

MVC Design Pattern (model-view-controller)

소프트웨어 공학에서 사용되는 디자인 패턴 중 하나

사용자 인터페이스로부터 프로그램 로직을 분리하여 애플리케이션의 시각적 요소나 이면에서 실행되는 부분을 서로 영향 없이 쉽게 고칠 수 있는 애플리케이션을 만들 수 있다.

**Django**는 **MTV Pattern**이라고 한다.



#### MTV Pattern

Model

* 응용프로그램의 데이터 구조를 정의하고 데이터베이스의 기록을  관리한다.
* (추가, 수정, 삭제)

Template (MVC pattern의 View)

* 파일의 구조나 레이아웃을 정의
* 실제 내용을 보여주는 데 사용<u>(presentation)</u>

**View** (MVC pattern의 controller)

* HTTP 요청을 수신하고 HTTP응답을 반환한다.
* <u>Model</u>을 통해 요청을 충족시키는데 필요한 데이터에 접근
* <u>template에게 응답의 서식 설정을 맡긴다.</u>

| MVC Pattern | MTV (Django) |
| ----------- | ------------ |
| Model       | Model        |
| View        | Template     |
| Controller  | View         |



### Django Intro

Django 설치 전 가상환경 생성 및 활성화

```bash
$ python -m venv venv
$ python venv/Scripts/activate
```

cf) terminal 환경 추가 사항 有 3/2 1



```bash
# django 설치
$ pip install django==3.2.12
# 현재 환경에 설치된 패키지 목록 확인
$ pip list
# 프로젝트 생성
$ django-admin startproject firstpjt .
# django 서버 실행(활성화)
$ python manga.py runserver
```

cf) LTS (Long Term Support) 장기 지원 버전

프로젝트 이름 주의사항

* Python이나 Django에서 사용 중인 키워드 및 '-'(하이픈 사용 불가)

다음과 같은 것은  되지 않는다.

​	`$ django-admin startproject Django .`

​	`$ django-admin startproject text .` 

​	`$ django-admin startproject class .`

​	`$ django-admin startproject django-test .`   



#### 프로젝트 구조

```
firstpjt
	__init__.py
	asgi.py
	settings.py
	urls.py
	vsgi.py
manage.py
```

##### \_\_init\_\_.py

* Python에게 이 디렉토리를 하나의 Python 패키지로 다루도록 지시하는 역할
* 건드릴 일 없다.



##### asgi.py

* Asynchronous Server Gateway Interface
* 비동기 서버 게이트웨이 인터페이스
* Django 애플리케이션이 비동기식 웹 서버와 연결 및 소통하는 돕는 역할
* 배포할 때 사용한다.
* 수업에서는 사용하지 않는다.



##### setting.py

* 애플리케이션의 모든 설정을 포함한다.
* Django 프로젝트의 모든 설정을 여기서 관리한다.



##### urls.py

* 사이트의 url과 적절한 views의 연결을 지정하는 역학
* 요청이 들어왔을 때 가장 먼저 만난다.



##### wsgi.py

* Web Server Gateway Interface
* Django 애플리케이션이 웹서버와 연결 및 소통하는 것을 돕는 역할
* 다른 서버에 연결할 때, 배포할 때 사용한다.



##### manage.py

* Django 프로젝트와 다양한 방법으로 상호작용하는 커맨드라인 유틸리티의 역할
* manage.py를 통해서 command를 동작하게 할 것이다.

```bash
# manage.py Usage
$ python manage.py <command> [options]
$ python manage.py runserver
```

cf) 서버를 끄는 방법 ctrl + c



**이 중 touch하지 않는 것!**

`__init__.py` `asgi.py` `wsgi.py` `manage.py`



#### Application 생성

일반적으로 Application명은 <u>**복수형**으로 하는 것을 권장</u>

```bash
$ python manage.py startapp articles
```

* articles가 application명
* project와 동등한 위치에 폴더가 생성된다.



#### Application 구조

```
articles
	migrations
	__init__.py
	admin.py
	apps.py
	models.py
	tests.py
	views.py
```

##### admin.py

* 관리자용 페이지를 설정하는 곳



##### apps.py

* 앱의 정보가 작성된 곳
* 만든 articles에 대한 app의 정보가 기록되어있다.
* 수정하지 않는다.



##### models.py

* 앱에서 사용하는 Model을 정의하는 곳
* MTV pattern의 M



##### tests.py

* 프로젝트의 테스트 코드를 작성하는 곳
* 서버를 테스트할 수 있는 코드들이 있다.
* 수업에서 사용하지는 않는다.



##### views.py

* view 함수들이 정의 되는 곳
* MTV pattern의 V

 

**MTV의 templates는 Django 명령어를 통해서 자동으로 생성되지 않는다.**

직접 생성해주어야한다.



 **Application만들 때 이 중 touch하지 않는 것!**

`__init__.py` `apps.py` `tests.py`



#### Project & Application

**Project(프로젝트)**

* 프로젝트는 앱의 집합 (collection of apps)
* 프로젝트에는 여러 앱이 포함될 수 있다.
* 앱은 여러 프로젝트에 있을 수 있다. (참고, 프로젝트가 커지면)



**Application(앱)**

* 앱은 실제 요청을 처리하고 페이지를 보여주고 하는 등의 역할을 담당한다.
  * 프로젝트에는 model도 view도 없었다.
* 하나의 프로젝트는 여러 앱을 가진다.
* 일반적으로 앱은 하나의 역할 및 기능 단위로 작성한다.



#### 앱 등록

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

프로젝트에서 앱을 사용하기 위해서는 반드시 INSTALLED_APPS 리스트에 추가해야한다.

**INSTALLED_APPS**

* Django installation에 활성화된 모든 앱을 지정하는 문자열 목록



#### 앱 생성시 주의 사항

**반드시 앱을 생성한 후 등록**

INSTALLED_APPS에 먼저 작성(등록)하고 생성하려면 앱이 생성되지 않는다.

작성시 추가 되는 것과 기존의 것을 순서를 구분하는 것을 권장한다.

* Local apps
* Third party apps
* Django apps



### 요청과 응답

클라이언트가 admin/를 요청

urls.py의 admin/ 요청을 확인 이를 보여줄 수 있는 view함수가 호출 필요 전달

views.py 안에 페이지를 return할 수 있는 함수 존재

Template안에 \<filename>.html 이 있어야 페이지를 보여준다.

views.py 함수가 URLS 요청을 받고 Template을 준비하여 응답

#### URLS

firstpjt > urls.py

<기본>

Django는 admin page가 기본적으로 만들어져 있다.

서버가 받아서 관리자페이지를 준다.

```python
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
]
```

```python
from django.contrib import admin
from django.urls import path
from articles import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('index/', views.index),
]
```

index/ 요청이 들어왔을 때 views.index 함수를 실행한다.

* ,: trailing comma
  * django에서 권장
  * 이후에 바로 작성할 수 있게 생산성을 높히기 위한 것



#### View

articles > views.py

```python
from django.shortcuts import render

def index(request):
    return render(request, 'index.html')
```

HTTP요청을 수신하고 HTTP 응답을 반환하는 함수 작성한다.

Model을 통해 요청에 맞는 필요 데이터에 접근한다.

Template에게 HTTP 응답 서식을 맡긴다.

**view함수의 규칙**

* 필수 인자 request

  `def index(request):`

  * HTTP request 객체: url의 요청 객체가 request 함수로 넘어오는 것
  * 요청 객체 안에 클라이언트들이 보낸 정보들이 담겨있고 이를 view함수가 사용하는 것

* `return render(request, 'index.html')`



#### Templates

자동으로 Django가 만들어 주지 않는다.

Templates은 앱에 만든다.

```html
<!-- aricles/templates/index.html -->
<h1> 안녕하세요! </h1>
```

실제 내용을 보여주는 데 사용되는 파일

파일의 구조나 레이아웃을 정의한다. (HTML)

<u>**약속**</u>

Template 파일 경로의 기본 값은 **app 폴더 안의 templates 폴더**

`app/templates`



#### 추가 설정

```python
# settings.py

LANGUAGE_CODE = 'ko-kr'
TIME_ZONE = 'Asia/Seoul'
```

LANGUAGE_CODE

* 모든 사용자에게 제공되는 번역을 결정한다.
* 이 설정이 적용 되려면 **USE_I18N이 활성화**되어 있어야 한다.
* language-identifiers



TIME_ZONE

* 데이터베이스 연결의 시간대를 나타내는 문자열 지정
* USE_TZ가 True이고 이 옵션이 설정된 경우 데이터베이스에서 날짜 시간을 읽으면, UTC 대신 새로 설정한 시간대의 인식 날짜와 시간이 반환된다.
* **USE_TZ이 False인 상태로 이 값을 설정하는 것은 error가 발생**한다.
* List of tz database time zones



UTS_I18N

국제화 internationalization

* Django의 번역 시스템을 활성화해야 하는지 여부를 지정한다.



UTE_L10N

지역화 localization

* 데이터의 지역화 된 형식(localized formatting)을 기본적으로 활성화할지 여부를 지정한다.
* True일 경우, Django는 현재 local의 형식을 사용하여 숫자와 날짜를 표시한다.



USE_TZ

시간대 timezone

* datetimes가 기본적으로 시간대를 인식하는지 여부를 지정한다.
* True일 경우 Django는 내부적으로 시간대 인식 날짜 / 시간을 사용한다.



### Template

#### Django Template

'데이터 표현을 제어하는 도구이자 표현에 관련된 로직'

사용하는 built-in system

* Django template language



#### Django template language (DTL)

* Django template에서 사용하는 built-in template system
* 조건, 반복, 변수 치환, 필터 등의 기능을 제공한다.
* 단순희 Python이 html에 포함된 것이 아니며, 프로그래밍적 로직이 아니라 **프레젠테이션을 표현하기 위한 것**이다
* Python처럼 일부 프로그래밍 구조(if, for등)를 사용할 수 있지만, 이것은 해당 **Python 코드로 실행되는 것이 아니다.**



#### DTL Syntax

1. Variable
2. Filters
3. Tags
4. Comments

##### Variable

```django
{{ variable }}
```

* render()를 사용하여 views.py에서 정의한 변수를 <u>template파일로 넘겨 사용</u>하는 것이다.

  views.py

  `return render(request, 'greeting.html', {'name: 'Alice',})`

  greeting.html

  `<p>{{ name }}</p>`

  

  views.py

  변수가 늘어나면 함수 안에 info = {'name': 'Alice'} context = { 'info': info,} 추가후 

  `return render(request, 'greeting.html', context)`

  greeting.html

  `<p>{{ info.name }}</p>`

* 변수명은 영어, 숫자와 밑줄(_)의 조합으로 구성될 수 있으나 밑줄로는 시작할 수 없다.

  * 공백이나 구두점 문자 또한 사용할 수 없다.

* dot(.)를 사용하면 변수 속성에 접근할 수 있다.

  `{{ info.name }}` `{{ foods }}` `{{ foods.0 }}` `{{ dic.fruit }}`

* render()의 세번째 인자로 {'key': value}와 같이 딕셔너리 형태로 넘겨주며, 여기서 정의한 key에 해당하는 문자열이 template에서 사용 가능한 변수명이 된다.



#### Filters

```django
{{ variable|filter }}
```

표시할 변수를 수정할 때 사용한다

60개의 built-in template filters를 제공한다.

chained가 가능하며 일부 필터는 인자를 받기도 한다.



**예시**

name 변수를 모두 소문자로 출력

```django
{{ name|lower }}
```

pick의 길이를 출력

```django
{{ pick|length }}
```

join을 이용하여 , 로 이어서 출력

```django
{{ foods|join:', ' }}
```

인자를 받는 예시

```django
{{ variable|truncatewords:30 }}
```



##### Tags

```django
{% tag %}
```

출력 텍스트를 만들거나, 반복 또는 논리를 수행하여 제어 흐름을 만드는 등 변수보다 복잡한 일들을 수행한다.

일부 태그는 시작과 종료 태그가 필요하다.

```django
{% if %}

{% endif %}
```

약 24개의 built-in template tags를 제공한다.



예시)

```django
<p>메뉴판</p>
<ul>
    {% for food in foods %}
    	<li>{{ food }}</li>
   	{% endfor%}
</ul>
```



##### Comments

```django
{# 주석은 이렇게 #}
```

django template에서 라인의 주석을 표현하기 위해 사용한다.

아래처럼 유효하지 않은 템플릿 코드가 포함 될 수 있다.

```django
{# {% if %} text {% else %} #}
```

한 줄 주석에만 사용할 수 있다. (줄 바꿈이 허용되지 않는다.)

여러줄의 주석은 {% comment %}와 {% endcomment %} 사이에 입력한다.

```django
{% comment %}
	주석
	주석
{% endcomment %}
```



**예시** dtl_practice.html 3/2 6

forloop.counter The current iteration of the loop(1-indexed)



#### Template inheritance 템플릿 상속

템플릿 상속은 기본적으로 코드의 재사용성에 초점을 맞춘다.

템플릿 상속을 사용하면 사이트의 모든 공통 요소를 포함하고, 하위 템플릿이 재정의(override) 할 수 있는 블록을 정의하는 기본 <u>'skeleton' 템플릿</u>을 만들 수 있다.

유지보수를 위해 사용한다.

**base.html**

만약 bootstrap을 사용하고 싶다면 각 html에 CDN을 추가해주어야한다.



#### Template inheritance - "tags" 

상속을 위해 알아야하는 두개의 태그

```django
{%extends ''%}
```

자식(하위) 템플릿이 부모 템플릿을 확장한다는 것을 알린다.

반드시 템플릿 최상단에 작성 되어야 한다.

```django
{% block content %}
{% endblock content %} 혹은 {% endblock %}
```

하위 템플릿에서 재지정(override)할 수 있는 블록을 정의한다.

즉, 하위 템플릿이 채울 수 있는 공간이다.



templates 폴더 생성 후 base.html 생성

**app_name/templates 디렉토리 외 템플릿 추가 경로 설정**

```python
# settings.py
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

`'DIRS': [BASE_DIR / 'templates',]`

BASE_DIR : Django 프로젝트를 가지고 있는 최상단의 폴더

Python의 객체 지향적 경로를 작성하는 문법중 하나이다.

이렇게 쓰는 이유는 운영체제마다 경로시스템이 다르기 때문에 이렇게 작성하여 구동하는 운영체제에 맞춰 번역시키기 위해서이다.



**bootstrap 및 간단한 navbar 작성**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
  <title>Document</title>
</head>
<body>
  {% include '_nav.html' %}
  Above the block
  {% block content %}

  {% endblock content %}
  Under the block
  {% block haha %}

  {% endblock haha %}

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script>
</body>
</html>
```



**index.html 변경**

```html
{% extends 'base.html' %}

{%block content %}
  <div class="container">
    <p class="fw-bold">This is index!</p>
  </div>
  <p>This area is for something</p>
{% endblock content %}

{% block haha %}
  밑의 아이다!
{% endblock haha %}
```



#### Template Tag - "include"

```django
{% include '' %}
```

템플릿을 로드하고 현재 페이지로 렌더링한다.

템플릿 내에 다른 템플릿을 "포함(including)"하는 방법

include에 사용할 html에 _(underbar)를 사용하면 관리가 용이하다.

**articles>templates>_nav.html**

articles/templates/ 디렉토리에 _nav.html 생성 후 base.html에 있던 네비게이션 코드 가져오기

```html
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">Navbar</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a class="nav-link active" aria-current="page" href="#">Home</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Features</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```



**templates>base.html**

include tag를 통해 base.html에 _nav.html 포함시키기

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
  {% block style %}{% endblock style %}
  <title>Document</title>
</head>
<body>
  {% include 'articles/_nav.html' %}
  <div class="container">
    {% block content %}
    {% endblock %}
  </div>
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script>
</body>
</html>
```



#### Django template system (Django 설계 철학)

표현과 로직(view)을 분리

* 템플릿 시스템은 <u>표현을 제어하는 도구이자 표현에 관련된 로직일 뿐</u>이라고 생각한다.
* 즉, 템플릿 시스템은 이러한 기본 목표를 넘어서는 기능을 지원하지 말아야한다.

중복을 배제

* 대다수의 동적 웹사이트는 공통 header, footer, navbar같은 사이트 공통 디자인을 갖는다.
* Django 템프릿 시스템은 이러한 요소를 한 곳에 저장하기 쉽게 하여 중복 코드를 없애야 한다.
* 이것이 템플릿 상속의 기초가 되는 철학이다.