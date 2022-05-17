# Django model relation

## Customizing authentication in Django

### Substituting a custom User model

Django는 User를 참조하는데 사용하는 **AUTO_USER_MODEL**값을 제공하여, default user model을 재정의(override)할 수 있도록 한다.

Django는 새 프로젝트를 시작하는 경우 기본 사용자 모델이 충분하더라도, 커스텀 유저 모델을 설정하는 것을 강력하게 권장 (highly recommended)

* **프로젝트의 모든 migrations 혹은 첫 migrate를 실행하기 전에 이 작업을 마쳐야한다.**

#### AUTH_USER_MODEL

User를 나타내는데 사용하는 모델

프로젝트가 **진행되는 동안 변경할 수 없다.**

프로젝트 시작 시 설정하기 위한 것이며, 참조하는 모델은 첫번째 마이그레이션에서 사용할 수 있어야 한다.

기본 값: 'auth.User' (auth 앱의 User 모델)



#### Custom User 모델 정의하기

AbstractUser를 상속받아 새로운 User 모델 작성

```python
# accounts/models.py
from django.contrib.auth.models import AbstractUser
from django.db import models

class User(AbstractUser):
    pass
```

기존에 Django가 사용하는 User모델이었던 auth 앱의 User모델을 accounts앱의 User모델을 사용하도록 변경

```python
# project/settings.py

AUTO_USER_MODEL = 'accounts.User'
```

admin site에 Custom User 모델 등록

```python
# accounts/admin.py
from django.contrib.auth.admin import UserAdmin
from .models import User

admin.site.register(User, UserAdmin)
```

프로젝트 중간에 진행한다면 데이터베이스 초기화 후 마이그레이션 진행

* db.sqlite3 파일 삭제
* migrations 파일 모두 삭제 (파일명에 숫자가 붙은 파일만 삭제)

```bash
$ python manage.py makemigrations
$ python manage.py migrate
```



class User(AbstractUser):

followings = models.ManyToManyField('self', symmetrical=False, related_name='followers')

user.following.filter(pk=request.person.pk)

person.followers.filter(pk=request.user.pk)