# Django 05

## REST API

### HTTP

HyperText Transfer Protocol

웹 상에서 컨텐츠를 전송하기 위한 약속

HTML 문서와 같은 리소스들을 가져올 수 있도록 하는 프로토콜(규칙, 약속)

웹에서 이루어지는 모든 데이터 교환의 기초

* 요청(request)
  * 클라이언트에 의해 전송되는 메세지
* 응답(response)
  * 서버에서 응답으로 전송되는 메세지

기본 특성

* Stateless
* Connectionless

쿠키와 세션을 토앻 서버 상태를 요청과 연결하도록 한다.



#### HTTP request methods

자원에 대한 행위(수행하고자 하는 동작)을 정의한다.

주어진 리소스(자원)에 수행하길 원하는 행동을 나타낸다.

HTTP Method

* GET(R, 조회)
* POST(C, 작성)
* PUT(U, 업데이트)
* DELETE(D, 삭제)



#### HTTP response status codes

특정 HTTP 요청이 성공적으로 완료되었는지 여부를 나타낸다.

응답은 5개의 그룹으로 나뉘어진다.

* **1xx** Informational responses
* **2xx** Successful response
* **3xx** Redirection messages
* **4xx** Client error responses
* **5xx** Server error responses



#### 웹에서의 리소스 식별

HTTP 요청의 대상을 리소스(resource, 자원)라고 한다.

리소스는 문서, 사진 또는 기타 어떤 것이든 될 수 있다.

각 리소스는 리소스 식별을 위해 HTTP 전체에서 사용되는 URI(Uniform Resource Identifier)로 식별된다.

* URL: 위치에 대한 정보
* URN: 별명
* path(URL, view. , URN)



#### URL, URN

**URL(Uniform Resource Locator)**

* 통합 자원 위치
* 네트워크 상에 자원이 어디 있는지 알려주기 위한 약속
* 과거에는 실제 자원의 위치를 나타냈지만 현재는 추상화된 의미론적인 구성이다.
* '웹 주소', '링크'라고도 불린다.

**URN(Uniform Resource Name)**

* 통합 자원의 이름
* URL과 달리 자원의 위치에 영향을 받지 않는 유일한 이름 역할을 한다.
* 예시 
  * ISBN(국제표준도서번호)



### URI

Uniform Resource Identifier

* 통합 자원 식별자
* 인터넷의 자원을 식별하는 유일한 주소 (정보의 자원을 포함한다.)
* 인터넷에서 자원을 식별하거나 이름을 지정하는데 사용되는 간단한 문자열
* 하위 개념
  * URL
  * URN

URI는 크게 URL과 URN으로 나눌 수 있지만, URN을 사용하는 비중이 매우 적기 때문에 일반적으로 URL은 URI와 같은 의미처럼 사용하기도 한다.



#### URI의 구조

**Scheme(protocol)**

브라우저가 사용해야하는 프로토콜

http(s), data, file, ftp, mailto

**https://**www.example.com:80/path/to/myfile.html/?key=value#quick-start



**Host(Domain name)**

요청을 받는 웹 서버의 이름

IP address를 직접 사용할 수도 있지만, 실 사용시 불편하므로 웹에서 자주 사용되지는 않는다.

(google의 IP address - 142.251.42142)

https://**www.example.com**:80/path/to/myfile.html/?key=value#quick-start



**Port**

웹 서버 상의 리소스에 접근하는데 사용되는 기술적인 '문(gate)'

HTTP 프로토콜의 표준 포트

* HTTP 80
* HTTP 443

https://www.example.com**:80**/path/to/myfile.html/?key=value#quick-start



**Path**

웹 서버 상의 리소스 경로

초기에는 실제 파일이 위치한 물리적인 위치를 나타냈지만, 오늘날은 물리적인 실제 위치가 아닌 추상화 형태의 구조로 표현한다.

https://www.example.com:80**/path/to/myfile.html**/?key=value#quick-start



**Query (Identifier)**

Query String Parameters

웹 서버에 제공되는 추가적인 매개 변수

&로 구분되는 key-value 목록

https://www.example.com:80/path/to/myfile.html/**?key=value**#quick-start



**Fragment**

Anchor

자원 안에서의 북마크의 한 종류를 나타낸다.

브라우저에게 해당 문서(HTML)의 특정 부분을 보여주기 위한 방법

브라우저에게 알려주는 요소이기 때문에 fragment identifier(부분 식별자)라고 부르며 '#' 뒤의 부분은 요청이 서버에 보내지지 않는다.

https://www.example.com:80/path/to/myfile.html/?key=value**#quick-start**



### RESTful API

### API

Application Programming Interface

프로그래밍 언어가 제공하는 기능을 수행할 수 있게 만든 인터페이스

* 애플리케이션과 프로그래밍으로 소통하는 방법
* CLI는 명령줄, GUI는 그래픽(아이콘), API는 프로그래밍을 통해 특정한 기능을 수행한다.

Web API

* 웹 애플리케이션 개발에서 다른 서비스에 요청을 보내고 응답을 받기 위해 정의된 명세
* 현재 웹 개발은 모든 것을 직접 개발하기 보다 여러 Open API를 활용하는 추세이다.

응답 데이터 타입

* HTML
* XML
* JSON 등

대표적인 API 서비스 목록

* Youtube API
* Naver Papago API
* Kakao Map API 등



#### REST

**RE**presentational **S**tate **T**ransfer

API Server를 개발하기 위한 일종의 소프트웨어 설계 방법론

* 2000년 로이 필딩의 박사학위 논문에서 처음으로 소개된 후 네트워킹 문화에 널리 퍼졌다.

네트워크 구조(Network Architecture) 원리의 모음

* 자원을 정의하고 자원에 대한 주소를 지정하는 전반적인 방법을 정한 방법론

REST 원리를 따르는 시스템을 RESTful이란 용어로 지칭한다.



자원을 정의하는 방법에 대한 고민

예) 정의된 자원을 어디에 위치시킬 것인가



REST의 자원과 주소의 지정 방법

1 자원

* URI

2 행위

* HTTP Method

3 표현

* 자원과 행위를 통해 궁극적으로 표현되는 (추상적인) 결과물
* JSON으로 표현된 데이터를 제공한다.



REST의 핵심 규칙

1 '정보'는 URI로 표현된다.

2 자원에 대한 '행위'는 HTTP Method로 표현 (GET, POST, PUT, DELETE)



설계 방법론은 지키지 않았을 때 잃는 것보다 지켰을 때 얻는 것이 훨씬 많다.

* 단, 설계 방법론을 지키지 않더라도 동작 여부에 큰 영향을 미치지는 않는다.



#### RESTful API

REST 원리를 따라 설계한 API

RESTful services, 혹은 simply REST services라고도 부른다.



프로그래밍을 통해 클라이언트의 요청에 JSON을 응답하는 서버를 구성한다.

* 지금까지 사용자의 입장에서 썼던 API를 제공자의 입장이 되어 개발해보기



#### JSON

JSON(JavaScript Object Notation)

* JSON is a lightweight data-interchange format
* JavaScript의 표기법을 따른 단순 문자열

특징

* 사람이 읽거나 쓰기 쉽고 기계가 파싱(해석, 분석)하고 만들어내기 쉽다.
* 파이썬의 dictionary, 자바스크립트의 object처럼 C계열의 언어가 갖고 있는 자료구조로 쉽게 변화할 수 있는 key-value 형태의 구조를 가지고 있다.



### Response

#### Init Project

제공된 00_json_response 프로젝트로 진행

가상환경 설정 및 패키지 설치

```bash
$ python -m venv venv
$ source venv/Scripts/activate
$ pip install -r requirements.txt
```



설치된 app 확인

```python
# settings.py

INSTALLED_APPS =[
    'articles',
    'django_seed'
]
```



작성된 url 확인

```python
# my_api/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/v1/', include('articles.urls')),
]
```

```python
from django.urls import path
from . import views

urlpatterns = [
    path('html/', views.article_html),
    path('json-1', views.article_json_1),
    path('json-2', views.article_json_2),
    path('json-3', views.article_json_3),
]
```



#### Create Dummy Data

작성된 model 확인

```python
# models.py

from django.db import models

class Article(models.Model):
    title = models.CharField(max_length=10)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```

django-seed 라이브러리를 사용해 모델 구조에 맞는 데이터 생성

```bash
$ python manage.py migrate
$ python manage.py seed articles --number=20
```



#### 1. Response - HTML

HTML을 응답하는 서버

```python
# articles/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('html/', views.article_html),
    path('json-1', views.article_json_1),
    path('json-2', views.article_json_2),
    path('json-3', views.article_json_3),
]
```

```python
# articles/views.py
from django.shortcuts import render
from .models import Article

def article_html(request):
    articles = Article.objects.all()
    context = {
        'articles': articles,
    }
    return render(request, 'articles/article.html', context)
```



HTML을 응답하는 서버

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <h1>Article List</h1>
  <hr> 
  <p>
    {% for article in articles %}
      <h2>{{ article.pk }}번 글. {{ article.title }}</h2>
      <p>{{ article.content }}</p>
      <hr>
    {% endfor%}
  </p>
</body>
</html>
```



#### 2. Response - JsonResponse

JsonResponse 객체를 활용한 JSON 데이터 응답

```python
# articles/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('json-1', views.article_json_1),
]
```

```python
# articles/views.py
from django.http.response import JsonResponse

def article_json_1(request):
    articles = Article.objects.all()
    articles_json = []

    for article in articles:
        articles_json.append(
            {
                'id': article.pk,
                'title': article.title,
                'content': article.content,
                'created_at': article.created_at,
                'updated_at': article.updated_at,
            }
        )
    return JsonResponse(articles_json, safe=False)
```



:heavy_check_mark: Dev Tools의 Content-Type: application/json

**Content-Type** entity header

* 데이터의 media type(MIME type, content type)을 나타내기 위해 사용된다.

* 응답 내에 있는 컨텐츠의 컨텐츠 유형이 실제로 무엇인지 클라이언트에게 알려준다.



**JsonResponse** objects

* JSON-encoded response를 만드는 HttpResponse의 서브 클래스
* "safe" parameter
  * True (기본값)
  * dict 이외의 객체를 직렬화(Serialization)하려면 False로 설정해야한다.

```python
# JSonResponse 예시
response = JsonResponse({'foo': 'bar'})
response = JsonResponse([1,2,3], safe=False)
```

safe=False 첫번째들어온 인자가 딕셔너리가 아니면 safe=False를 해야 JSON으로 변환된다.



#### Serialization

"직렬화"

데이터 구조나 객체 상태를 동일하거나 다른 컴퓨터 환경에 저장하고, 나중에 재구성할 수 있는 포맷으로 변환하는 과정

Serializers in Django

* Queryset 및 Model Instance와 같은 복잡한 데이터를 JSON, XML 등의 유형으로 쉽게 변환할 수 있는 Python 데이터 타입으로 만들어 준다.

```python
def serialize(format, queryset, **options):
    """
    Serialize a queryset (or any iterator that returns database objects) using
    a certain serializer.
    """
    s = get_serializer(format)()
    s.serialize(queryset, **options)
    return s.getvalue()
```



#### 3. Response - Django Serializer

Django의 내장 HttpResponse를 활용한 JSON 응답

```python
# articles/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('json-2', views.article_json_2),
]
```



Django의 내장 HttpResponse를 활용한 JSON 응답 객체

주어진 모델 정보를 활용하기 때문에 이전과 달리 필드를 개별적으로 직접 만들어줄 필요가 없다.

```python
from django.http.response import JsonResponse, HttpResponse
from django.core import serializers

def article_json_2(request):
    articles = Article.objects.all()
    data = serializers.serialize('json', articles)
    return HttpResponse(data, content_type='application/json')
```



#### 4. Response - Django REST Framework

Django REST framework(DRF) 라이브러리를 사용한 JSON 응답

설치 과정 확인 (requirement.txt에 미리 작성되어 있다.)

```bash
$ pip install djangorestframework
```

```python
# settings.py

INSTALLED_APPS = [
    'rest_framework',
]
```



DRF 라이브러리를 사용한 JSON 응답 url 확인

```python
# articles/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('json-3', views.article_json_3),
]
```



Article 모델에 맞춰 자동으로 필드를 생성해 serialize해주는 ModelSerializer 확인

```python
# articles/serializers.py
from rest_framework import serializers
from .models import Article

class ArticleSerializer(serializers.ModelSerializer):

    class Meta:
        model = Article
        fields = '__all__'
```



DRF의 Response()를 활용해 Serialize된 JSON 객체 응답

(DRF를 이용한 view함수 작성은 다음 챕터에서 진행한다.)

```python
from rest_framework.decorators import api_view
from rest_framework.response import Response
from .serializers import ArticleSerializer

@api_view()
def article_json_3(request):
    articles = Article.objects.all()
    serializer = ArticleSerializer(articles, many=True)
    return Response(serializer.data)
```

:heavy_check_mark: @api_view() 필수이다.

:heavy_check_mark: DRF 라이브러리를 사용한 JSON 응답 확인



python 파일을 통해 직접 요청을 보낸 후 응답 확인해보기

(requests 라이브러리를 활용) -> 설치가 필요하다.

:heavy_check_mark: API DATA 제공자가 우리이다. templates를 작성하지 않는다. RESTful django server를 만든다.

```python 
import requests
form pprint import pprint

response = requests.get('http://127.0.01:8000/api/v1/json-3/')
pprint(response.json())
```



#### Django REST Framework (DRF)

Web API 구축을 위한 강력한 Toolkit을 제공하는 라이브러리

DRF의 Serializer는 Django의 Form 및 ModelForm 클래스와 매우 유사하게 구성되고 작동한다.



Web API

웹 애플리케이션 개발에서 다른 서비스에 요청을 보내고 응답을 받기 위해 정의된 명세



#### Django ModelForm vs. DRF Serializer

|          |  Django   |    DRF     |
| :------: | :-------: | :--------: |
| Response |   HTML    |    JSON    |
|  Model   | ModelForm | Serializer |



### Single Model

#### DRF with Single Model

단일 모델의 data를 직렬화(serialization)하여 JSON으로 변환하는 방법에 대한 학습

단일 모델을 두고 CRUD 로직을 수행 가능하도록 설계

API 개발을 위한 핵심 기능을 제공하는 도구 활용

* DRF built-in form
* Postman



#### [참고] Postman

API를 구축하고 사용하기 위해 여러 도구를 제공하는 API 플랫폼

설계, 테스트, 문서화 등의 도구를 제공함으로써 API를 더 빠르게 개발 및 생성할 수 있도록 돕는다.



#### Init Project

제공된 01_drf 프로젝트로 진행

가상환경 설정 및 패키지 설정

```bash
$ python -m venv venv
$ source ven/Scripts/activate

$ pip install -r requirements.txt
```



설치된 app 확인

```python
# settings.py

INSTALLED_APPS = [
    'articles',
    'django_seed',
    'django_extensions',
    'rest_framework'
]
```



작성된 url 확인

```python
# my_api/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/v1/', include('articles.urls')),
]
```

```python
# articles/urls.py
from django.urls import path
from . import views

urlpatterns = [

]
```



작성된 model 확인

```python
# models.py
from django.db import models

class Article(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```



#### Create Dummy Data

django-seed 라이브러리를 사용해 모델 구조에 맞는 데이터 생성

```bash
$ python manage.py migrate
$ python manage.py seed articles --number=20
```



#### ModelSerializer

모델 필드에 해당하는 필드가 있는 Serializer 클래스를 자동으로 만들 수 있는 shortcut

아래 핵심 기능을 제공

1. 모델 정보에 맞춰 자동으로 필드 생성
2. serializer에 대한 유효성 검사기를 자동으로 생성
3. .create() & .update()의 간단한 기본 구현이 포함된다.



Model의 필드를 어떻게 '직렬화'할 지 설정하는 것이 핵심이다.

이 과정은 Django에서 Model의 필드를 설정하는 것과 동일하다.

```python
# articles/serializers.py
from rest_framework import serializers
from .models import Article

class ArticleSerializer(serializers.ModelSerializer):

    class Meta:
        model = Article
        fields = ('id', 'title',)
```



#### Serializer in Shell

shell_plus에서 serializer 사용해보기

```bash
#1. shell_plus 실행
$ python manage.py shell_plus

#2. 작성한 Serializer import
>>> from articles.serializers import ArticleListSerializer

#3. 기본 인스턴스 구조 확인
>>> serializer = ArticleListSerializer()
>>> serializer
ArticleListSerializer():
	id = IntegerField(label='ID', read_only=True)
	title = CharField(max_length=100)
	
#4. Model instance 객체
>>> article = Article.objects.get(pk=1)
>>> article
<Article: Article object (1)>

>>> serializer = ArticleListSerializer(article)
>>> serializer
ArticleListSerializer(<Article: Article object (1)>):
	id = IntegerField(label='ID', read_only=True)
	title = CharField(max_length=100)
>>> serializer.data
{'id': 1, 'title': 'Site economic if two country science.'}

#5. QuerySet 객체
>>> article = Article.objects.all()

#5-1. many=True 옵션 x
>>> serializer = ArticleListSerializer(articles)
>>> serializer.data
AttributeError

#5-2. many=True 옵션 o
>>> serializer = ArticleListSerializer(articles, many=True)
>>> serializer.data
[OrderedDict([('id', 1), ('title','Live left research.'), ('content', 'Small') ...])]
```



#### 'many' argument

**many=True**

* "Serializing multiple objects"
* 단일 인스턴스 대신 QuerySet 등을 직렬화하기 위해서는 serializer를 인스턴스화 할 때 many=True를 키워드 인자로전달해야한다.

```python
@api_view(['GET'])
def comment_list(request):
    comments = get_list_or_404(Comment)
    serializer = CommentSerializer(comments, many=True)
    return Response(serializer.data)
```

```python
qeryset = Book.objects.all()
serializer = BookSerializer(queryset, many=True)
print(serializer.data)
```



#### Build RESTful API

|             |     GET      |  POST   |     PUT     |   DELETE    |
| :---------: | :----------: | :-----: | :---------: | :---------: |
|  articles/  | 전체 글 조회 | 글 작성 |             |             |
| articles/1/ | 1번 글 조회  |         | 1번 글 수정 | 1번 글 삭제 |



#### 1. GET - Article List

url 및 view 함수 작성

```python
# articles/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('articles/', views.article_list),
]
```

```python
# articles/view.py

from rest_framework.response import Response
from rest_framework.decorators import api_view
from django.shortcuts import render, get_list_or_404
from .models import Article
from .serializers import ArticleListSerializer

@api_view(['GET'])
def article_list(request):
    if request.method == 'GET':
        # articles = Article.objects.all()
        articles = get_list_or_404(Article)
        serializer = ArticleListSerializer(articles, many=True)
        return Response(serializer.data)
```



**api_view** decorator

* 기본적으로 GET 메서드만 허용되며 다른 메서드 요청에 대해서는 405 Method Not Allowed로 응답
* View 함수가 응답해야하는 HTTP 메서드의 목록을 리스트의 인자로 받는다.
* DRF에서는 선택이 아닌 **필수적으로 작성**해야 해당 view함수가 정상적으로 동작한다.

http://127.0.0.1:8000/api/v1/articles/로 GET 요청 후 응답 확인



#### 2. GET - Article Detail

Article List와 Article Detail을 구분하기 위해 추가 Serializer을 정의한다.

모든 필드를 직렬화하기 위해 fields 옵션을 `__all__`로 설정한다.

```python
# articles/serializers.py

class ArticleSerializer(serializers.ModelSerializer):
    class Meta:
        model = Article
        fields = '__all__'
```

url 및 view함수 작성

```python
# articles/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('articles/<int:article_pk>/', views.article_detail),
]
```

```python
# articles/views.py

from django.shortcuts import get_object_or_404
from .serializers import ArticleSerializer 

@api_view(['GET', 'DELETE', 'PUT'])
def article_detail(request, article_pk):
    article = get_object_or_404(Article, pk=article_pk)

    if request.method == 'GET':
        serializer = ArticleSerializer(article)
        return Response(serializer.data)
```

http://127.0.0.1:8000/api/v1/articles/1/로 GET 요청 후 응답 확인



#### 3. POST - Create Article

201 Created 상태 코드 및 메시지 응답

RESTful 구조에 맞게 작성

1. URI는 자원을 표현한다.
2. 자원을 조작하는 행위는 HTTP Method

article_list 함수로 게시글을 조회하거나 생성하는 행위를 모두 처리 가능하다.



view 함수 수정

```python
# articles/views.py

from rest_framework import status
from rest_framework.response import Response
from rest_framework.decorators import api_view
from django.shortcuts import get_list_or_404, get_object_or_404
from .serializers import ArticleListSerializer, ArticleSerializer, 
from .models import Article

@api_view(['GET', 'POST'])
def article_list(request):
    if request.method == 'GET':
        articles = get_list_or_404(Article)
        serializer = ArticleListSerializer(articles, many=True)
        return Response(serializer.data)

    elif request.method == 'POST':
        serializer = ArticleSerializer(data=request.data)
        if serializer.is_valid(raise_exception=True):
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
```



#### Status Codes in DRF

DRF에는 status code를 보다 명확하고 읽기 쉽게 만드는 데 사용할 수 있는 정의된 상수 집합을 제공한다.

**status** 모듈에 HTTP status code집합이 모두 포함되어 있다.

단순히 status=201 같은 표현으로도 사용할 수 있지만 DRF는 권하지 않는다.

예) ```Response(serializer.data, status=201)`



HTTP body에 form-data로 title과 content 데이터를 작성한다.

http://127.0.0.1:8000/api/v1/articles/로 POST 요청 후 응답 확인



#### 'raise_exception' argument

"Raising and exception on invalid data"

is_valid()는 유효성 검사 오류가 있는 경우 `serializer.ValidationError` 예외를 발생시키는 선택적 raise_exception 인자를 사용할 수 있다.

DRF에서 제공하는 기본 예외 처리기에 의해 자동으로 처리되며, 기본적으로 HTTP status code 400을 응답으로 반환한다.



raise_exception 작성

```python
# articles/views.py

from rest_framework import status
from rest_framework.response import Response
from rest_framework.decorators import api_view
from django.shortcuts import get_list_or_404, get_object_or_404
from .serializers import ArticleListSerializer, ArticleSerializer, CommentSerializer
from .models import Article, Comment
from articles import serializers

# Create your views here.
# @api_view()
@api_view(['GET', 'POST'])
def article_list(request):
    if request.method == 'GET':
        articles = get_list_or_404(Article)
        serializer = ArticleListSerializer(articles, many=True)
        return Response(serializer.data)

    elif request.method == 'POST':
        serializer = ArticleSerializer(data=request.data)
        # Return a 400 response if the data was invalid.
        if serializer.is_valid(raise_exception=True):
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
```



#### 4. DELETE - Delete Article

204 No Content 상태 코드 및 메시지 응답

article_detail 함수로 상세 게시글을 조회하거나 삭제하는 행위 모두 처리 가능하다.

```python
# articles/views.py

from rest_framework import status
from rest_framework.response import Response
from rest_framework.decorators import api_view
from django.shortcuts import get_object_or_404
from .serializers import ArticleSerializer
from .models import Article

@api_view(['GET', 'DELETE'])
def article_detail(request, article_pk):
    article = get_object_or_404(Article, pk=article_pk)

    if request.method == 'GET':
        serializer = ArticleSerializer(article)
        return Response(serializer.data)

    elif request.method == 'DELETE':
        article.delete()
        data = {
            'delete': f'데이터 {article_pk}번이 삭제되었습니다.',
        }
        return Response(data, status=status.HTTP_204_NO_CONTENT)
```

http://127.0.0.1:8000/api/v1/articles/1/로 DELETE 요청 후 응답 확인



#### 5. PUT - Update Article

article_detail 함수로 상세 게시글을 조회하거나 삭제, 수정하는 행위 모두 처리 가능

```python
# articles/views.py
from rest_framework import status
from rest_framework.response import Response
from rest_framework.decorators import api_view
from django.shortcuts import get_object_or_404
from .serializers import ArticleSerializer
from .models import Article

@api_view(['GET', 'DELETE', 'PUT'])
def comment_detail(request, comment_pk):
    comment = get_object_or_404(Comment, pk=comment_pk)
    
    if request.method == 'GET':
        serializer = CommentSerializer(comment)
        return Response(serializer.data) 

    elif request.method == 'DELETE':
        comment.delete()
        data = {
            'delete': f'데이터 {comment_pk}번이 삭제되었습니다.',
        }
        return Response(data, status=status.HTTP_204_NO_CONTENT)

    elif request.method == 'PUT':
        serializer = CommentSerializer(comment, request.data)
        if serializer.is_valid(raise_exception=True):
            serializer.save()
            return Response(serializer.data)
```



HTTP body에 form-data로 title과 content 수정 데이터 작성

http://127.0.0.1:8000/api/v1/articles/1/로 PUT 요청 후 응답 확인



### 1:N Relation

#### DRF with 1:N Relation

1:N 관계에서의 모델 data를 직렬화(serialization)하여 JSON으로 변환하는 방법에 대한 학습

2개 이상의 1:N 관계를 맺는 모델을 두고 CRUD 로직을 수행 가능하도록 설계하기



데이터 베이스 초기화 후 Comment 모델 작성

```python
# articles/models.py
from django.db import models

class Comment(models.Model):
    article = models.ForeignKey(Article, on_delete=models.CASCADE)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```



마이그레이션 작업 후 data seed 진행

```bash
$ python manage.py makemigrations
$ python manage.py migrate
$ python manage.py seed articles --number=20
```



#### 1. GET - Comment List

CommentSerializer 작성

```python
# articles/serializers.py

class CommentSerializer(serializers.ModelSerializer):

    class Meta:
        model = Comment
        fields = '__all__'
```



url 작성 및 comment_list 함수 정의

```python
# articles/urls.py
from django.urls import path
from . import views

urlpatterns = [

    path('comments/', views.comment_list),
]
```

```python
# articles/views.py
from rest_framework import status
from rest_framework.response import Response
from rest_framework.decorators import api_view
from django.shortcuts import get_list_or_404
from .serializers import CommentSerializer
from .models import Comment

@api_view(['GET'])
def comment_list(request):
    comments = get_list_or_404(Comment)
    serializer = CommentSerializer(comments, many=True)
    return Response(serializer.data)
```

http://127.0.0.1:8000/api/v1/comments/로 GET 요청 후 응답 확인



#### 2. GET - Comment Detail

url 작성 및 comment_detail 함수 정의

```python
from django.urls import path
from . import views

urlpatterns = [
    path('comments/<int:comment_pk>/', views.comment_detail),
]
```

```python
# articles/views.py
from rest_framework.response import Response
from rest_framework.decorators import api_view
from django.shortcuts import get_object_or_404
from .models import Comment

@api_view(['GET'])
def comment_detail(request, comment_pk):
    comment = get_object_or_404(Comment, pk=comment_pk)
    
    if request.method == 'GET':
        serializer = CommentSerializer(comment)
        return Response(serializer.data) 
```



http://127.0.0.1:8000/api/v1/comments/1/로 GET 요청 후 응답 확인



#### 3. POST - Create Comment

url 및 comment_create 함수 작성

```python
# articles/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('comments/<int:comment_pk>/', views.comment_detail),
]
```

```python
# articles/views.py
from rest_framework import status
from rest_framework.response import Response
from rest_framework.decorators import api_view
from django.shortcuts import get_object_or_404
from .serializers import CommentSerializer
from .models import Article

@api_view(['POST'])
def comment_create(request, article_pk):
    article = get_object_or_404(Article, pk=article_pk)
    serializer = CommentSerializer(data=request.data)
    if serializer.is_valid(raise_exception=True):
        serializer.save()
        return Response(serializer.data, status=status.HTTP_201_CREATED)
```



http://127.0.0.1:8000/api/v1/articles/1/comments/로 POST 요청 후 응답 확인



Article 생성과 달리 Comment 생성은 생성 시에 참조하는 모델의 객체 정보가 필요하다.

1: N 관계에서 N은 어떤 1을 참조하는지에 대한 정보가 필요하기 때문이다.(외래키)

```
IntegrityError at /api/v1/articles/1/comments/
NOT NULL constraint failed: artiicles_comment.article_id
```



#### Passing Additional attributes to .save()

.save() 메서드는 특정 Serializer 인스턴스를 저장하는 과정에서 추가적인 데이터를 받을 수 있다.

* 인스턴스를 저장하는 시점에 추가 데이터 삽입이 필요한 경우

```python
# articles/views.py
from rest_framework import status
from rest_framework.response import Response
from rest_framework.decorators import api_view
from django.shortcuts import get_object_or_404
from .serializers import CommentSerializer
from .models import Article

@api_view(['POST'])
def comment_create(request, article_pk):
    article = get_object_or_404(Article, pk=article_pk)
    serializer = CommentSerializer(data=request.data)
    if serializer.is_valid(raise_exception=True):
        serializer.save(article=article)
        return Response(serializer.data, status=status.HTTP_201_CREATED)
```



http://127.0.0.1:8000/api/v1/articles/1/comments/로 POST 요청 재시도

article 필드에 대해 "이 필드는 필수 항목입니다." 라는 응답을 수신한다.



#### Read Only Field (읽기 전용 필드)

어떤 게시글에 작성하는 댓글인지에 대한 정보를 form-data로 넘겨주지 않았기 때문에 직렬화하는 과정에서 article 필드가 유효성 검사(is_valid)를 통과하지 못한다.

* CommentSerializer에서 article field에 해당하는 데이터 또한 요청으로부터 받아서 직렬화하는 것으로 설정되었기 때문이다.

이때는 읽기 전용 필드(read_only_fields) 설정을 통해 직렬화하지 않고 반환 값에만 해당 필드가 포함되도록 설정할 수 있다.

```python 
# articles/serializers.py

class CommentSerializer(serializers.ModelSerializer):

    class Meta:
        model = Comment
        fields = '__all__'
        read_only_fields = ('article',)
```



http://127.0.0.1:8000/api/v1/articles/1/comments/로 POST 요청 재시도



#### 4. DELETE & PUT - delete, update Comment

Article 생성 로직에서와 마찬가지로 comment_detail함수가 모두 처리할 수 있도록 작성한다.

```python
from rest_framework import status
from rest_framework.response import Response
from rest_framework.decorators import api_view
from django.shortcuts import get_object_or_404
from .serializers import CommentSerializer
from .models import Comment

@api_view(['GET', 'DELETE', 'PUT'])
def comment_detail(request, comment_pk):
    comment = get_object_or_404(Comment, pk=comment_pk)
    
    if request.method == 'GET':
        serializer = CommentSerializer(comment)
        return Response(serializer.data) 

    elif request.method == 'DELETE':
        comment.delete()
        data = {
            'delete': f'데이터 {comment_pk}번이 삭제되었습니다.',
        }
        return Response(data, status=status.HTTP_204_NO_CONTENT)

    elif request.method == 'PUT':
        serializer = CommentSerializer(comment, request.data)
        if serializer.is_valid(raise_exception=True):
            serializer.save()
            return Response(serializer.data)
```



http://127.0.0.1:8000/api/v1/comments/2/로 DELETE 요청 후 응답 확인

http://127.0.0.1:8000/api/v1/comments/3/로 PUT 요청 후 응답 확인



#### 1:N Serializer

1 특정 게시글에 작성된 댓글 목록 출력하기

* 기존 필드 override

2 특정 게시글에 작성된 댓글의 개수 구하기

* 새로운 필드 추가



### 1. 특정 게시글에 작성된 댓글 목록 출력하기

Serializer는 기존 필드를 override하거나 추가 필드를 구성할 수 있다.

우리가 작성한 로직에서는 크게 2가지 형태로 구성할 수 있다.

1. PrimaryKeyRelatedField (댓글에 대한 번호만 출력할 것이다.)
2. Nested relationships (댓글을 다 출력할 것이다.)



case1) **PrimaryKeyRelatedField**

* pk를 사용하여 관계된 대상을 나타내는 데 사용할 수 있다.
* 필드가 to many relationships(N)를 나타내는데 사용되는 경우 many=True 속성이 필요하다.
* comment_set 필드 값을 form-data로 받지 않으므로 read-only=True 설정 필요

```python
# articles/serializers.py

class ArticleSerializer(serializers.ModelSerializer):
    comment_set = serializers.PrimaryKeyRelatedField(many=True, read_only=True)

    class Meta:
        model = Article
        fields = '__all__'
```



many=True는 comment가 N이기 때문

read_only=True는 조회만 되어야하기 때문



[참고] 역참조 시 생성되는 comment_set을 다른 매니저 이름으로 override할 수 있다.

* 단, 다음과 같이 수정할 경우 이전 serializers.py에서의 클래스 변수명도 일치하도록 수정해야한다.

```python
# articles/models.py

class Comment(models.Model):
    article = models.ForeignKey(Article, on_delete=models.CASADE, related_name='comments')
```



http://127.0.0.1:8000/api/v1/articles/1/로 GET 요청 후 응답 확인



case2) Nested relationships

* 모델 관계상으로 참조된 대상은 참조하는 대상의 표현(응답)에 포함되거나 중첩(nested)될 수 있다.
* 이러한 중첩된 관계는 serializers를 필드로 사용하여 표현할 수 있다.
* 두 클래스의 상하위치를 변경한다.

```python
# articles/serializers.py
# articles/serializers.py

class CommentSerializer(serializers.ModelSerializer):

    class Meta:
        model = Comment
        fields = '__all__'
        read_only_fields = ('article',)
        
class ArticleSerializer(serializers.ModelSerializer):
    comment_set = serializers.PrimaryKeyRelatedField(many=True, read_only=True)

    class Meta:
        model = Article
        fields = '__all__'
```



http://127.0.0.1:8000/api/v1/articles/1/로 GET 요청 후 응답 확인



comment_set 매니저는 모델 관계로 인해 자동으로 구성되기 때문에 커스텀 필드를 구성하지 않아도 comment_set이라는 필드명을 fields 옵션에 작성만 해도 사용할 수 있었다.

하지만 지금처럼 별도의 값을 위한 필드를 사용하려는 경우 자동으로 구성되는 매니저가 아니기 때문에 직접 필드를 작성해야한다.

```python
# articles/serializers.py
class ArticleSerializer(serializers.ModelSerializer):
    comment_set = CommentSerializer(many=True, read_only=True)
    comment_count = serializers.IntegerField(source='comment_set.count', read_only=True)

    class Meta:
        model = Article
        fields = '__all__'
```



**source** arguments

필드를 채우는 데 사용할 속성의 이름

점 표기법(dot notation)을 사용하여 속성을 탐색할 수 있다.

comment_set이라는 필드에 .(dot)을 통해 전체 댓글의 개수를 확인 가능하다.

.count()는 built-in Queryset API 중 하나이다.



http://127.0.0.1:8000/api/v1/articles/1/로 GET 요청 후 응답 확인



#### [주의 사항] 'read_only_fields' shortcut issue

특정 필드를 override 혹은 추가한 경우 read_only_fields shortcut으로 사용할 수 없다.



:heavy_check_mark:

form을 대체하는 것이 serializer이다.

serializer를 사용하는 이유: msa(마이크로 서비스 아키텍처)



**기억해 둘 status code**

100 continue

200 OK

201 Created

204 No Content

301 Moved Permanently

400 Bad Request 

401 Unauthorized

403 Forbidden

404 No found

500 Internal Server Error

501 Not Implemented
