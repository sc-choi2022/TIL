[toc]



# TypeError

```python
x, y = 1

TypeError                                 Traceback (most recent call last)
Input In [16], in <module>
----> 1 x, y = 1

TypeError: cannot unpack non-iterable int object
```

```python
print = 'hi'
print(5)

TypeError                                 Traceback (most recent call last)
Input In [1], in <module>
      1 print = 'hi'
----> 2 print(5)

TypeError: 'str' object is not callable
```

```python
# immutable

a = 'my string?'
a[-1] = '!

TypeError                                 Traceback (most recent call last)
Input In [41], in <module>
      1 a = 'my string?'
----> 2 a[-1] = '!'

TypeError: 'str' object does not support item assignment
```

```python
print(1+"개")

TypeError                                 Traceback (most recent call last)
Input In [113], in <module>
----> 1 print(1+"개")

TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

```python
print(range(1)+range(2,5))

TypeError                                 Traceback (most recent call last)
Input In [161], in <module>
----> 1 print(range(1)+range(2,5))

TypeError: unsupported operand type(s) for +: 'range' and 'range'
```

```python
print(range(1)*3)

TypeError                                 Traceback (most recent call last)
Input In [165], in <module>
----> 1 print(range(1)*3)

TypeError: unsupported operand type(s) for *: 'range' and 'int'
```

```python
print({1,2,3}[0])

TypeError                                 Traceback (most recent call last)
Input In [9], in <module>
----> 1 print({1,2,3}[0])

TypeError: 'set' object is not subscriptable
```

```python
print('3' + 4)

TypeError                                 Traceback (most recent call last)
Input In [4], in <module>
----> 1 print('3' + 4)

TypeError: can only concatenate str (not "int") to str
```

```python
print('3.5' + 5)

TypeError                                 Traceback (most recent call last)
Input In [6], in <module>
----> 1 print('3.5' + 5)

TypeError: can only concatenate str (not "int") to str
```

```python
range(l)

TypeError                                 Traceback (most recent call last)
Input In [14], in <module>
      1 l = [1, 2, 3, 4]
----> 2 range(l)

TypeError: 'list' object cannot be interpreted as an integer
```

```python
dict(l)

TypeError                                 Traceback (most recent call last)
Input In [15], in <module>
      1 l = [1, 2, 3, 4]
----> 3 dict(l)

TypeError: cannot convert dictionary update sequence element #0 to a sequence
```

```python
print(range(1)+range(2,5))

TypeError                                 Traceback (most recent call last)
Input In [161], in <module>
----> 1 print(range(1)+range(2,5))

TypeError: unsupported operand type(s) for +: 'range' and 'range'
```

```python
print(range(1)*3)

TypeError                                 Traceback (most recent call last)
Input In [165], in <module>
----> 1 print(range(1)*3)

TypeError: unsupported operand type(s) for *: 'range' and 'int'
```

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



# ValueError

```python
x, y = 1, 2, 3

ValueError                                Traceback (most recent call last)
Input In [17], in <module>
----> 1 x, y = 1, 2, 3

ValueError: too many values to unpack (expected 2)
```

```python
complex('1 + 2j')

ValueError                                Traceback (most recent call last)
Input In [36], in <module>
----> 1 complex('1 + 2j')

ValueError: complex() arg is a malformed string
```

```python
a = 'hi'
print(int(a))

ValueError                                Traceback (most recent call last)
Input In [117], in <module>
      1 a = 'hi'
----> 2 print(int(a))

ValueError: invalid literal for int() with base 10: 'hi'
```

```python
a = '3.5'
print(int(a))

ValueError                                Traceback (most recent call last)
Input In [118], in <module>
      1 a = '3.5'
----> 2 print(int(a))

ValueError: invalid literal for int() with base 10: '3.5'
```

```python
print(float('3/4') + 5.3)

ValueError                                Traceback (most recent call last)
Input In [9], in <module>
----> 1 print(float('3/4') + 5.3)

ValueError: could not convert string to float: '3/4'
```





# IndexError

```python
str_a = 'apple'
print(str_a[99])

IndexError                                Traceback (most recent call last)
Input In [1], in <module>
      1 str_a = 'apple'
----> 2 print(str_a[99])

IndexError: string index out of range
```



# KeyError

```python
dic = {1: 2, 2: 3}

print(dic[3])
KeyError                                  Traceback (most recent call last)
Input In [40], in <module>
      2 print(dic[1])
      3 print(dic.get(1))
----> 5 print(dic[3])

KeyError: 3
```

```python
my_dict = {'apple':'사과', 'banana':'바나나'}
data = my_dict.pop('pineapple')
print(data, my_dict)

---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
Input In [62], in <module>
      1 my_dict = {'apple':'사과', 'banana':'바나나'}
----> 2 data = my_dict.pop('pineapple')
      3 print(data, my_dict)

KeyError: 'pineapple'
```



# NameError

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

```python
from check import odd	# check.py 사용
even(4)

True
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
Input In [2], in <module>
      3 from check import odd
----> 4 even(4)

NameError: name 'even' is not defined
```



# SyntaxError

```python
def greeting(name = 'john deo', age):

    Input In [1]
    def greeting(name = 'john deo', age):
                                       ^
SyntaxError: non-default argument follows default argument
```

```python
add(x=3, 5)

  Input In [2]
    add(x=3, 5)
              ^
SyntaxError: positional argument follows keyword argument
```

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

```python
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

