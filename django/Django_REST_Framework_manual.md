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
$ django-admin startproject my_api .
# my_api is the name of project
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
$ python manage.py startapp musics
# musics is the name of Application
```



8 Application 등록

firstpjt > settings.py

```python
INSTALLED_APPS = [
    'musics',
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

class Artist(models.Model):
    name = models.CharField(max_length=200)

class Music(models.Model):
    artist = models.ForeignKey(Artist, on_delete=models.CASCADE)
    title = models.CharField(max_length=200)
```



## Migrations

makemigrations

```bash
$ python manage.py makemigrations
```

migrate

```bash
$ python manage.py migrate
```



#### admin 등록

```python
# musics/admin.py
from django.contrib import admin
from .models import Artist, Music

admin.site.register(Artist)
admin.site.register(Music)
```

admin.py는 관리자 사이트에 Artist, Music객체가 관리자 인터페이스를 가지고 있다는 것을 알려주는 것

models.py에 정의한 \_\_str\_\_의 형태로 객체가 표현된다.



## Django REST Framework

```bash
$ pip install djangorestframework
```

```bash
$ pip freeze > requirements.txt
```



```python
# settings.py
INSTALLED_APPS = [
    'rest_framework',
]
```

```python
# my_api/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/v1/', include('musics.urls')),
]
```



### api/v1/artists/ :heavy_check_mark:

```python
# musics/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('artists/', views.artist_list),
]
```



#### GET:heavy_check_mark:

```python
# serializers.py
from rest_framework import serializers
from .models import Artist

class ArtistListSerializer(serializers.ModelSerializer):

    class Meta:
        model = Artist
        fields = ('id', 'name',)
```

```python
# views.py
from django.shortcuts import get_list_or_404
from rest_framework.response import Response
from rest_framework.decorators import api_view
from .models import Artist
from .serializers import ArtistListSerializer

@api_view()
def artist_list(request):
    artist = get_list_or_404(Artist)
    serializers = ArtistListSerializer(artist, many=True)
    return Response(serializers.data)
```

```json
[
    {
        "id": 1,
        "name": "IU"
    },
    {
        "id": 2,
        "name": "BTS"
    }
]
```



#### GET & POST:heavy_check_mark:

```python
# serializers.py
from rest_framework import serializers
from .models import Artist

class ArtistListSerializer(serializers.ModelSerializer):

    class Meta:
        model = Artist
        fields = ('id', 'name',)


class ArtistSerializer(serializers.ModelSerializer):

    class Meta:
        model = Artist
        # fields = ('id', 'name', 'music_set', 'music_count',)
        fields = '__all__'
```

```python
# views.py
from django.shortcuts import get_list_or_404
from rest_framework import status
from rest_framework.response import Response
from rest_framework.decorators import api_view
from .models import Artist
from .serializers import ArtistListSerializer, ArtistSerializer

@api_view(['GET', 'POST'])
def artist_list(request):
    if request.method == 'GET':
        artist = get_list_or_404(Artist)
        serializers = ArtistListSerializer(artist, many=True)
        return Response(serializers.data)
    elif request.method =='POST':
        serializer = ArtistSerializer(data=request.data)
        if serializer.is_valid(raise_exception=True):
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
```

```json
{
    "id": 3,
    "name": "Jay Park"
}
```



### api/v1/artists/<artist_pk>/:heavy_check_mark:

특정 가수의 모든 컬럼을 JSON으로 응답한다. 

특정 가수의 노래 정보와 노래의 개수 정보를 함께 응답한다.

```python
# musics/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('artists/', views.artist_list),
    path('artists/<artist_pk>/', views.artist_detail),
]
```



#### GET:heavy_check_mark:

```python
# serializers.py
from rest_framework import serializers
from .models import Artist, Music

class ArtistSerializer(serializers.ModelSerializer):
    music_set = MusicSerializer(many=True, read_only=True)
    music_count = serializers.IntegerField(source='music_set.count', read_only=True)
    class Meta:
        model = Artist
        fields = ('id', 'name', 'music_set', 'music_count',)
```

```python
# views.py
from django.shortcuts import get_object_or_404
from rest_framework.decorators import api_view
from rest_framework.response import Response
from .models import Artist
from .serializers import ArtistSerializer

@api_view(['GET'])
def artist_detail(request, artist_pk):
    artist = get_object_or_404(Artist, pk=artist_pk)
    serializer = ArtistSerializer(artist)
    return Response(serializer.data)
```

```json
{
    "id": 1,
    "name": "IU",
    "music_set": [
        {
            "id": 3,
            "title": "strawberry moon",
            "artist": 1
        },
        {
            "id": 5,
            "title": "Blueming",
            "artist": 1
        },
        {
            "id": 6,
            "title": "Celebrity",
            "artist": 1
        }
    ],
    "music_count": 3
}
```



### api/v1/artists/<artist_pk>/music/:heavy_check_mark:

```python
# serializers.py
from django.urls import path
from . import views

urlpatterns = [
    path('artists/', views.artist_list),
    path('artists/<artist_pk>/', views.artist_detail),
    path('artists/<artist_pk>/music/', views.music_create),
    path('music/', views.music_list),
    path('music/<music_pk>/', views.music_detail),
]
```



#### POST:heavy_check_mark:

```python
# serializers.py
from rest_framework import serializers
from .models import Music

class MusicSerializer(serializers.ModelSerializer):

    class Meta:
        model = Music
        fields = ('id','title','artist',)
```

```python
# views.py
from django.shortcuts import get_object_or_404
from rest_framework import status
from rest_framework.decorators import api_view
from rest_framework.response import Response
from .models import Artist
from .serializers import MusicSerializer

@api_view(['POST'])
def music_create(reqeust, artist_pk):
    artist = get_object_or_404(Artist, pk=artist_pk)
    serializer = MusicSerializer(data=reqeust.data)
    if serializer.is_valid(raise_exception=True):
        serializer.save(artist=artist)
        return Response(serializer.data, status=status.HTTP_201_CREATED)
```

```json
{
    "id": 7,
    "title": "LILAC",
    "artist": 1
}
```



### api/v1/music/ :heavy_check_mark:

```python
# musics/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('music/', views.music_list),
]
```



#### GET:heavy_check_mark:

```python
# serializers.py
from rest_framework import serializers
from .models import Music

class MusicListSerializer(serializers.ModelSerializer):

    class Meta:
        model = Music
        fields = ('id','title',)
```

```python
# views.py
from django.shortcuts import get_list_or_404
from rest_framework.response import Response
from rest_framework.decorators import api_view
from .models import Music
from .serializers import MusicListSerializer

@api_view(['GET'])
def music_list(request):
    music = get_list_or_404(Music)
    serializers = MusicListSerializer(music, many=True)
    return Response(serializers.data)
```

```json
[
    {
        "id": 1,
        "title": "strawberry moon"
    },
    {
        "id": 2,
        "title": "Butter"
    }
]
```



### api/v1/music/<music_pk>/:heavy_check_mark:

```python
# musics/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('music/<music_pk>/', views.music_detail),
]
```



#### GET:heavy_check_mark:

```python
# serializers.py
class MusicSerializer(serializers.ModelSerializer):

    class Meta:
        model = Music
        fields = ('id','title','artist',)
```

```python
# views.py
from django.shortcuts import get_object_or_404
from rest_framework.response import Response
from rest_framework.decorators import api_view
from .models import Music
from .serializers import MusicSerializer

@api_view(['GET'])
def music_detail(request, music_pk):
    music = get_object_or_404(Music, pk=music_pk)
    serializer = MusicSerializer(music)
    return Response(serializer.data)
```

```json
{
    "id": 1,
    "title": "strawberry moon",
    "artist": 1
}
```



#### PUT:heavy_check_mark:

```python
# serializers.py
class MusicSerializer(serializers.ModelSerializer):

    class Meta:
        model = Music
        fields = ('id','title','artist',)
```

```python
# views.py
from django.shortcuts import get_object_or_404
from rest_framework.response import Response
from rest_framework.decorators import api_view
from .models import Music
from .serializers import MusicSerializer

@api_view(['GET','PUT'])
def music_detail(request, music_pk):
    music = get_object_or_404(Music, pk=music_pk)
    if request.method == 'GET':
        serializer = MusicSerializer(music)
        return Response(serializer.data)

    elif request.method == 'PUT':
        serializer = MusicSerializer(instance=music, data=request.data)
        if serializer.is_valid(raise_exception=True):
            serializer.save()
            return Response(serializer.data)
```

```python
{
    "id": 1,
    "title": "Coin",
    "artist": 1
}
```



#### DELETE:heavy_check_mark:

```python
# serializers.py
class MusicSerializer(serializers.ModelSerializer):

    class Meta:
        model = Music
        fields = ('id','title','artist',)
```

```python
# views.py
from django.shortcuts import get_object_or_404
from rest_framework import status
from rest_framework.response import Response
from rest_framework.decorators import api_view
from .models import Music
from .serializers import MusicSerializer

@api_view(['GET','PUT','DELETE'])
def music_detail(request, music_pk):
    music = get_object_or_404(Music, pk=music_pk)
    if request.method == 'GET':
        serializer = MusicSerializer(music)
        return Response(serializer.data)

    elif request.method == 'PUT':
        serializer = MusicSerializer(instance=music, data=request.data)
        if serializer.is_valid(raise_exception=True):
            serializer.save()
            return Response(serializer.data)
    
    elif request.method == 'DELETE':
        music.delete()
        data = {
            'delete': f'{music_pk}번 음악이 삭제되었습니다.'
        }
        return Response(data, status=status.HTTP_204_NO_CONTENT)
```

```json
{
    "delete": "1번 음악이 삭제되었습니다."
}
```

