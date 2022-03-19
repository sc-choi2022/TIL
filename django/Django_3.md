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