### 함수

Decomposition

Abstraction

기능하는 코드 조각

필요시에만 호출하여 간편히 사용



#### Cumstom Function

구현되어 있는 함수가 없는 경우, 사용자가 직접 함수를 작성 가능

```python
def function_nume(parameter):
    # code block
    return ruturning_Value
```



### 함수를 사용해야 하는 이유

Built-in Function : 내장함수

* 코드 중복 방지
* 재사용 용이



### 함수 기본 구조

Define & Call(선언과 호출)

Input(입력)

Doc-String(문서화)

Scope(범위)

Output(결과값)



#### Define & Call

함수의 선언은 **def 키워드**를 활용함

들여쓰기를 통해 **Function body**(실행될 코드 블록)을 작성함

* Docstring은 함수 body 앞에 선택적으로 작성 가능
  * 작성 시 반드시 첫 번째 문장에 문자열 ''' '''

함수는 parameter을 넘겨줄 수 있음

함수는 동작 후 return을 통해 결과값을 전달함

```python
def <함수이름>(parameter1, parameter2):
    <코드 블럭>
    return value
```



함수는 함수명() 으로 호출

```python
# parameter가 없는 경우
def foo():
    return True

def add(x, y):
    return x + y

foo()
add(2,3)
```



#### Output

값에 따른 함수의 종류

**Void function**

: 명시적인 return 값이 없는 경우, None을 반환하고 종료

**Value returning function**

: 함수 실행 후, return 문을 통해 값을 반환하고 함수 종료

```python
a = print('hello')
b = float('3.5')

print(a, b)

hello
None 3.5
```



**두 개 이상의 값 반환**

반환 값으로 tuple 사용

```python
def minus_and_product(x, y):
    return x - y
	return x * y

print(minus_and_product(4, 5))

-1
# 함수는 항상 단일한 값만을 반환

# 반환 값으로 튜플 사용
def minus_and_product(x, y):
    return x - y, x * y

print(minus_and_product(4, 5))

(-1, 20)
```



**값 반환 외의 return문의 용도**

​	return을 하게 되면, 값 반환 후에 함수가 바로 종료된다.

​	함수를 빠져나갈 때, return문을 사용한다.



<u>**주의**</u>

* return은 함수 안에서만 사용되는 <u>키워드</u>
* print는 출력을 위해 사용되는 <u>함수</u>
* REPL(Read-Eval-Print Loop) 환경에서는 마지막으로 작성된 코드의 리턴 값을 보여주므로 같은 동작을 하는 것으로 착각할 수 있다.

```python
# Void function example
def void_product(x, y):
    print(f'{x} x {y} = {x*y}')
    
void_product(4, 5)
ans = void_product(4, 5)
print(ans)

# Value returning function
def value_returning_product(x, y):
    return x*y

value_returning_product(4, 5)
ans = value_returning_product(4, 5)
print(ans)

4 x 5 = 20
4 x 5 = 20
None
20
```



return

- return x - None
- return o - 하나의 object를 반환



#### Input

##### Parameter와 Argument

Parameter : 함수를 실행할 때, 함수 내부에서 사용되는 식별자

Argument :  함수를 호출할 때, 넣어주는 값

```python
def say_anything(anything): # parameter = anything 이름
    print(f'hello {anything}')

say_anything('python') # argument : 'python' 값

hello python
```



**Argument**

: 함수 호출 시 함수의 parameter를 통해 전달되는 값

Argument는 소괄호 안에 할당 func_name(argument)

* 필수 Argument : 반드시 전달되어야 하는 argument
* 선택 Argument : 값을 전달하지 않아도 되는 경우는 기본 값이 전달



**Positional Arguments**

기본적으로 함수 호출 시 Argument는 위치에 따라 함수 내에 전달된다.

```python
def add(x, y):
    return x + y

add(2, 3) # x = 2, y = 3
```



**Keyword Arguments** (호출)

직접 변수의 이름으로 특정 Argument를 전달할 수 있음

Keyword Argument 다음에 Positional Argument를 활용할 수 없음

```python
def add(x, y):
    return x + y

add(x = 2, y = 5) # x = 2, y = 5
add(2, y = 5) # x = 2, y = 5
add(x = 2, 5) # x = 2, y = 5 
			  # SyntaxError :positional argument follows keyword argument
    
  Input In [5]
    add(x = 2, 5) # x = 2, y = 5
                ^
SyntaxError: positional argument follows keyword argument
```



**Default Arguments Value** (정의)

기본값을 지정하여 함수 호출 시 argument값을 설정하지 않도록 함

정의된 것보다 적은 개수의 argument들로 호출 될 수 있음

```python
def add(x, y =0):
    return x + y

add(2) # x = 2, y = 0
```



**정해지지 않은 여러 개의 Arguments 처리**



**Positional Arguments Packing/Unpacking**

Positional Arguments Packing/Unpacking 연산자(*)

: 여러 개의 Positional Arguments를 하나의 필수 parameter로 받아서 사용

몇 개의 Positional Argument를 받을지 모르는 함수를 정의할 때 유용

```python
def add(*args):
    for arg in args:
        print(arg)
        
add(2)
add(2, 3, 4, 5)

2
2
3
4
5
```

```python
a = [1, 2, 3]

def func1(x):
    for i in x:
        print(i)
func1(a)        

def func2(*x):
    for i in x:
        print(i)
    	print(type(x))
func2(a)        

1
2
3
[1, 2, 3]
<class 'tuple'>
```



Positional Arguments Packing/Unpacking 연산자(**)

: 함수가 임의의 개수 Argument를 Keyword Argument로 호출될 수 있도록 지정

Argument들은 딕셔너리로 묶여 처리되며, parameter에 **를 붙여 표현

```python
def family(**kwargs):
    for key, value in kwargs.items():
        print(key, ":", value)
        
family(father = 'John', mother = 'Jane', me = 'John Jr.')
# father, mother은 dictionary를 정의하겠다는 것이 아닌 이름과 값을 묶어서 주겠다는 것

father : John
mother : Jane
me : John Jr.
```



<u>**함수 정의 주의 사항**</u>

```python
def greeting(name = 'john deo', age):

#기본 argument 값을 가지는 argument다음에 기본 값이 없는 argument로 정의할 수 없음
#SyntaxError: non-default argument follows default argument

add(x=3, 5)

#keyword argument 다음에 positional argument를 활용할 수는 없음
#SyntaxError: positional argument follows keyword argument
```



#### Scope

함수는 코드 내부에 **local scope**를 생성하고 그 외의 공간인 **global scope**과 구분

local scope :

​	global scope : 코드 어디에서든 참조할 수 있는 공간

​	local scope : 함수가 만든 scope. 함수 내부에서만 참조 가능

variable

​	global variable : global scope에 정의된 변수

​	local variable : local scope에 정의된 변수



**life scope**

변수는 각자의 life scope(변수 수명주기)가 존재

built-in scope

: Python이 실행된 이후부터 영원히 유지

global scope

: 모듈이 호출된 시점 이후 혹은 인터프리터(.py)가 끝날 때까지 유지

local scope

: 함수가 호출될 때 생성되고, 함수가 종료될 때까지 유지(return이 될때까지)

```python
def func():
    a = 20
    print('local',a)

func()
print('global',a)

# a는 local scope에서만 존재

local 20
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
Input In [1], in <module>
      5     print('local',a)
      7 func()
----> 8 print('global',a)

NameError: name 'a' is not defined
```



**Name Resolution**

파이썬에서 사용되는 실별자들은 <u>namespace</u>에 저장되어 있음

아래와 같은 순서로 이름을 찾아나가며 LEGB Rule이라고 부름

* Local scope : 함수
* Enclosed scope : 특정 함수의 상위 함수
* Global scope : 함수 밖의 변수, Import 모듈
* Bulit-in scope : 파이썬 안에 내장되어 있는 함수 또는 속성

즉, 함수 내에서는 바깥 Scope의 변수에 접근 가능하나 <u>수정은 할 수 없음</u>



예시1

```python
a = 0
b = 1
def enclosed():
    a = 10
    c = 3
    def local(c):
        print(a, b, c)
    local(300)
    print(a, b, c)
    
enclosed()
print(a, b)

10 1 300
10 1 3
0 1
```



예시2

```python
print(sum)
print(sum(range(2)))
sum = 5
print(sum)
print(sum(range(2)))

<built-in function sum>
1
5
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Input In [8], in <module>
      7 sum = 5
      8 print(sum)
----> 9 print(sum(range(2)))

TypeError: 'int' object is not callable
```



##### global문

밖에 있는 변수를 black box안에서 조작하고 싶다. global keyword를 이용하여 사용할 수 있다.

현재 코드 블록 전체에 적용되며, 나열된 식별자(Identifiers, 이름)이 global variable임을 나타냄

* global에 나열된 이름은 같은 코드 블록에서 global 앞에 등장할 수 없음
* global에 나열된 이름은 parameter, for 루프 대상, 클래스/함수 정의 등으로 정의되지 않아야 함

```python
# 함수 내부에서 글로벌 변수 변경하기
a = 10
def func1():
    global a
    a = 3		# local scope에서 global 변수 값의 변경
    			# global키워드를 사용하지 않으면, local scope에 a 변수가 생성됨
print(a)
func1()
print(a)

10
3
```



global 변수 사용 제한 예시

global 변수를 사용할 때는 반드시 가장 상단에 사용하기 전에 선언해주어야한다.

```python
a = 10
def func1():
    print(a)	# 반드시 a를 사용하기 전에 global a
    global a
    a = 3
    
print(a)
func1()
print(a)

a = 10
def func2(a):
    global a
    a = 3
    
print(a)
func1(3)
print(a)

Input In [12]
    global a
    ^
SyntaxError: name 'a' is used prior to global declaration

```



##### nonlocal

: global을 제외하고 가장 가까운 (둘러 싸고 있는) scope의 변수를 연결하도록 함

nonlocal에 나열된 이름은 같은 코드 블록에서 nonlocal앞에 등장할 수 없음

nonlocal에 나열된 이름은 parameter, for 루프 대상, 클래스/함수 정의 등으로 정의되지 않아야 함

<u>global과는 달리 이미 존재하는 이름과 연결만 가능함</u>

```python
x = 0
def func1():
    x = 1
    def func2():
        nonlocal x
        x = 2
    func2()
    print(x)
    
func1()
print(x)

2
0
```



##### nonlocal, global 비교

```python
# 선언된 적 없는 변수의 활용
def func1():
    global out		# global는 없는 global out을 만들 수 있다.
    out = 3
    
func1()
print(out)

3

def func2():
    def func3():
        nonlocal y	# global과 다르게 없는 nonlocal y을 만들 수 없다.
        y = 2
	func3()        
    print(y)
    
func2()

Input In [16]
    nonlocal y	# global과 다르게 없는 nonlocal y을 만들 수 없다.
    ^
SyntaxError: no binding for nonlocal 'y' found
```



##### 주의

<u>기본적으로 함수에서 선언된 변수는 Local scope에 생성되며, 함수 종료 시 사라짐</u>

<u>해당 scope에 변수가 없는 경우 LEGB rule에 의해 이름을 검색함</u>

* 변수에 접근은 가능하지만, 해당 변수를 수정할 수는 없음
* 값을 할당하는 경우 해당 scope의 이름공간에 새롭게 생성되기 때문
* **단, 함수 내에서 필요한 상위 scope 변수는 argument로 넘겨서 활용할 것 (클로져\*제외)**
  * 클로저랸? 어떤 함수 내부에 중첩된 형태로써 외부 scope 변수에 접근 가능한 함수

상위 scope에 있는 변수를 수정하고 싶다면 <u>global, nonlocal</u> 키워드를 활용가능

* 단, 코드가 복잡해지면서 변수의 변경을 추적하기 어렵고, 예기치 못한 오류가 발생
* 가습적 사용하지 않는 것을 권장하며, **함수로 값을 바꾸고자 한다면 항상 argument로 넘기고 리턴값을 사용하는 것을 추천**



##### 범위 확인하기

globals()와 locals()

namespace(global, local, builtin)을 dictionary로 정리

* globals() : global, local, builtin 정보 모두 <u>dict</u> 형태로 정리
* locals() : locals()가 실행되어지는 함수 내의 local namespace들을 정리

```python
a_var = range(2)
def locals_test():
    b_var = 3
    c_var = 'hi'
    d_var = locals()
    print(d_var)
locals_test()

e_var = globals()
print(e_var)

{'b_var': 3, 'c_var': 'hi'}
{'__name__': '__main__', '__doc__': 'Automatically created module for IPython interactive environment', '__package__': None, '__loader__': None, '__spec__': None, '__builtin__': <module 'builtins' (built-in)>, '__builtins__': <module 'builtins' (built-in)>, '_ih': ['', "# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\ndef greeting(name = 'john deo', age):", '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\nadd(x=3, 5)', '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\na = 0\nb = 1\ndef enclosed():\n    a = 10\n    b = 3\n    def local(c):\n        print(a, b, c)\n\tlocal(300)\n    print(a, b, c)\n    \nenclosed()\nprint(a, b)', '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\na = 0\nb = 1\ndef enclosed():\n    a = 10\n    b = 3\n    def local(c):\n        print(a, b, c)\n    local(300)\n    print(a, b, c)\n    \nenclosed()\nprint(a, b)', '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\na = 0\nb = 1\ndef enclosed():\n    a = 10\n    b = 3\n    def local(c):\n        print(a, b, c)\n    local(300)\n    print(a, b, c)\n    \nenclosed()\nprint(a, b)', '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\na = 0\nb = 1\ndef enclosed():\n    a = 10\n    b = 3\n    def local(c):\n        print(a, b, c)\n    local(300)\n    print(a, b, c)\n    \nenclosed()\nprint(a, b)', '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\na = 0\nb = 1\ndef enclosed():\n    a = 10\n    c = 3\n    def local(c):\n        print(a, b, c)\n    local(300)\n    print(a, b, c)\n    \nenclosed()\nprint(a, b)', '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\nprint(sum)\nprint(sum(range(2)))\nsum = 5\nprint(sum)\nprint(sum(range(2)))', '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.', '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\na = 10\ndef fun1():\n    global a\n    a = 3\t\t# local scope에서 global 변수 값의 변경\n    \t\t\t# global키워드를 사용하지 않으면, local scope에 a 변수가 생성됨\nprint(a)\nfunc1()\nprint(a)', '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\na = 10\ndef func1():\n    global a\n    a = 3\t\t# local scope에서 global 변수 값의 변경\n    \t\t\t# global키워드를 사용하지 않으면, local scope에 a 변수가 생성됨\nprint(a)\nfunc1()\nprint(a)', '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\na = 10\ndef func1():\n    print(a)\t# 반드시 a를 사용하기 전에 global a\n    global a\n    a = 3\n    \nprint(a)\nfunc1()\nprint(a)\n\na = 10\ndef func2(a):\n    global a\n    a = 3\n    \nprint(a)\nfunc1(3)\nprint(a)', '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\nx = 0\ndef func1():\n    x = 1\n    def func2():\n        nonlocal x\t\n        x = 2\n    func2()\n    print(x)\n    \nfunc1()\nprint(X)', '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\nx = 0\ndef func1():\n    x = 1\n    def func2():\n        nonlocal x\n        x = 2\n    func2()\n    print(x)\n    \nfunc1()\nprint(x)', '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\ndef func1():\n    global out\t\t# global는 없는 global out을 만들 수 있다.\n    out = 3\n    \nfunc1()\nprint(out)\n\ndef func2():\n    def func3():\n        nonlocal y\t# global과 다르게 없는 nonlocal y을 만들 수 없다.\n        y = 2\n\tfunc3()        \n    print(y)\n    \nfunc2()', '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\ndef func1():\n    global out\t\t# global는 없는 global out을 만들 수 있다.\n    out = 3\n    \nfunc1()\nprint(out)\n\ndef func2():\n    def func3():\n        nonlocal y\t# global과 다르게 없는 nonlocal y을 만들 수 없다.\n        y = 2\n    func3()        \n    print(y)\n    \nfunc2()', '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\n\ndef func2():\n    def func3():\n        nonlocal y\t# global과 다르게 없는 nonlocal y을 만들 수 없다.\n        y = 2\n    func3()        \n    print(y)\n    \nfunc2()', "# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\n\na_var = range(2)\ndef locals_test():\n    b_var = 3\n    c_var = 'hi'\n    d_var = locals()\n    print(d_var)\nlocals_test()\n\ne_var = globals()\nprint(e_var)"], '_oh': {}, '_dh': [WindowsPath('C:/Users/choiy/Desktop/ssafy7/handsout_MINE/0119/실습자료')], 'In': ['', "# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\ndef greeting(name = 'john deo', age):", '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\nadd(x=3, 5)', '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\na = 0\nb = 1\ndef enclosed():\n    a = 10\n    b = 3\n    def local(c):\n        print(a, b, c)\n\tlocal(300)\n    print(a, b, c)\n    \nenclosed()\nprint(a, b)', '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\na = 0\nb = 1\ndef enclosed():\n    a = 10\n    b = 3\n    def local(c):\n        print(a, b, c)\n    local(300)\n    print(a, b, c)\n    \nenclosed()\nprint(a, b)', '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\na = 0\nb = 1\ndef enclosed():\n    a = 10\n    b = 3\n    def local(c):\n        print(a, b, c)\n    local(300)\n    print(a, b, c)\n    \nenclosed()\nprint(a, b)', '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\na = 0\nb = 1\ndef enclosed():\n    a = 10\n    b = 3\n    def local(c):\n        print(a, b, c)\n    local(300)\n    print(a, b, c)\n    \nenclosed()\nprint(a, b)', '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\na = 0\nb = 1\ndef enclosed():\n    a = 10\n    c = 3\n    def local(c):\n        print(a, b, c)\n    local(300)\n    print(a, b, c)\n    \nenclosed()\nprint(a, b)', '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\nprint(sum)\nprint(sum(range(2)))\nsum = 5\nprint(sum)\nprint(sum(range(2)))', '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.', '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\na = 10\ndef fun1():\n    global a\n    a = 3\t\t# local scope에서 global 변수 값의 변경\n    \t\t\t# global키워드를 사용하지 않으면, local scope에 a 변수가 생성됨\nprint(a)\nfunc1()\nprint(a)', '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\na = 10\ndef func1():\n    global a\n    a = 3\t\t# local scope에서 global 변수 값의 변경\n    \t\t\t# global키워드를 사용하지 않으면, local scope에 a 변수가 생성됨\nprint(a)\nfunc1()\nprint(a)', '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\na = 10\ndef func1():\n    print(a)\t# 반드시 a를 사용하기 전에 global a\n    global a\n    a = 3\n    \nprint(a)\nfunc1()\nprint(a)\n\na = 10\ndef func2(a):\n    global a\n    a = 3\n    \nprint(a)\nfunc1(3)\nprint(a)', '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\nx = 0\ndef func1():\n    x = 1\n    def func2():\n        nonlocal x\t\n        x = 2\n    func2()\n    print(x)\n    \nfunc1()\nprint(X)', '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\nx = 0\ndef func1():\n    x = 1\n    def func2():\n        nonlocal x\n        x = 2\n    func2()\n    print(x)\n    \nfunc1()\nprint(x)', '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\ndef func1():\n    global out\t\t# global는 없는 global out을 만들 수 있다.\n    out = 3\n    \nfunc1()\nprint(out)\n\ndef func2():\n    def func3():\n        nonlocal y\t# global과 다르게 없는 nonlocal y을 만들 수 없다.\n        y = 2\n\tfunc3()        \n    print(y)\n    \nfunc2()', '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\ndef func1():\n    global out\t\t# global는 없는 global out을 만들 수 있다.\n    out = 3\n    \nfunc1()\nprint(out)\n\ndef func2():\n    def func3():\n        nonlocal y\t# global과 다르게 없는 nonlocal y을 만들 수 없다.\n        y = 2\n    func3()        \n    print(y)\n    \nfunc2()', '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\n\ndef func2():\n    def func3():\n        nonlocal y\t# global과 다르게 없는 nonlocal y을 만들 수 없다.\n        y = 2\n    func3()        \n    print(y)\n    \nfunc2()', "# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\n\na_var = range(2)\ndef locals_test():\n    b_var = 3\n    c_var = 'hi'\n    d_var = locals()\n    print(d_var)\nlocals_test()\n\ne_var = globals()\nprint(e_var)"], 'Out': {}, 'get_ipython': <bound method InteractiveShell.get_ipython of <ipykernel.zmqshell.ZMQInteractiveShell object at 0x000002644CE8B2B0>>, 'exit': <IPython.core.autocall.ZMQExitAutocall object at 0x000002644CE34640>, 'quit': <IPython.core.autocall.ZMQExitAutocall object at 0x000002644CE34640>, '_': '', '__': '', '___': '', '_i': '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\n\ndef func2():\n    def func3():\n        nonlocal y\t# global과 다르게 없는 nonlocal y을 만들 수 없다.\n        y = 2\n    func3()        \n    print(y)\n    \nfunc2()', '_ii': '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\ndef func1():\n    global out\t\t# global는 없는 global out을 만들 수 있다.\n    out = 3\n    \nfunc1()\nprint(out)\n\ndef func2():\n    def func3():\n        nonlocal y\t# global과 다르게 없는 nonlocal y을 만들 수 없다.\n        y = 2\n    func3()        \n    print(y)\n    \nfunc2()', '_iii': '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\ndef func1():\n    global out\t\t# global는 없는 global out을 만들 수 있다.\n    out = 3\n    \nfunc1()\nprint(out)\n\ndef func2():\n    def func3():\n        nonlocal y\t# global과 다르게 없는 nonlocal y을 만들 수 없다.\n        y = 2\n\tfunc3()        \n    print(y)\n    \nfunc2()', '_i1': "# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\ndef greeting(name = 'john deo', age):", '_i2': '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\nadd(x=3, 5)', '_i3': '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\na = 0\nb = 1\ndef enclosed():\n    a = 10\n    b = 3\n    def local(c):\n        print(a, b, c)\n\tlocal(300)\n    print(a, b, c)\n    \nenclosed()\nprint(a, b)', '_i4': '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\na = 0\nb = 1\ndef enclosed():\n    a = 10\n    b = 3\n    def local(c):\n        print(a, b, c)\n    local(300)\n    print(a, b, c)\n    \nenclosed()\nprint(a, b)', 'a': 10, 'b': 1, 'enclosed': <function enclosed at 0x000002644CF043A0>, '_i5': '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\na = 0\nb = 1\ndef enclosed():\n    a = 10\n    b = 3\n    def local(c):\n        print(a, b, c)\n    local(300)\n    print(a, b, c)\n    \nenclosed()\nprint(a, b)', '_i6': '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\na = 0\nb = 1\ndef enclosed():\n    a = 10\n    b = 3\n    def local(c):\n        print(a, b, c)\n    local(300)\n    print(a, b, c)\n    \nenclosed()\nprint(a, b)', '_i7': '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\na = 0\nb = 1\ndef enclosed():\n    a = 10\n    c = 3\n    def local(c):\n        print(a, b, c)\n    local(300)\n    print(a, b, c)\n    \nenclosed()\nprint(a, b)', '_i8': '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.\n\nprint(sum)\nprint(sum(range(2)))\nsum = 5\nprint(sum)\nprint(sum(range(2)))', 'sum': 5, '_i9': '# check.py 파일에 짝수, 홀수를 판별하는 함수를 작성해봅시다.\n# 1. n을 매개변수로 받아 홀수인지를 판단하는 odd 함수를 작성해 주세요.\n# 2. return은 n이 홀수라면 True를, 아니라면 False를 return 합니다.', '_i10': '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\na = 10\ndef fun1():\n    global a\n    a = 3\t\t# local scope에서 global 변수 값의 변경\n    \t\t\t# global키워드를 사용하지 않으면, local scope에 a 변수가 생성됨\nprint(a)\nfunc1()\nprint(a)', 'fun1': <function fun1 at 0x000002644CE69550>, '_i11': '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\na = 10\ndef func1():\n    global a\n    a = 3\t\t# local scope에서 global 변수 값의 변경\n    \t\t\t# global키워드를 사용하지 않으면, local scope에 a 변수가 생성됨\nprint(a)\nfunc1()\nprint(a)', 'func1': <function func1 at 0x000002644EA523A0>, '_i12': '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\na = 10\ndef func1():\n    print(a)\t# 반드시 a를 사용하기 전에 global a\n    global a\n    a = 3\n    \nprint(a)\nfunc1()\nprint(a)\n\na = 10\ndef func2(a):\n    global a\n    a = 3\n    \nprint(a)\nfunc1(3)\nprint(a)', '_i13': '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\nx = 0\ndef func1():\n    x = 1\n    def func2():\n        nonlocal x\t\n        x = 2\n    func2()\n    print(x)\n    \nfunc1()\nprint(X)', 'x': 0, '_i14': '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\nx = 0\ndef func1():\n    x = 1\n    def func2():\n        nonlocal x\n        x = 2\n    func2()\n    print(x)\n    \nfunc1()\nprint(x)', '_i15': '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\ndef func1():\n    global out\t\t# global는 없는 global out을 만들 수 있다.\n    out = 3\n    \nfunc1()\nprint(out)\n\ndef func2():\n    def func3():\n        nonlocal y\t# global과 다르게 없는 nonlocal y을 만들 수 없다.\n        y = 2\n\tfunc3()        \n    print(y)\n    \nfunc2()', '_i16': '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\ndef func1():\n    global out\t\t# global는 없는 global out을 만들 수 있다.\n    out = 3\n    \nfunc1()\nprint(out)\n\ndef func2():\n    def func3():\n        nonlocal y\t# global과 다르게 없는 nonlocal y을 만들 수 없다.\n        y = 2\n    func3()        \n    print(y)\n    \nfunc2()', 'out': 3, '_i17': '# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\n\ndef func2():\n    def func3():\n        nonlocal y\t# global과 다르게 없는 nonlocal y을 만들 수 없다.\n        y = 2\n    func3()        \n    print(y)\n    \nfunc2()', '_i18': "# 3. n을 매개변수로 받아 짝수인지를 판단하는 even 함수를 작성해 주세요.\n# 4. return은 n이 짝수라면 True를, 아니라면 False를 return 합니다.\n\n\na_var = range(2)\ndef locals_test():\n    b_var = 3\n    c_var = 'hi'\n    d_var = locals()\n    print(d_var)\nlocals_test()\n\ne_var = globals()\nprint(e_var)", 'a_var': range(0, 2), 'locals_test': <function locals_test at 0x000002644EA52670>, 'e_var': {...}}
```



#### Doc-String

함수의 문서화 :  함수나 클래스의 설명

Docstring(Documentation String)

Jupyter notebook에서 함수에 커서를 놓고 shift + tab 

```python
def foo():
    '''
    이 함수는 foo입니다.
    docstring으로 함수나 클래스의 기능을 설명합니다.
    '''
    
foo.__doc__    
```

```python
print(print.__doc__)

print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)

Prints the values to a stream, or to sys.stdout by default.
Optional keyword arguments:
file:  a file-like object (stream); defaults to the current sys.stdout.
sep:   string inserted between values, default a space.
end:   string appended after the last value, default a newline.
flush: whether to forcibly flush the stream.
    
help(print)

Help on built-in function print in module builtins:

print(...)
    print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
    
    Prints the values to a stream, or to sys.stdout by default.
    Optional keyword arguments:
    file:  a file-like object (stream); defaults to the current sys.stdout.
    sep:   string inserted between values, default a space.
    end:   string appended after the last value, default a newline.
    flush: whether to forcibly flush the stream.
```



##### Naming Convention

좋은 함수와 parameter 이름 짓는 방법

* 상수 이름은 영문 전체를 대문자 (예) PI = 3.141592)
* 클래스 및 예외의 이름은 각 단어의 첫 글자만 영문 대문자
* 이외 나머지는 소문자 또는 밑줄로 구분한 소문자 사용 > 함수

스스로를 설명

* 함수의 이름만으로 어떠한 역할을 하는 함수인지 파악 가능해야 함
* 어떤 기능을 수행하는지, 결과 값으로 무엇을 반환하는지 등

약어 사용을 지양

* 보편적으로 사용하는 약어를 제외하고 가급적 약어 사용을 지양

```python
how_are_you_doing	# snake case
HowAreYou			# pascal case
howAreYou			# camel case
```



### 함수 응용

#### Built-in Functions

파이썬 인터프리터에는 항상 사용할 수 있는 많은 함수와 형(type)이 내장되어 있다.



##### map

map(function, iterable) function: 사용하고 싶은 함수의 이름

:순회 가능한 데이터구조(iterable)의 모든 요소에 함수(function)를 적용하고, 그 결과를 map object로 반환

<u>function : 각 요소에 적용하고 싶은 함수 이름</u>

```python
numbers = [1, 2, 3]
result = map(str, numbers)
print(result, type(result))

<map object at 0x000002644D024D60> <class 'map'>
#enumerate에서 본 적 있다. 많은 것들을 하나씩 꺼낼 수 있게 담은 통
list(result)

['1', '2', '3']	#list 형변환을 통해 결과 직접 확인
```



<u>map(str,input().split())</u> 와 <u>list(map(int,input().split()))</u> 정말 많이 사용

```python
def add x:
    a, b = x
    return a + b

a = list(map(add,[[1, 2],[3, 4]]))
print(a)

[3, 7]
```

예: input 값들을 숫자로 바로 활용하고 싶을 때

```python
n, m = map(int, input().split())	# 20 20

print(n, m)		# 20 20
print(type(n),type(m))	# <class 'int '> <class 'int'>
```



##### filter

filter(function, iterable)

순회 가능한 데이터구조(iterable)의 모든 요소에 함수(function)을 적용하고 그 결과가 True인 것들을 filter object로 반환

```python
def odd(n):
    return n%2					# True/False 를 반환 
numbers = [1, 2, 3]
result = filter(odd, numbers)	# True가 있는 것만 반환
print(result, type(result))

list(result)
```



##### zip

zip(*iterables)

: 복수의 iterable을 모아 **tuple**을 원소로 하는 zip object를 반환

```python
girls = ['jane', 'ashley']
boys = ['justin', 'eric']
pair = zip(girls, boys)
print(pair, type(pair))

<zip object at 0x000002644EAB45C0> <class 'zip'>

list(pair)
[('jane', 'justin'), ('ashley', 'eric')]
```



```python
a = ['a', 'b', 'c']
b = [1, 2, 3]
print(list(zip(a, b)))

[('a', 1), ('b', 2), ('c', 3)]
```

```python
a = ['a', 'b', 'c']
b = [1, 2, 3]
c = ['x', 'y', 'z']
print(list(zip(a, b, c)))

[('a', 1, 'x'), ('b', 2, 'y'), ('c', 3, 'z')]
```



만약 하나의 list가 길다면 짧은 것을 기준으로 zip이 진행된다.

```python
a = ['a', 'b', 'c']
b = [1, 2, 3, 4, 5]
print(list(zip(a, b)))

[('a', 1), ('b', 2), ('c', 3)]
```



```python
from pprint import pprint
a = [[1, 2, 3, 4, 5]]*5
pprint(a)
print()

b = list(zip(*a))
pprint(b)
print()

c = list(zip(*a))[::-1]
pprint(c)
print()

d = list(zip(*a[::-1]))
pprint(d)
print()

[[1, 2, 3, 4, 5],
 [1, 2, 3, 4, 5],
 [1, 2, 3, 4, 5],
 [1, 2, 3, 4, 5],
 [1, 2, 3, 4, 5]]

[(1, 1, 1, 1, 1),		# transpose
 (2, 2, 2, 2, 2),		
 (3, 3, 3, 3, 3),
 (4, 4, 4, 4, 4),
 (5, 5, 5, 5, 5)]

[(5, 5, 5, 5, 5),		# 반시계 방향
 (4, 4, 4, 4, 4),
 (3, 3, 3, 3, 3),
 (2, 2, 2, 2, 2),
 (1, 1, 1, 1, 1)]

[(1, 1, 1, 1, 1),		# 시계 방향
 (2, 2, 2, 2, 2),
 (3, 3, 3, 3, 3),
 (4, 4, 4, 4, 4),
 (5, 5, 5, 5, 5)]

```



##### lambda 함수

lambda [parameter] : 표현식

: 표현식을 계산한 결과값을 반환하는 함수로, 이름이 없는 함수여서 <u>익명함수</u>라고도 불림

특징 :

return문을 가질 수 없음

간편 조건문 외 조건문이나 반복문을 가질 수 없음

장점:

함수를 정의해서 사용하는 것보다 간결하게 사용 가능

def를 사용할 수 없는 곳에서도 사용가능

```python
def triangle_area(b, h):
    return 0.5 * b * h
triangle_area(5, 6)

triangle_area = lambda b, h : 0.5 * b * h
triangle_area(5, 6)
```

```python
func = lambda x : x+1
print(func(1))

2
```



**filter와 lambda**

```python
def odd(n):
    return n % 2

print(list(filter(odd, range(5))))

[1, 3]

print(list(filter(lambda n: n%2, range(5))))

[1, 3]
```



##### recursive function

재귀함수

: <u>자기 자신을 호출하는 함수</u>

무한한 호출을 목표로 하는 것이 아니며, 알고리즘 설계 및 구현에서 유용하게 활용

* 알고리즘 중 재귀 함수로 로직을 표현하기 쉬운 경우가 있음(e.g) 점화식))
* 변수의 사용이 줄어들며, 코드의 가독성이 높아짐

<u>1개 이상의 base case(종료되는 상황)가 존재하고, 수렴하도록 작성</u>

```python
# Factorial n!
# recursive function
def factorial(n):
    if n == 0 or n == 1:
        return 1
    else:
        return n * factorial(n-1)        
factorial(4)        

# for문으로도 작성가능
def fact(n):
    result = 1
    while n > 1:
        result *= n
        n -= 1
    return result     
fact(4)
```



<u>재귀 함수의 주의 사항</u>

재귀 함수는 <u>base case</u>에 도달할 때까지 함수를 호출함

메모리 스택이 넘치게 되면(stack overflow) 프로그램이 동작하지 않게 됨

파이썬에서는 <u>최대 재귀 깊이</u>(maximum recursion depth)가 1,000번으로, 호출 횟수가 이를 넘어가게 되면 Recursion Error 발생



**반복문과 재귀 함수 비교**

알고리즘 자체가 <u>재귀적인 표현</u>이 자연스러운 경우 재귀 함수를 사용함

재귀 호출은 <u>변수 사용을 줄여줄 수 있음</u>

재귀 호출은 <u>입력 값이 커질 수록 연산 속도가 오래 걸림</u>