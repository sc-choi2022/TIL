## 파이썬 프로그램 구성 단위

### Identifier

식별자

변수, 함수, 클래스 등 프로그램이 실행되는 동안 다양한 값을 가질 수 있는 이름



### Literal

리터럴

일혀지는 대로 쓰여있는 값 자체

```python
# name은 식별자 = variable
# '김나리'는 literal
name = '김나리'
```



### Expression

표현식

새로운 데이터 값을 생성하거나 계산하는 모드 조각



### Statement

문장

특정한 작업을 수행하는 코드 전체

Python이 실행 가능한 최소한의 코드 단위

Expression은 값을 생성하는 일부분이고, 문장은 특정장접을 수행하는 코드 전체

<u>모든 expression은 statement이다.</u>

```python
# 하나의 값(value)도 문장이 될 수 있습니다.
'sales'

# 표현식(expression)도 문장이 될 수 있습니다.
5 * 21 - 4

# 실행 가능(executable)해야 하기 때문에 아래의 코드는 문장이 될 수 없습니다.
name = '
```



### Function

함수

특정 명령을 수행하는 함수 묶음

```python
def multiply(x, y, z):
    return x * y * z


multiply(5, 6, 3)
```



### Module

모듈

함수/클래스의 모음 또는 하나의 프로그램을 구성하는 단위



### Package

패키지

프로그램과 모듈 묶음

* 프로그램 : 실행하기 이ㅜ한 것
* 모듈 : 다른 프로그램에서 불러와 사용하기 위한 것



### Library

라이브러리

패키지 모음

