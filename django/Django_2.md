# Django 2



### HTML Form

#### HTML "form" element

웹에서 사용자 정보를 입력하는 여러 방식(text, button, checkbox, file, hidden, image, password, radio, reset, submit)을 제공하고, 사용자로부터 할당된 데이터를 서버로 전송하는 역할을 담당한다.

핵심 속성(attribute)

* **action**: 입력 데이터가 전송도리 URL 지정
* **method**: 입력 데이터 전달 방식 지정
  * GET(조회), POST(서버를 건드릴 수 있다.)
  * GET이 default이며 POST를 주로 사용할 것



#### HTML "input" element

사용자로부터 데이터를 입력 받기 위해 사용한다.

type 속성에 따라 동작 방식이 달라진다.

핵심 속성(attribute)

* **name** 
  * 중요 - key : value의 형태로 데이터가 전달된다. key가 name
* 중복 가능, 양식을 제출했을 때 name이라는 이름에 설정된 값을 넘겨서 값을 가져올 수 있다.
* 주요 용도는 GET/POST 방식으로 서버에 전달하는 파라미터(name은 key, value는 value)로 **?key=value&key=value**형태로 전달 된다.



#### HTML "label" element

사용자 인터페이스 항목에 대한 설명(caption)을 나타낸다.

label을 input 요소와 연결하기

1. input에 id 속성을 부여한다.
2. label에는 input의 id와 동일한 값의 for 속성이 필요하다.

label과 input 요소 연결의 주요 이점

* 시각적인 기능 뿐만 아니라 화면 리더기에서 label을 읽어서 사용자가 입력해야 하는 텍스트가 무엇인지 더 쉽게 이해할 수 있도록 돕는 프로그래밍적 이점도 있다.
* label을 클릭해서 input에 초점(focus)를 맞추거나 활성화(activate) 시킬 수 있다.



#### HTML "for" attribute

for 속성의 값과 일치하는 id를 가진 문서의 첫 번째 요소를 제어한다.

* 연결된 요소가 labelable elements인 경우 이 요소에 대한 labeled control이 된다.



"labelable elements"

* label 요소와 연결할 수 있는 요소
* button, input(not hidden type), select, textarea ..



#### HTML "id" attribute

전체 문서에서 고유(must unique)해야하는 식별자를 정의한다.

사용 목적

* liking, scripting, styling 시 요소를 식별한다.



#### HTTP

HyperText Transfer Protocol

웹에서 이루어지는 모든 데이터 교환의 기초

주어진 리소스가 수행할 원하는 작업을 나타내는 request methods를 정의한다.

HTTP request method 종류 (요청의 종류)

* GET, POST, PUT, DELETE



#### HTTP request method - "GET"

서버로 부터 **정보를 조회**하는 데 사용한다.

데이터를 가져올 때만 사용해야한다.

데이터를 서버로 전송할 때 body가 아닌 Query String Parameters를 통해 전송한다. (POST방식에서는 body에다 담겨서 전송된다.)

우리는 서버에 요청을 하면 HTML문서 파일 한 장을 받는데, 이때 사용하는 요청의 방식이 GET이다.

##### Throw & Catch

**Throw**

```python
# project > urls.py
urlpatterns = [
    # path('주소/', view 함수)
    path('throw/', views.throw),
]
```

```python
# app > views.py
def throw(request):
    return render(request, 'throw.html')
```

``` html
<!-- throw.html -->
{% extends 'base.html' %}

{% block content %}
  <h1>Throw</h1>
  <form action="/catch/" method="#">
    <label for="message">Throw</label>
    <input type="text" id="message" name="message">
    <input type="submit">
  </form>
{% endblock content %}
```



**Catch**

**Throw**

```python
# project > urls.py
urlpatterns = [
    # path('주소/', view 함수)
    path('catch/', views.catch),
]
```

```python
# app > views.py
def catch(request):
    return render(request, 'catch.html')
```

``` html
<!-- catch.html -->
{% extends 'base.html' %}

{% block content %}
  <h1>Catch</h1>
  <form action="#" method="#">
    <h1>Catch</h1>
    <p>{{ message }}</p>
    <a href="/throw/">Back</a>
  </form>
{% endblock content %}
```



### URL

#### Django URLs

Dispatcher(발송자, 운항 관리자)로서의 URL

웹 애플리케이션은 URL을 통한 클라이언트의 요청에서부터 시작된다.



#### Variable Routing

URL 주소를 변수로 사용하는 것

URL의 일부를 변수로 지정하여 view 함수의 인자로 넘길 수 있다.

즉, 변수 값에 따라 하나의 path()에 여러 페이지를 연결 시킬 수 있다.

사용 예시

* path('accounts/user/\<int:user_pk>',...)
  * account/user/1 -> 1번 user 관련 페이지
  * account/user/2 -> 2번 user 관련 페이지

```python
# project> urls.py

urlpatterns = [
    path('hello/<str:name>/', views.hello),
]
```

```python
# app> views.py

def hello(request, name):
    
    return render(request, 'hello.html')
```

```html
# hello.html

{% extends 'base.html' %}

{% block content %}
  <h1> 만나서 반가워요 {{ name }}</h1>
{% endblock %}
```



#### URL Path converters

**str**

'/'를 제외하고 비어 있지 않은 모든 문자열과 매치

작성하지 않을 경우 기본 값

**int**

0 또는 양의 정수와 매치

**slug**

ASCII 문자 또는 숫자, 하이픈 및 밑줄 문자로 구성된 모든 슬러그 문자열과 매치

예) 'building-your-1st-django-site'

**uuid**

**path**



#### App URL mapping

app의 view 함수가 많아지면서 사용하는 path()또한 많아지고, app또한 더 많이 작성되기 때문에 프로젝트의 urls.py에서 모두 관리하는 것은 프로젝트 유지보수에 좋지 않다.

이제 **각 app에 urls.py를 작성** + include를 활용

각각의 앱 안에 urls.py을 생성하고 프로젝트 urls.py에서 각 앱의 urls.py파일로 URL mapping을 위탁한다.

urlpatterns은 어제든지 다른 URLconf 모듈을 include할 수 있다.



**include()**

* 다른 URLconfig(app1/urls.py)들을 참조할 수 있도록 돕는다.
* 함수 include()를 만나게 되면, URL의 그 시점까지 일치하는 부분을 잘라내고, 남은 문자열 부분의 후속 처리를 위해 include된 URLconf로 전달한다.
* **django는 명시적 상대경로(from .module import ..)를 권장한다.**

<원래 project의 urls.py>

```python
from django.contrib import admin
from django.urls import path
from articles import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('index/', views.index),
    path('greeting/', views.greeting),
    path('dinner/', views.dinner),
    path('dtl-practice/', views.dtl_practice),
    path('throw/', views.throw),
    path('catch/', views.catch),
    path('hello/<str:name>/', views.hello),
]
```

<project의 urls.py>

```python
from django.contrib import admin
from django.urls import path, include
from articles import views

urlpatterns = [
    path('admin/', admin.site.urls),
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

```html
# throw.html
<form action="/catch/" method="#"></form>
<from action="/articles/catch/" method="#"></from>

# catch.html
<a href="/throw/">Back</a>
<a href="articles/throw/">Back</a>
```



#### Naming URL patterns

이제는 링크에 url을 직접 작성하는 것이 아니라 path()함수의 name 인자를 정의해서 사용한다.

Django Template Tag 중 하나인 url 태그를 사용해서 path() 함수에 작성한 name을 사용할 수 있다.

<u>url 설정에 정의 된 특정 경로들의 의존성을 제거</u>할 수 있다.

```python
urlpatterns = [
    path('index/', views.index, name='index'),
]
```

```html
<a href="{% url 'index' %}">메인 페이지</a>
```



예시)

app > views.py

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

app>templates>throw.html

```html
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

app>templates>catch.html

```html
{% extends 'base.html' %}

{% block content %}
  <h1>Catch</h1>
  <h2>{{message}}를 받았다!</h2>
  <a href="{% url 'throw' %}">다시 던질게</a>
{% endblock content %}
```



#### url template tag

The 'name' value as called by the {% url %} template tag

`{% url '' %}`

주어진 url 패턴 이름 및 선택적 매개 변수와 일치하는 절대 경로 주소를 반환한다.

템플리셍 URL을 하드 코딩하지 않고도 DRY 원칙을 위반하지 않으면서 링크를 출력하는 방법이다.



### Framework의 성격

<u>**Opinionated 독선적**</u> : Django

Unopinionated 관용적
