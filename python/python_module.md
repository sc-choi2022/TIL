## Module



### Module and Package

Module

: 특정 기능을 하는 코드를 파이썬 파일(.py) 단위로 작성한 것



Package

: 다양한 파일을 하나의 폴더로

* 특정 기능과 관련된 여러 Module의 집합
* Package 안에는 또 다른 Sub Package를 포함



Library

: 다양한 Package를 하나의 묶음으로



#### Module 과 Package 불러오기

```python
import module
from module import var, function, Class
from module import *	#* : all

from package import module
from package.module import var, function, Class
```

```python
import random

print(random.sample(range(1,46), 6))
```

```python
import pprint

pprint.pprint(a)

from pprint import pprint
pprint(a)
```



### Python Standard Library (PSL)

Python에 기본적으로 설치된 모듈과 내장 함수

<https://docs.python.org/ko/3/library/index.html>



### pip (파이썬 패키지 관리자)

PyPI(Python Package Index)에 저장된 외부 Package들을 설치하도록 도와주는 Package 관리 시스템

* 어떤 input값을 넣어 어떤 output값을 받을 수 있는지 확인

예) Jupyter



#### pip 명령어

* 패키지 설치
  * 최신 버전 / 특정 버전 / 최소 버전을 명시하여 설치 할 수 있음
  * 이미 설치되어 있는 경우 이미 설치되어 있음을 알리고 아무것도 하지 않음

```
$ pip install SomePackage
$ pip install SomePackage==1.0.5
$ pip install 'SomePackage>=1.0.4'

$ : 모두 bash, cmd 환경에서 사용되는 명령어
```

**Successfully installed ** 확인



* 패키지 삭제
  * pip는 패키지를 업그레이드 하는 경우 과거 버전을 자동으로 지워줌
  * **Successfully uninstalled**

```
$ pip uninstall SomePackage
```



* 패키지 목록 및 특정 패키지 정보

```
$ pip list
$ pip show SomePackage
```



* 패키지 freeze
  * 설치된 패키지의 비슷한 목록을 만들지만, pip install에서 활용되는 형식으로 출력
  * 해당하는 목록을 requirements.txt(관습)으로 만들어 관리함

```
$ pip freeze
```



* 패키지 관리하기
  * 아래의 명령어들을 통해 패키지 목록을 관리[1]하고 설치할 수 있음[2]
  * 일반적으로 패키지를 기록하는 파일의 이름은 requirements.txt로 정의함

```
$ pip freeze > requirements.txt
$ pip install -r requirements.txt
```



* 다양한 Python 프로젝트에서 사용됨



### 사용자 Module 과 Package

#### Module 만들기 - check

* check.py에 짝수를 판별하는 함수(even)와 홀수를 판별하는 함수(odd)를 만들고 check 모듈을 활용 해 보시오.

```python
# check.py
def odd(n):
    return bool(n%2)

def even(n):
    return not bool(n%2)
```



#### Module 활용하기 - check

* 모듈을 활용하기 위해서는 import문을 통해 가져옴

```python
import check	# 위 check.py 사용
dir(check)		# 결과 생략
check.odd(3)
check.even(3)

True
False
```

```python
from check import odd	# 위 check.py 사용
odd(5)
even(4)

True
# NameError
```

```python
from check import *	# 위 check.py 사용
odd(5)
even(4)

True
False
```



#### Package

* 패키지는 여러 Module/ 하위 Package로 구조화
  * 활용 예시:  package.module
* 모든 폴더에는 \__init__.py를 만들어 Package로 인식
  * Python 3.3부터는 파일이 없어도 되지만, 하위 버전 호환 및 프레임워크 등에서의 동작을 위해 파일을 생성하는 것을 권장



#### Package 만들기

* 수학과 통계 기능이 들어간 Package를 아래와 같이 구성

  * math의 tools: 자연 상수 e, 원주율 pi 값, 최대값을 구하는 my_max 함수

  * statistics의 tools: 평균을 구하는 mean 함수

  * 폴더 구조

    ​	my_package/

    ​			\__init__.py

    ​			math/

    ​					\__init__.py

    ​					tools.py

    ​			statistics/

    ​				\__init__.py

    ​				tools.py

* 라이브강의에서 예시 실습진행



### 가상환경

* 파이썬 표준 라이브러리가 아닌 외부 Package와 Module을 사용하는 경우 모두 pip를 통해 설치를 해야함
* 복수의 프로젝트를 하는 경우 버전이 상이할 수 있음
  * 과거 외주 프로젝트 - django 버전 2.x
  * 신규 회사 프로젝트 - django 버전 3.x
* 이러한 경우 가상환경을 만들어 프로젝트별로 독립적인 패키지를 관리 할 수 있음



#### venv

* 가상 환경을 만들고 관리하는데 사용되는 Module(Python 버전 3.5부터)
* 특정 디렉토리에 가상 환경을 만들고, 고유한 Python Package 집합을 가질 수 있음
  * 특정 폴더에 가상 환경이(Package 집한 폴더 등) 있고
  * 실행 환경(예 - bash)에서 가상환경을 활성화 시켜
  * 해당 폴더에 있는 Package를 관리/사용함



#### 가상환경 생성

* 가상환경을 생성하면, 해당 디렉토리에 별도의 Python package가 설치됨

```bash
$ python -m venv venv
```



#### 가상환경 활성화/비활성화

* 아래의 명령어를 통해 가상환경을 활성화
  * \<venv>는 가상환경을 포함하는 디렉토리의 경로

| 플랫폼 |       셀        |      가상 환경을 활성화하는 명령      |
| :----: | :-------------: | :-----------------------------------: |
| POSIX  |    bash/zsh     |    $ source \<venv>/ bin/activate     |
|        |      fish       |  $ source \<venv>/ bin/activate.fish  |
|        |    csh/tcsh     |  $ source \<venv>/ bin/activate.csh   |
|        | PowerShell Core |      $ \<venv>/vin/Activate.ps1       |
| 윈도우 |     cmd.exe     |  C:\\>\<venv>\\Scrips\\activate.bat   |
|        |   PowerShell    | PS C:\\>\<venv>\\Scrips\\Activate.ps1 |

* 가상환경 비활성화는 $ decativate 명령어를 사용