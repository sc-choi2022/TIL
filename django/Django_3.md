# Django 3



### Namespace

#### 2가지 문제 발생

1. articles 앱의 index 페이지에서 두번째 앱 pages의 index로 이동하는 하이퍼링크를 클릭 시 현재 페이지로 이동된다.
   * URL namespace
2. pages 앱 index url로 이동해도 articles 앱의 index 페이지가 출력된다.
   * Template namespace



#### namespace

객체를 구분할 수 있는 범위를 나타내는 말로 일반적으로 하나의 이름 공간에서는 하나의 이름이 단 하나의 객체만을 가리키게 된다.

프로그래밍을 하다 보면 모든 변수명과 함수명 등 이들 모두를 겹치지 않게 정의하는 것은 어려운 일이다.

그래서 django에서는 

1. 서로 다른 app의 같은 이름을 가진 url name은 이름공간을 설정해서 구분한다.
2. templates, static 등 django는 정해진 경로 하나로 모아서 보기 때문에 <u>중간에 폴더를 임의로 만들어 줌으로써 이름공간을 설정</u>한다.



#### URL namespace

URL namespace를 사용하면 서로 다른 앱에서 동일한 URL 이름을 사용하는 경우에도 이름이 지정된 URL을 고유하게 사용할 수 있다.

urls.py에 **''app_name''** attribute 값을 작성한다.

**어떤 앱의 url인지 작성하겠다.**



##### 참조

':' 연산자를 사용하여 지정

```python
# views.py
app_name = 'articles'
urlpatterns = [
    path('index/', views.index, name='index'),
]
```

```html
<a href="{% url 'articles:index' %}">메인페이지</a>
```



#### Template namespace

Django는 기본적으로 app_name/templates/ 경로에 있는 templates 파일들만 찾을 수 있으며, INSTALLED_APPS에 작성한 app순서로 template을 검색한 후 렌더링한다.

그래서 임의로 templates의 폴더 구조를 app_name/templates/app_name 형태로 변경하여 임의로 이름 공간을 생성 후 변경된 추가 경로로 수정한다.

```python
# views.py
def index(request):
    return render(request, 'articles/index.html')
```



폴더 구조 변경 및 템플릿 경로 재작성



### Static files

##### 웹 서버와 정적 파일

웹 서버는 특정 위치(URL)에 있는 자원(resource)을 요청(HTTP request)받아서 제공(serving)하는 응답(HTTP response)을 처리하는 것을 기본 동작으로 한다.

이는 자원과 접근 가능한 주소가 정적으로 연결된 관계이다.

* 예를 들어, 사진 파일은 자원이고 파일 경로는 웹 주소라고 한다.

즉, 웹 서버는 요청 받은 URL로 서버에 존재하는 정적 자원(static resource)를 제공한다.



##### Static file

정적 파일

응답할 때 별도의 처리 없이 파일 내용을 그대로 보여주면 되는 파일

* 사용자의 요청에 따라 내용이 바뀌는 것이 아니라 요청한 것을 그래도 보여주는 파일

예를 들어, 웹 서버는 일반적으로 이미지, 자바 스크립트 또는 CSS와 같은 미리 준비된 추가 파일(움직이지 않는)을 제공해야 한다.

파일 자체가 고정되어 있고, 서비스 중에도 추가되거나 변경되지 않고 고정되어 있다.

Django에서는 이러한 파일들을 "Static file"이라고 한다.

* Django는 staticfiles 앱을 통해 정적 파일과 관련된 기능을 제공한다.



##### Static file 구성

1. django.contrib.staticfiles가 INSTALLED_APPS에 포함되어 있는지 확인한다.

2. settings.py에서 STATIC_URL을 정의한다.

3. 템플릿에서 static 템풀릿 태그를 사용하여 지정된 상대경로에 대한 URL을 빌드한다.

   ```django
   {% load static %}
   <img src="{% static 'my_app/example.jpg' %}" alt="My image">
   ```

4. 앱의 static 디렉토리에 정적 파일을 저장

   * 예시) my_app/static/my_app/example.jpg



#### The staticfiles app

**STATICFILES_DIRS**

* 'app/static/' 디렉토리 경로(기본 경로)를 사용하는 것외에 추가적인 정적 파일 경로 목록을 정의하는 리스트
* 추가 파일 디렉토리에 대한 전체 경로를 포함하는 문자열 목록으로 작성되어야 한다.

```python
STATICFILES_DIRS = [
    BASE_DIR / 'static',
]
```



##### STATIC_URL

STATIC_ROOT에 있는 정적 파일을 참조할 떄 사용할 URL

* 개발 단계에서는 실제 정적 파일들이 저장되어 있는 'app/static/' 경로(기본 경로) 및 STATICFILES_DIRS에 정의된 추가 경로들을 탐색한다.
* 실제 파일이나 디렉토리가 아니며, URL로만 존재한다.
* 비어있지 않은 값으로 설정한다면 반드시 slash(/)로 끝나야 한다.

```python
STATIC_URL = '/static/'
```



##### STATIC_ROOT

collectstatic이 배포를 위해 정적 파일을 수집하는 디렉토리의 절대 경로

django 프로젝트에서 사용하는 모든 정적 파일을 한 곳에 모아 넣는 경로

개발 과정에서 settings.py의 DEBUG 값이 True로 설정되어 있으면 해당 값은 사용되지 않는다.

* 직접 작성하지 않으면 django 프로젝트에서는 settings.py에 작성되어 있지 않는다.

실 서비스 환경(배포 환경)에서 django의 모든 정적 파일을 다른 웹 서버가 직접 제공하기 위한 것이다.



cf)

\# SECURITY WARINING: don't run with debug turned on in production!

DEBUG = True(개발 단계에서 runserver했을 때 오류와 코드를 보여주는 것)

DEBUG = False (배포시 내부코드를 보여주면 안되기 때문에 배포때에는 False로 만든다.)



#### [참고] collectstatic

STATIC_ROOT에 정적 파일을 수집



STATIC_ROOT 작성

```python
STATIC_URL = '/static/'
# STATIC_URL 아래
STATIC_ROOT = BASE_DIR / 'staticfiles'
```



collectstatic 명령어

```bash
$ python manage.py collectstatic
```



#### Django template tag

**load**

* 사용자 정의 템플릿 태그 세트를 로드(load)
* 로드하는 라이브러리, 패키지에 등록된 모든 태그와 필터를 불러온다.



**static**

* STATIC_ROOT에 저장된 정적 파일에 연결한다.

```django
{% load static %}

<img src="{% static 'my_app/example.jpg' %}" alt="My image">
```



#### 정적 파일 사용하기

기본 경로

app/static/app

template에서 경로 참조

```django
<!-- articles/index.html -->

{% extends 'base.html' %}
{% load static %}

{% block content %}
  <img src="{% static 'articles/sample-img-1.jpg' %}" alt="sample-img">
  <h1>INDEX</h1>
{% endblock content %}
```

정적 파일 위치 및 추가 경로 작성

```python
# settings.py
STATICFILES_DIRS = [
    BASE_DIR / 'static',
]
```

```html
<!-- base.html -->
{% load static %}
<!DOCTYPE html>
	...
  <img src="{% static 'images/sample-img-2.jpg' %}" alt="sample-img-2">
{% block content %}
{% endblock content %}
```

