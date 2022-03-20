# Django 4

## Django Model

### Django Model

#### Model

**<u>웹 애플리케이션의 데이터를 구조화하고 조작하기 위한 도구</u>**

데이터들의 필드를 모델에서 관리하고 하나의 데이터베이스 테이블에 하나의 모델을 사용할 것이다.

단일한 데이터에 대한 정보를 가진다.

* 사용자가 저장하는 데이터들의 필수적인 필드들과 동작들을 포함한다.

저장된 데이터베이스의 구조(layout)

Django는 model을 통해 데이터에 접속하고 관리한다.

일반적으로 각각의 model은 하나의 데이터베이스 테이블에 매핑된다.



#### Database

**데이터베이스(DB)**

* 체계화된 데이터의 모임

**쿼리(Query)**

* 데이터를 조회하기 위한 명령어
* 조건에 맞는 데이터를 추출하거나 조작하는 명령어
* "Query를 날린다." -> DB를 조작한다.

#### Database의 기본 구조

스키마(Schema)

* 데이터베이스에서 자료의 구조, 표현방법, 관계 등을 정의한 구조 (structure)

* 데이터베이스의 구조와 제약 조건(자료의 구조, 표현 방법, 관계)에 관련한 전반적인 명세를 기술한 것.

  | column | datatype |
  | ------ | -------- |
  | id     | INT      |
  | age    | INT      |
  | email  | TEXT     |

  

테이블(Table)

 열(컬럼/필드)과 행(레코드/값)의 모델을 사용해 조직된 데이터 요소들의 집합.

 SQL 데이터베이스에서는 테이블을 관계라고도 한다.

* 열(column) : 필드(field) or 속성
  * 각 열에는 고유한 데이터 형식이 지정된다. INTEGER TEXT NULL 등
* 행(row) : 레코드(record) or 튜플
  * 테이블의 데이터는 행에 저장된다.
  * 즉, user 테이블에 4명의 고객정보가 저장되어 있다면 행은 4개가 존재한다.

* PK(기본키)
  * 각 행(레코드)의 고유값으로 Primary Key로 불린다.
  * 반드시 설정해야하며, 데이터베이스 관리 및 관계 설정 시 주요하게 활용된다.



### ORM

Object-Relational-Mapping

객체 지향 프로그래밍 언어를 사욯하여 호환되지 않는 유형의 <u>시스템 간에(Django - SQL)데이터를 변환하는 프로그래밍 기술</u>이다.

OOP 프로그래밍에서 RDBMS을 연동할 때, 데이터베이스와 객체 지향 프로그밍 언어 간의 호환되지 않는 데이터를 변환하는 프로그래밍 기법이다.

Django는 내장 Django ORM을 사용한다.



SQL statement ⇆ ORM ⇆ Python Object

model이 database table에 mapping하는 것인데, model을 객체로 받아주고 model에서 ORM을 사용해서 sql문을 사용하겠다. sql문을 사용하지 않고 데이터를 다루는 방법을 만들어주겠다.

Python을 활용해서 sql을 다룰 것, model인 object를 사용한다.



#### ORM의 장점과 단점

장점

* SQL을 잘 알지 못해도 DB 조작이 가능하다.
* SQL의 절차적 접근이 아닌 객체 지향적 접근으로 인한 높은 생산성을 가진다.

단점

* ORM만으로 완전한 서비스를 구현하기 어려운 경우가 있다.

현대 웹 프레임워크의 요점은 웹 개발의 속도를 높이는 것. (**생산성**)



**"우리는 DB를 객체(Object)로 조작하기 위해 ORM을 사용한다."**



#### models.py 작성

```python
# articles/models.py
from django.db import models

class Article(models.Model):
    title = models.CharField(max_length=10)
    content = modes.TextField()
```

각 모델은 django.models.Model 클래스의 서브 클래스로 표현된다.

* django.db.models 모듈의 Model 클래스를 상속받는다.

models 모듈을 통해 어떠한 타입의 DB 컬럼을 정의할 것인지 정의한다.

* title과 content은 모델의 필드를 나타낸다.
* 각 필드는 크래스 속성으로 지정되어 있으며, 각 속성은 각 데이터베이스의 열에 매핑한다.



#### 사용 모델 필드

**CharField(max_length=, \*\*options)**

* <u>길이의 제한이 있는 문자열</u>을 넣을 때 사용한다.
* CharField의 max_length는 필수 인자
* **필드의 최대 길이(문자),** 데이터베이스 레벨과 Django의 <u>유효성 검사</u>(값을 검증하는 것)에서 활용한다.

**TextField(\*\*options)**

* 글자의 수가 많을 때 사용한다.
* max_length 옵션 작성시 자동 양식 필드인 <u>textarea 위젯에 반영은 되지만 모델과 데이터베이스 수준에는 적용되지 않는다</u>.
  * max_length 사용은 CharField에서 사용해야한다.



### Migrations

#### Mirgration(마이그레이션)

Django가 model에 생긴 변화를 반영하는 방법

Migration 실행 및 DB 스키마를 다루기 위한 몇가지 명령어

* makemigrations
* migrate
* sqlmigrate
* showmigrations



#### Migrations Commands

1. makemigrations
   * model을 변경한 것에 기반한 새로운 마이그레이션(like <u>설계도</u>)을 만들 때 사용한다.
2. migrate
   * <u>마이그래이션을 DB에 반영하기 위해 사용</u>한다.
   * 설계도를 실제 DB에 반영하는 과정이다.
   * 모델에서의 변경 사항들과 DB의 스키마가 동기화를 이룬다.
3. sqlmigrate
   * 마이그레이션에 대한 <u>SQL 구문</u>을 보기 위해 사용한다.
   * 마이그레이션이 SQL문으로 어떻게 해석되어서 동작할지 미리 확인할 수 있다.
4. showmigrations
   * 프로젝트 전체의 마이그레이션 상태를 확인하기 위해 사용한다.
   * <u>마이그레이션 파일들이 migrate 됐는지 안됐는지 여부를 확인</u>할 수 있다.



**실습**

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



실제 DB table확인

vscode sqlite 확장 프로그램을 통해 확인



sqlmigrate

해당 migrations 설계도가 SQL문으로 어떻게 해석되어서 동작할지 미리 확인 가능

```bash
$ python manage.py sqlmigrate app_name 0001
```

```sqlite
BEGIN;
--
-- Create model Article
--
CREATE TABLE "articles_article"
("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT,
"title" varchar(10) NOT NULL, "content" text NOT NULL);
COMMIT;
```

실제 DB에 전달되는 SQL문



showmigrations

```bash
$ python manage.py showmigrations
```

migrations 설계도들이 migrate 됐는지 안됐는지 여부 확인 가능

설계도들의 목록을 볼 수 있다.



showmigrations 결과

```sqlite
admin
 [X] 0001_initial
 [X] 0002_logentry_remove_auto_add
 [X] 0003_logentry_add_action_flag_choices
articles
 [X] 0001_initial
auth
 [X] 0001_initial
 [X] 0002_alter_permission_name_max_length
 [X] 0003_alter_user_email_max_length
 [X] 0004_alter_user_username_opts
 [X] 0005_alter_user_last_login_null
 [X] 0006_require_contenttypes_0002
 [X] 0007_alter_validators_add_error_messages
 [X] 0008_alter_user_username_max_length
 [X] 0009_alter_user_last_name_max_length
 [X] 0010_alter_group_name_max_length
 [X] 0011_update_proxy_permissions
 [X] 0012_alter_user_first_name_max_length
contenttypes
 [X] 0001_initial
 [X] 0002_remove_content_type_name
sessions
 [X] 0001_initial
```



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



#### DateField's options

시험에 나오기 좋다.

**auto_now_add**

* 최초 생성 일자
* Django ORM이 최초 insert(테이블에 데이터를 입력)시에만 현재 날짜와 시간으로 갱신(테이블에 어떤 값을 최초로 넣을 때)

**auto_now**

* 최종 수정 일자
* Django ORM이 save를 할 때마다 현재 날짜와 시간으로 갱신



#### DateTimeField가 아닌 DateField의 option을 확인한 이유

DateTimeField는 Datefield와 동일한 추가 인자(extra argument)를 사용한다.

DateTimeField는 Datefield의 서브 클래스



#### 반드시 기억해야 할 migration 3단계

1. models.py
   * model 변경사항 발생 시
2. $ python manage.py makemigrations
   * migration 파일 생성
3. $ python manage.py migrate
   * DB 반영(모델과 DB의 동기화)



### Database API

"DB를 조작하기 위한 도구"

Django가 기본적으로 ORM을 제공함에 따른 것으로 DB를 편하게 조작할 수 있도록 돕는다.

Model을 만들면 Django는 객체를 만들고 읽고 수정하고 지울 수 있는 database-abstract API를 자동으로 만든다.

database-abstract API 혹은 database-access API라고도 한다.



#### DB API 구문 - Making Queries

Article.objects.all()

Class Name.Manager.QuerySet API



#### DB API

Manager

* <u>Django 모델에 데이터베이스 query 작업이 제공되는 인터페이스</u>
* 기본적으로 모든 Django 모델 클래스에 objects라는 Manager를 추가한다.

QuerySet

* <u>데이터베이스로부터 전달받은 객체 목록</u>
* queryset안의 객체는 0개, 1개 혹은 여러 개일 수 있다.
* 데이터베이스로부터 조회, 필터, 정렬 등을 수행할 수 있다.



#### Django shell

일반 Python shell을 통해서는 장고 프로젝트 환경에 접근할 수 없다.

그래서 장고 프로젝트 설정이 load된 Python shell을 활용해 DB API 구문 테스트를 진행한다.



기본 Django shell보다 더 많은 기능을 제공하는 shell_plus를 사욯해서 진행한다.

* Django-extensions 라이브러리의 기능 중 하나



**실습**

라이브러리 설치

```bash
$ pip install ipython
$ pip install django-extensions
```

More powerful interactive shell을 위한 2가지 라이브러리 설치



라이브러릴 등록 및 실행

```python
# settings.py

INSTALLED_APPS = [
    'django_extensions',
]
```

```bash
$ python manage.py shell_plus
```

앱 등록 후 shell_plus 실행



### CRUD

대부분의 컴퓨터 소프트웨어가 가지는 기본적인 데이터 처리 기능인 Create(생성), Read(읽기), Update(갱신), Delete(삭제)를 묶어서 일컫는 말



##### READ

```sqlite
# DB에 인스턴스 객체를 얻기 위한 쿼리문 날리기
# 이때, 레코드가 하나마 있으면 인스턴스 객체로, 두 개 이상이면 쿼리셋으로 리턴
>>> Aritcle.objects.all()
<QuerySet []>
```

전체 article 객체 조회



##### CREATE

시험에 나오기 좋다.

1 인스턴스 생성 후 인스턴스 변수 설정

```sqlite
### 특정 테이블에 새로운 행을 추가하여 데이터 추가
>>> article = Article() # Article(class)로부터 article(instance)
>>> article.title = "first" # 인스턴스 변수(title)에 값을 할당
>>> article.content = "first content" # 인스턴스 변수(content)에 값을 할당

# save를 하지 않으며 아직 DB에 값이 저장되지 않는다.
>>> article
<Article: Article object (None)>
>>> Article.objects.all()
<QuerySet []>

# save를 하고 확인하면 저장된 것을 확인할 수 있다
article.save()
>>> article
<Article: Article object (1)>
>>> Article.objects.all()
<QuerySet [Article: Article object (1)]>

# 인스턴스인 article을 활용하여 변수에 접근해보자(저장된 것을 확인)
>>> article.title
'first'
>>> article.content
'first content'
>>> article.created_at
datetime.datetime(2022, 3, 20,2 43, 56, 49345, tzinfo=<UTC>)
```



2 초기 값과 함께 인스턴스 생성

```sqlite
>>> article = Article(title="second", content="second content")

# save를 하지 않으며 아직 DB에 값이 저장되지 않는다.
>>> article
<Article: Article object (None)>
>>> Article.objects.all()
<QuerySet []>

>>> article.save()
>>> article
<Article: Article object (2)>
>>> Article.objects.all()
<QuerySet [<Article: Article object (1)>, <Article: Article object (1)>]>

>>> article.pk
2
>>> article.title
'second'
>>> article.content
'second content'
```



3 QuerySet API - create() 사용

```sqlite
# 위의 2개의 방식과는 다르게 바로 쿼리 표현식 리턴
>>> Article.objects.creat(title="third", content="third content")
<Article: Article object(3)>
```



#### CREAT 관련 메서드

**.save() method**

* Saving objects
* 객체를 데이터베이스에 저장한다.
* 데이터 생성 시 save()을 호출하기 전에는 객체의 ID 값이 무엇인지 알 수 없다.
  * ID 값은 Django가 아님 DB에서 계산되기 때문이다.
* 단순히 모델을 인스턴스화 하는 것은 DB에 영향을 미치지 않기 때문에 반드시 save()가 필요하다.



#### str method

```python
class Article(models.Model):
    title = models.CharField(max_length=10)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DataTimeField(auto_now=True)
    
    def __str__(self):
        return self.title
```

표준 파이썬 클래스의 메소드인 str()을 정의하여 각각의 object가 사람이 읽을 수 있는 문자열을 반환(return)하도록 할 수 있다.

**작성 후 반드시 sehll_plus를 재시작해야 반영됨**



#### READ

QuerySet API method를 사용해 다양한 조회를 하는 것이 중요

QuerySet API method는 크게 2가지로 분류

1. Methods that **return new querysets**
2. Methods that **do not return querysets**



**.all()**

현재 QuerySet의 복사본을 반환한다.

```sqlite
>>> Article.objects.all()
```

<QuerySet [<Article: first>, <Article: second>, <Article: third>, <Article: first>]>



**.get()**

주어진 lookup 매개변수와 일치하는 객체를 **반환**

객체를 찾을 수 없으면 DoesNotExist 예외를 발생시키고,

둘 이상의 객체를 찾으면 MultipleObjectsReturned 예외를 발생 시킨다.

```sqlite
>>> article = Article.objects.get(pk=100)
```

DoesNotExist: Article matching query does not exist.

```sqlite
>>> Article.objects.get(title="first")
```

MultipleObjectsReturned: get() returned more than one Article -- it returned 2!

**위와 같은 특징을 가지고 있기 때문에 primary key와 같이 고유(unique)성을 보장하는 조회에서 사용해야 한다.**



**.filter()**

주어진 lookup 매개변수와 일치하는 객체를 **포함하는 새 QuerySet을 반환**

```sqlite
>>> Article.objects.filter(title="first")
```

Out[17]: <QuerySet [<Article: first>, <Article: first>]>



#### UPDATE

article 인스턴스 객체의 인스턴스 변수의 값을 변경 후 저장

```sqlite
# UPDATE articles SET title='fourth' WHERE id=1;
>>> article = Article.objects.get(pk=4)
>>> article.title
"first"

# 값을 변경하고 저장
>>> article.title = "fourth"
>>> article.save()

# 정상적으로 변경된 것을 확인
>>> article.title
"fourth"
```

Out[19]: 'first'



#### DELETE

**delete()**

* QuerySet의 모든 행에 대해 SQL 삭제 쿼리를 수행하고, 
* 삭제된 개체수와 객체 유형당 삭제 수가 포함된 딕셔너리를 반환

```sqlite
>>> article = Article.objects.get(pk=1)

# 삭제
article.delete()
(1, {'Articles.Articles':1})

# 1번은 이제 찾을 수 없다.
>>> Article.obejcts.get(pk=1)
DoesNotExist: Article matching query does not exist.
```

출력

```sqlite
(1, {'articles.Article': 1})
```



#### Field lookups

조회 시 특정 검색 조건을 지정한다.

QuerySet 메서드 **filter(), exclude()** 및 **get()**에 대한 키워드 인수로 지정된다.

```sqlite
Article.objects.filter(pk__gt=2)
Article.objects.filter(contetnt__contains='ja')
```



**QuerySet API**

데이터베이스 조작을 위한 다양한 QuerySet API methods는 해당 공식 문서를 반드시 참고하여 학습



### Admin Site

#### Automatic admin interface

사용자가 아닌 서버의 관리자가 활용하기 위한 페이지

Model class를 admin.py에 등록하고 관리한다.

django.contrib.auth 모듈에서 제공된다.

record 생성 여부 확인에 매우 유용하며, 직접 record를 삽입할 수도 있다.



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



### CRUD with views

```bash
$ pip install -r requirements.txt
$ git init
$ git add .
$ git status
$ git commit -m 'first commit'
$ git log --oneline
```

