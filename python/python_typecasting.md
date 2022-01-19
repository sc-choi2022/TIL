## Typecasting

형 변환, 자료형 변환

파이썬에서는 데이터 현태는 서로 변환 가능함

**Implicit** : 암시적 형 변환

**Explicit** : 명시적 형 변환



### Implict Typecasting

사용자가 의도하지 않고, 파이썬 내부적으로 자료현을 변환 하는 경우

bool

```python
print(True + 3)

4
```



Numeric type(int, float, complex)

```python
print(3 + 5.0)
print(type(3 + 5.0))
print(3 + 4j +5)
print(type(3 + 4j +5))

8.0
<class 'float'>
(8+4j)
<class 'complex'>
```



### Explict Typecasting

사용자가 특정 함수를 활용하여 의도적으로 자료형을 변환 하는 경우



#### **int**

str, float

단, 형식에 맞는 문자열만 정수로 변환 가능

```python
# 문자열은 암시적 타입 변환이 되지 않음. 명시적 타입 변환 필요
print('3' + 4)
print(int('3') + 4)

# 정수 형식이 아닌 경우 타입 변환 불가능
print('3.5' + 5)

TypeError                                 Traceback (most recent call last)
Input In [4], in <module>
----> 1 print('3' + 4)

TypeError: can only concatenate str (not "int") to str

7

TypeError                                 Traceback (most recent call last)
Input In [6], in <module>
----> 1 print('3.5' + 5)

TypeError: can only concatenate str (not "int") to str
```



#### **float**

str, int

단, 형식에 맞는 문자열만 실수로 변환 가능

```python
# 문자열은 암시적 타입 변환이 되지 않음. 명시적 타입 변환 필요
print('3.5' + 3.5)
print(float('3.5') + 3.5)

# 정수 형식 타입 변환 가능
print(float('3'))

# float 형식이 아닌 경우 타입 변환 불가능
print(float('3/4') + 5.3)

TypeError                                 Traceback (most recent call last)
Input In [7], in <module>
----> 1 print('3.5' + 3.5)

TypeError: can only concatenate str (not "float") to str
    

7.0

ValueError                                Traceback (most recent call last)
Input In [9], in <module>
----> 1 print(float('3/4') + 5.3)

ValueError: could not convert string to float: '3/4'
```



#### **str**

int, float, list, tuple, dict



### Container Typecasting

Range와 Dictionary로 변환 불가능

Dictionary는 key만 나온다.

**list**

```python
l = [1, 2, 3, 4]
str(l)

'[1, 2, 3, 4]'

tuple(l)

(1, 2, 3, 4)

set(l)

{1, 2, 3, 4}

range(l)

TypeError                                 Traceback (most recent call last)
Input In [14], in <module>
      1 l = [1, 2, 3, 4]
----> 2 range(l)

TypeError: 'list' object cannot be interpreted as an integer
    
    
dict(l)

TypeError                                 Traceback (most recent call last)
Input In [15], in <module>
      1 l = [1, 2, 3, 4]
----> 3 dict(l)

TypeError: cannot convert dictionary update sequence element #0 to a sequence
```



**tuple**

```python
t = (1, 2, 3, 4)
str(t)

'(1, 2, 3, 4)'

list(t)

[1, 2, 3, 4]

set(t)

{1, 2, 3, 4}

range(t)

---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Input In [17], in <module>
      1 t = (1, 2, 3, 4)
----> 3 range(t)

TypeError: 'tuple' object cannot be interpreted as an integer
    
dict(t)

TypeError                                 Traceback (most recent call last)
Input In [18], in <module>
      1 t = (1, 2, 3, 4)
----> 3 dict(t)

TypeError: cannot convert dictionary update sequence element #0 to a sequence
```



**range**

```python
r = range(1, 5)
str(r)

'range(1, 5)'

list(r)

[1, 2, 3, 4]

set(r)

{1, 2, 3, 4}

tuple(r)

(1, 2, 3, 4)

dict(r)

TypeError                                 Traceback (most recent call last)
Input In [23], in <module>
      1 r = range(1, 5)
----> 2 dict(r)

TypeError: cannot convert dictionary update sequence element #0 to a sequence
```



**set**

```python
s = {1, 2, 3, 4}
str(s)

'{1, 2, 3, 4}'

list(s)

[1, 2, 3, 4]

tuple(s)

(1, 2, 3, 4)

range(s)

TypeError                                 Traceback (most recent call last)
Input In [28], in <module>
      1 s = {1, 2, 3, 4}
----> 2 range(s)

TypeError: 'set' object cannot be interpreted as an integer

dict(s)

TypeError                                 Traceback (most recent call last)
Input In [29], in <module>
      1 s = {1, 2, 3, 4}
----> 2 dict(s)

TypeError: cannot convert dictionary update sequence element #0 to a sequence
```



**dictionary**

dictionary는 key만 나온다.

```python
d = {'name': 'sandy', 'year': 2020}
str(d)

"{'name': 'sandy', 'year': 2020}"

list(d)

['name', 'year']

tuple(d)

('name', 'year')

set(d)

{'name', 'year'}

range(d)

TypeError                                 Traceback (most recent call last)
Input In [34], in <module>
----> 1 range(d)

TypeError: 'dict' object cannot be interpreted as an integer
```

