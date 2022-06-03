### A

1. venv/requirements
2. git init, git ignore
3. repo / remote / maintainer
4. git add / commit / push



### B

1. git clone
2. venv/ requirements
3. git add / commit / push



### A / B

1. git pull
2. git add / commit /push



### model 생성 후 새로운 레코드가 생성되었을 시

1. git pull
2. 레코드 추가
3. `python manage.py dumpdata --indent 4 app_name.model_name > model_name.json`
   1. 레코드가 추가된 모델만
4. git add / commit / push



### 상대방이 새로운 레코드를 만들었을 시

1. git pull
2. `python manage.py loaddata model_name.json`

```bash
$ python manage.py migrate
$ python manage.py loaddate movies/
```

