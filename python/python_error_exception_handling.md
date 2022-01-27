# Error/Exception_Handling

##### 디버깅

제거가 되는 시점

조건/반복, 함수

##### branches 

: 모든 조건이 원하는대로 동작하는지

##### for loops 

: 반복문에 진입하는지, 원하는 횟수만큼 실해되는지

##### while loops 

: for loops와 동일, 종료조건이 제대로 동작하는지

##### function

: 함수 호출시, 함수 파라미터, 함수 결과



### Debugging

print문 활용

* 특정 함수 결과, 반복/조건 결과 등 나눠서 생각, 코드를 bisection으로 나눠서 생각

개발환경(text editor, IDE) 등에서 제공하는 기능 활용

* breakpoint, 변수 조회등

Python tutor 활용(단순 파이썬 코드인 경우)

뇌컴파일, 눈디버깅



에러 메시지가 발생하는 경우

* 해당 하는 위치를 찾아 메시지를 해결

로직 에러가 발생하는 경우

* 명시적인 에러 메시지 없이 예상과 다른 결과가 나온 경우
  * 정상적으로 동작하였던 코드 이후 작성된 코드를 생각해봄
  * 전체 코드를 살펴봄
  * 휴식을 가져봄
  * 누군가에게 설명해봄



### Error and Exception

#### Syntax Error

문법 에러



SyntaxError가 발생하면, Python 프로그램은 실행이 되지 않음

파일이름, 줄번호, ^문자를 통해 Python이 코드를 읽어 나갈 때(parser) 문제가 발생한 위치를 표현

줄에서 에러가 감지된 가장 앞의 위치를 가리키는 캐럿(caret)기호(^)를 표시

```python
if True:
    print('참')
else
    print('거짓')
    
Input In [1]
    else
        ^
SyntaxError: invalid syntax    
```



**Invalid syntax**

```python
while

  Input In [1]
    while
         ^
SyntaxError: invalid syntax
```



**assign to literal**

```python
5 = 3

  Input In [2]
    5 = 3
    ^
SyntaxError: cannot assign to literal
```



**EOL (End of Line)**

```py
print('hi)

SyntaxError: EOL while scanning string literal
```



**EOF (End of File)**

```python
print('hi'
      
  Input In [3]
    print('hi'
              ^
SyntaxError: unexpected EOF while parsing      
```



#### Exception

예외



실행 도중 예상치 못한 상황을 맞이하면, 프로그램 실행을 멈춤

* 문장이나 표현식이 <u>문법적으로 올바르더라도 발생하는 에러</u>

실행 중에 감지되는 에러들을 예외(Exception)라고 부름

예외는 여러 타입(type)으로 나타나고, 타입이 메시지의 일부로 출력됨

* NameError, TypeError 등은 발생한 예외 타입의 종류(이름)

모든 내장 예외는 Exception Class를 상속받아 이뤄짐

사용자 정의 예외를 만들어 관리할 수 있음



**ZeroDivisionError** : 0으로 나누고자 할 때 발생

```python
10/0

ZeroDivisionError                         Traceback (most recent call last)
Input In [1], in <module>
----> 1 10/0

ZeroDivisionError: division by zero
```



**NameError** : namespace 상에 이름이 없는 경우

```python
print(name_error)

NameError                                 Traceback (most recent call last)
Input In [2], in <module>
      1 # abc라는 변수를 print로 출력해 보고 오류를 확인해 봅시다.
----> 3 print(name_error)

NameError: name 'name_error' is not defined
```



**TypeError** 

: 타입 불일치

```python
1 + '1'

TypeError                                 Traceback (most recent call last)
Input In [3], in <module>
----> 1 print(1+'1')

TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

```python
round('3.5')

TypeError                                 Traceback (most recent call last)
Input In [4], in <module>
----> 1 round('3.5')

TypeError: type str doesn't define __round__ method
```



**Exception**

: argument 누락

```python
divmod()

TypeError                                 Traceback (most recent call last)
Input In [5], in <module>
----> 1 divmod()

TypeError: divmod expected 2 arguments, got 0
```

```python
import random
random.sample()

TypeError                                 Traceback (most recent call last)
Input In [6], in <module>
      1 import random
----> 2 random.sample()

TypeError: sample() missing 2 required positional arguments: 'population' and 'k'
```



: argument 개수 초과

```python
divmod(1, 2, 3)

TypeError                                 Traceback (most recent call last)
Input In [7], in <module>
----> 1 divmod(1, 2, 3)

TypeError: divmod expected 2 arguments, got 3
```

```python
import random
random.sample(range(3), 1, 2)

---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Input In [8], in <module>
      1 import random
----> 2 random.sample(range(3), 1, 2)

TypeError: sample() takes 3 positional arguments but 4 were given
```



: argument type 불일치

```python
import random
random.sample(1, 2)

TypeError                                 Traceback (most recent call last)
Input In [9], in <module>
      1 import random
----> 2 random.sample(1, 2)

File ~\AppData\Local\Programs\Python\Python39\lib\random.py:433, in Random.sample(self, population, k, counts)
    431     population = tuple(population)
    432 if not isinstance(population, _Sequence):
--> 433     raise TypeError("Population must be a sequence.  For dicts or sets, use sorted(d).")
    434 n = len(population)
    435 if counts is not None:

TypeError: Population must be a sequence.  For dicts or sets, use sorted(d).
```



**ValueError**

: 타입은 올바르나 <u>값이 적절하지 않거나 없는 경우</u>

```python
int('3.5')

---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
Input In [10], in <module>
----> 1 int('3.5')

ValueError: invalid literal for int() with base 10: '3.5'
```

```python
range(3).index(6)

ValueError                                Traceback (most recent call last)
Input In [11], in <module>
----> 1 range(3).index(6)

ValueError: 6 is not in range
```



**IndexError**

: 인덱스가 존재하지 않거나 범위를 벗어나는 경우

```python
empty_list = []
empty_list[2]

---------------------------------------------------------------------------
IndexError                                Traceback (most recent call last)
Input In [12], in <module>
      1 empty_list = []
----> 2 empty_list[2]

IndexError: list index out of range
```



**KeyError**

: 해당 키가 존재하지 않는 경우

```python
song = {'IU':'좋은날'}
song['BTS']

KeyError                                  Traceback (most recent call last)
Input In [13], in <module>
      1 song = {'IU':'좋은날'}
----> 2 song['BTS']

KeyError: 'BTS'
```



**ModuleNotFoundError**

: 존재하지 않는 모듈을 import 하는 경우

```python
import happy

ModuleNotFoundError                       Traceback (most recent call last)
Input In [15], in <module>
----> 1 import happy

ModuleNotFoundError: No module named 'happy'
```



**ImportError**

: Module은 있으나 존재하지않는 클래스/함수를 가져오는 경우

```python
from random import sample
sample(range(3),1)

[1]
```

```python
from random import samp

ImportError                               Traceback (most recent call last)
Input In [19], in <module>
----> 1 from random import samp

ImportError: cannot import name 'samp' from 'random' (C:\Users\choiy\AppData\Local\Programs\Python\Python39\lib\random.py)
```



**KeyboardInterrupt**

: 임의로 프로그램을 종료하였을 때

```python
While True:
    continue
```



**IndentationError**

: Indentation이 적절하지 않은 경우

```python
for i in range(3):

print(i)  

  Input In [20]
    print(i)
    ^
IndentationError: expected an indented block
```

```python
for i in range(3):
    print(i)
    	print(i)
        
  Input In [21]
    print(i)
    ^
IndentationError: unexpected indent        
```



### Exception Handling

try 문 (statement) / except 절 (clause)을 이용하여 예외 처리를 할 수 있음

try문

* 오류가 발생할 가능성이 있는 코드를 실행
* 예외가 발생되지 않으면, except 없이 실행 종료

except문

* 예외가 발생하면, except 절이 실행
* 예외 상황을 처리하는 코드를 받아서 적절한 조치를 취함

```python
try:
    num = input('숫자입력 :')
    print(int(num))
except ValueError:
    print('숫자가 입력되지 않았습니다.')
    
숫자입력 :d
숫자가 입력되지 않았습니다.    
```

```python
num = input('100으로 나눌 값을 입력하시오 : ')
print(100/int(num))

# 100/int('a') : TypeError
# 100/int('0') : ZeroDivisionError

try:
    num = input('값을 입력하시오: ')
    100/int(num)
except ValueError:
    print('숫자를 넣어주세요.')
except ZeroDivisionError:
    print('0으로 나눌 수 없습니다.')
except:
    print('에러는 모르겠지만 에러가 발생하였습니다.')
    
100으로 나눌 값을 입력하시오 : a
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
Input In [23], in <module>
      1 num = input('100으로 나눌 값을 입력하시오 : ')
----> 2 print(100/int(num))
      4 # 100/int('a') : TypeError
      5 # 100/int('0') : ZeroDivisionError
      7 try:

ValueError: invalid literal for int() with base 10: 'a'
        
100으로 나눌 값을 입력하시오 : 0
---------------------------------------------------------------------------
ZeroDivisionError                         Traceback (most recent call last)
Input In [24], in <module>
      1 num = input('100으로 나눌 값을 입력하시오 : ')
----> 2 print(100/int(num))
      4 # 100/int('a') : TypeError
      5 # 100/int('0') : ZeroDivisionError
      7 try:

ZeroDivisionError: division by zero        
```



<u>**에러가 순차적으로 수행됨으로, 가장 작은 범주부터 예외 처리를 해야함**</u>

```python
try:
    num = input('값을 입력하시오: ')
    100/int(num)
except Exception:
    print('에러는 모르겠지만 에러가 발생하였습니다.')
except ValueError:
    print('숫자를 넣어')
    
값을 입력하시오: e
에러는 모르겠지만 에러가 발생하였습니다.    
```



try

* 코드를 실행함

except

* try 문에서 예외가 발생시 실행함

else

* try 문에서 예외가 발생하지 않으면 실행함

finally

* 예외 발생 여부와 관계없이 항상 실행함



예시

파일을 열고 읽는 코드를 작성하는 경우

* 파일 열기 시도
  * 파일 없는 경우 -> '해당 파일이 없습니다.' 출석
  * 파일 있는 경우 -> 파일 내용을 출력
* 해당 파일 읽기 작업 종료 메시지 출력

```python
# 파일이 없는 경우
try:
    f = open('nooofile.txt')
except FileNotFoundError:
    print('해당 파일이 없습니다.')
else:
    print('파일을 읽기 시작합니다.')
    print(f.read())
    print('파일을 모두 읽었습니다.')
    f.close()
finally:
    print('파일 읽기를 종료합니다.')
    
해당 파일이 없습니다.
파일 읽기를 종료합니다.   

#파일이 존재하는 경우

파일을 읽기 시작합니다.
파일내용
파일을 모두 읽었습니다.
파일 읽기를 종료합니다.
```



#### 에러 메시지 처리 (as)

as 키워드를 활용하여 원본 에러 메시지를 사용할 수 있음

* 예외를 다른 이름에 대입

```python
[][-1]

IndexError                                Traceback (most recent call last)
Input In [27], in <module>
----> 1 [][-1]

IndexError: list index out of range
```

```python
try:
    empty_list = []
    print(empty_list[-1])
except IndexError as err:
    print(f'{err}, 오류가 발생했습니다.')
    
list index out of range, 오류가 발생했습니다.    
```



### Error Occur

예외 발생 시키기

#### raise statement

<u>raise를 통해 예외를 강제로 발생</u>

raise<표현식>(메시지)

: 예외 타입 지정 (주어지지 않을 경우 현재 스코프에서 활성화된 마지막 예외를 다시 일으킴)

```python
raise

---------------------------------------------------------------------------
RuntimeError                              Traceback (most recent call last)
Input In [29], in <module>
----> 1 raise

RuntimeError: No active exception to reraise
```

```python
raise ValueError('값 에러 발생')

---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
Input In [30], in <module>
----> 1 raise ValueError('값 에러 발생')

ValueError: 값 에러 발생
```

```python
try:
    raise ValueError('hi')
except ValueError as err:
    print(err)
else:
    pass
finally:
    pass
    
hi
```





#### assert 

assert를 통해 예외를 강제로 발생

assert는 상태를 검증하는데 사용되며, 무조건 AssertionError가 발생

<u>일반적으로 디버깅 용도로 사용</u>

assert<표현식>,<메시지>

<u>: False인 경우 Assertion Error</u>

```python
assert len([1]) == 1, '길이가 1이 아닙니다.'

# 오류 발생하지 않음
```



```python
assert len([1,2]) == 1, '길이가 1이 아닙니다.'
---------------------------------------------------------------------------
AssertionError                            Traceback (most recent call last)
Input In [31], in <module>
----> 1 assert len([1,2]) == 1, '길이가 1이 아닙니다.'

AssertionError: 길이가 1이 아닙니다.
```



Python 실행

##### raise vs assert

raise : 실제 프로덕션 코드에서 활용

assert :  특정 조건이 거짓이면 발생. 디버깅 및 테스트에서 활용

* -O 옵션으로 실행하는 경우, assert문과 \__debug__에 따른 조건부 코드를 제거 후 실행
