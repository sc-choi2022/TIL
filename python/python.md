## Python 기초

* 변수에 별도의 **타입 지정**이 필요 없음
* 문장 구분 시 **들여쓰기** 사용

크로스 플랫폼 언어

* Windows, macOS, Linux, Unix 등 다양한 운영체제에서 실행가능

인터프리터 언어(Interpreter)

* 컴파일 과정 (소스코드를 기계어로 변환) 없이 바로 실행 가능
* 한 줄 입력하고 실행하여 바로 확인 가능

객체 지향 프로그래밍(Object Orented Programming)

* 모든 것이 객체(Object)로 구현되어 있음



#### Jupyter Lab

웹 브라우저 환경에서 코드를 작성할 수 있는 오픈소스

대화형 환경 (e.g) Python 기본 Interpreter



### Python 스크립트 실행

#### IDE(Integrated Development Environment) 통합 개발 환경

e.g.) Pycharm

#### Text editor

e.g.) Visual Studio Code



cf)

Algorithm : Pycharm

Coding

​			Python : Jupyter Notebook, Visual Studio Code

​			Web : Visual Studio Code



### 기초 문법

#### 기초 스타일 가이드

Python에서 제안하는 스타일 가이드 : PEP8

기업, 오픈소스 등에서 사용되는 스타일 가이드 : Google Style guide



#### 들여쓰기(Identation)

**4칸(space키 4번)** 혹은 **1탭(Tab키 1번)**



#### 객체(Object)

숫자, 문자, 클래스 등 값을 가지고 있는 모든 것



#### 변수(Variable)

컴퓨터 메모리에 저장되어 있는 객체를 참조하기 위해 사용되는 이름

변수는 할당 연산자(=)를 통해 값을 할당(assignment)

* type()
  * 변수에 할당된 값의 타입
  * 변수 활용의 핵심은 **이 변수의 type이 무엇인가**이다.
* id()
  * 변수에 할당된 값(객체)의 고유한 identity 값이며, 메모리주소

변수할당의 예시

```python
x = y = 1004
x, y = 1, 2
```

임시 변수 활용의 예시

```python
x, y = 10, 20
tmp = x
x = y
y = tmp
```

Python에서의 방법 (Pythonic!)

```python
x, y = 10, 20
y, x = x, y
```



#### 식별자(Identifiers)

파이썬 객체(변수, 함수, 모듈, 클래스 등)를 식별하는데 사용하느 이름(name)

규칙

* 이름을 영문 알파벳, _, 숫자로 구성
* 첫 글자에 숫자가 올 수 없음
* 대소문자를 구별
* 길이제한 없음
* 예약어는 사용할 수 없음
* 내장함수나 모듈 등의 이름으로 만들면 안됨

RedApple : CamelCase

**red_apple : snake_case**



#### 예약어(reserved words)

False, None, True, and, as, assert, async, await, break, class, continue, def, del, elif, else, except, finally, for, from, global, if, import, in, is, lambda, nonlocal, not, or, pass, raise, return, try, while, with, yield

```python
import keyword
print(keyword.kwlist)

['False', 'None', 'True', '__peg_parser__', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```

* 사용시에 SyntaxError: cannot assign to False 와 같은 error가 나온다.

#### 사용자 입력

```python
input()
```

반환값은 항상 문자열의 형태



#### 주석(Comment)

코드에 대한 설명

* 중요한 점이나 다시 확인 필요한 부분 표시

가장 중요한 습관

* 쉬운 이해와 코드의 분석 및 수정이 용이

한 줄 주석

* 주석으로 처리될 내용 앞에 '#'을 입력

여러 줄 주석

* 한 줄 씩 '#' 사용
* """ 또는 '''으로 표현
* ctrl + / 를 이용해서 주석 작성

특수한 형태의 주석

* 함수/클래스의 설명을 작성



### 파이썬 자료형(Python Datatype)

#### Data Type

* Boolean Type
* Numeric Type
  * Int (Integer, 정수)
  * Float (Floating point number, 부동소수점, 실수)
  * Complex (complex number, 복소수)
* String Type
* None

#### Boolean Type

True / False 값을 가진 타입

비교/논리 연산 수행에 활용

```python
if lit: '''
		만약 list lit이 []이라면 False
		만약 list lit이 []이 아니라면 True
		전자의 경우라면 if문이 실행되지 않을 것
		'''
```



**False로 변환되는 것**

* 0, 0.0, (), [], {}, '', None

#### Numeric Type

##### Int 

: 모든 정수의 타입

매우 큰 수를 나타낼 때 오버플로가 발생하지 않음

cf) 오버플로우(overflow) : 데이터 타입별로 사용할 수 있는 메모리의 크기를 넘어서는 상황

**0b : 2진수 / 0o : 8진수 / 0x : 16진수**



##### Float

: 정수가 아닌 모든 실수의 타입

부동소수점: Floating point number

**Floating point rounding error**

```python
3.14 - 3.02 == 0.12

False
```

매우 작은 수보다 작은지를 확인하거나 math 모듈 활용

```python
#1. 임의의 작은 수 
abs(a - b) <= 1e-10

#2. system상의 machine epslion(컴퓨터가 표현할 수 있는 가장 작은 수)
import sys
print(abs(a-b)<=sys.float_info.epsilon)
print(sys.float_info.epsilon)

#3. python 3.5이상
import math
math.isclose(a,b)
```



##### Complex

: 실수부와 허수부로 구성된 모든 복소수의 타입

허수부는 j로 표현



#### String Type

##### str

: 모든 문자의 타입

문장부호 ' 혹은 문장부호 "를 활용하여 표기 **(문자열을 묶을 때 동일한 문장부호를 활용)**

**Immutable**

**Iterable**

##### 중첩따옴표(Nested Quotes)

```python
print("문자열 안에 '작은 따옴표'를 사용하려면 큰 따옴표로 묶는다")
print('문자열 안에 "큰 따옴표"를 사용하려면 작은 따옴표로 묶는다')
```



##### 삼중따옴표(Triple Quotes)

```python
print('''문자열 안에 '작은 따옴표'나 "큰 따옴표"를 사용할 수 있고 여러 줄을 사용할 때도 편리하다.''')
# 작은 따옴표나 큰 따옴표를 삼중으로 사용
```



##### Escape sequence

문자열 내에서 특정 문자나 조작을 위해서 백슬래시(\)를 활용하여 구분

| Escape sequence | 의미              |
| --------------- | ----------------- |
| \n              | 줄 바꿈(new line) |
| \t              | 탭                |
| \r              | 캐리지리턴        |
| \0              | 널(Null)          |
| \\\             | \\                |
| \\'             | '                 |
| \\"             | "                 |

캐리지리턴

: 커서를 맨 앞으로 보내는 것(타자기 끝을 앞으로 당기는 것)

```python
print('123456\rabc')

abc456
```

```python
print('철수 \'안녕\'')

철수 '안녕'
```



##### String Interpolation (문자열 사이에 변수)

%-formatting

```python
print('Hello, %s' %name)
print('score: %d' %score)
print('total: %.2f' %total)
```



str.format()

```python
print('Hello, {}! 성적은 {}'.format(name,total))
```



f-strings : **python 3.6+**

```python
print(f'Hello, {name}! 성적은 {total}')
```

```python
import datetime
today = datetime.datetime.now()

f'오늘은 {today:%y}년 {today:%m}월 {today:%d}일'

pi = 3.141592
f'원주율은 {pi:.3}. 반지름이 2일때 원의 넒이는 {pi*2*2}'

결과
'원주율은 3.14. 반지름이 2일때 원의 넓이는 12.566368'
#.을 포함해서 3자리수
#{pi:.2}라면 3.1까지 출력된다.
```



#### None

값이 없음을 표현하기 위한 타입

반환 값이 없는 함수에서 사용하기도 함

```python
a = print()
print(a)

None
```

