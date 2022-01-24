```python
dic_list = [{'age' : 20, 'location' : '서울'}, {'age' : 30, 'location' : '경기'}]
# list안에 모든 object가 들어갈 수 있다.

# '서울'이라는 정보를 꺼내고 싶다.
dic_list[0]		#dictionary
print(dic_list[0]['location'])		# 자료가 없으면 error
print(dic_list[0].get('location'))	# 자료가 없어도 error 나지 않음

# 30이라는 정보를 꺼내고 싶다.
print(dic_list[1]['age'])
```

immutable한 아이들이 hash 함수를 통과하면 같은 값으로 나오기때문에

set이나 dictionary의 key에는 imutable이 올 수 있다.(str, int, tuple)

hash가 안되기 때문에 dictionary의 키에 들어갈 수 없는 것

```python
dic = {
    'dic_list' : [{'age' : 20, 'location' : '서울'}, {'age' : 30, 'location' : '경기'}], 
    'list' : ['1', '2', '3'], 
    1 : 'integer', 
    (1, 2) : 'tuple'
}

# 30을 뽑고 싶다.
print(dic.get('dic_list')[1].get('age'))

30
```



Q. 입력된 문자의 중앙 글자를 뽑는 함수

```python
def get_middle_char(word):
    l = len(word) // 2
    
    if len(word) % 2:
        res = word[l]
    else:
        res = word[l-1:l+1]
    return res

print(get_middle_char('model'))
print(get_middle_char('coding'))

d
di
```



Q. 여러 인자를 받아 평균을 구하는 함수

```python
def func(*args):
    s = 0
    l = 0
    for i in args:
        s += i
        l += 1
    res = s / l
    return res
```



Q. Dictionary로 이루어지 List의 합 구하는 함수

```python
def dict_list_sum(args):
    s = 0
    for arg in args:
        s += arg['age']
    return s

dict_list_sum([{'name' : 'kim', 'age' : 12},
              {'name' : 'lee', 'age' : 4}])
```



Q. 2차원 List의 전체 합 구하기

```python
def all_list_sum(args):
    s = 0
    for i in args:
        for j in i:
            s += j
    return s

all_list_sum([[1], [2, 3], [4, 5, 6], [7, 8, 9, 10]])
```



**map**

```python
n, m = map(int, input().split())

print(n, m)
print(type(n), type(m))

3 5
<class 'int'> <class 'int'>
```

```python
list_a = [1, 2, 3, 4, 5]
list_b = map(lambda x : x**2, list_a)
print(list(map(lambda x : x**2, list_a)))# 눈으로 보기 위해 list

[1, 4, 9, 16, 25]

#list로 map을 안 감싸고 사용도 가능
for i in list_b:
    print(i)
    
1
4
9
16
25
```

```python
numbers = [1, 2, 3]
# 위의 변수 numbers를 문자열 '123'으로 만드세요. (join 메서드 활용)
print(''.join(map(str,numbers)))
print(type(''.join(map(str,numbers))))

123
<class 'str'>
```



**import**

```python
import random

ramdom.choice()
```

```python
import random as r
r.choice()

# 만약 random이라는 함수를 만들때에도 r과 random으로 구분
def random(x):
    return
```

```python
from math import pi as p, isclose as close	#함수 이름 지정가능

print(p)
print(close(1, 1.000000001))
```



**enumerate**

```python
list_a = [1, 2, 3, 4, 5, 6]
for idx, i in enumerate(list_a):
    print(idx, ":", i)
    
0 : 1
1 : 2
2 : 3
3 : 4
4 : 5
5 : 6
```

```python
names = ['개똥이', '철수', '짱구', '훈이']

for idx, name in enumerate(names, 10):
    print(idx, name)

10 개똥이
11 철수
12 짱구
13 훈이
```



**all() 함수 만들기**

```python
def my_all(elements):
    for element in elements:
        element:
            pass
        else:
            return False
    else:
        return True
```



**else**

```python
for i in []:
    print(1)
else:			# break없이 for문이 정상적으로 끝날 때
    print(2)
    
2
```



Q. 자릿수 더하기(재귀)

```python
def sum_of_digit(number):
    
    if number < 10:
        return number
    
    else:
        return (number % 10) + sum_of_digit(number//10)
```

피보나치수열

```python
def fib(n):
    if n < 2:
        return n
    else:
        return fib(n-1) + fib(n-2)
```

```python
def fib_loop(n):
    if n < 2:
        return n
    
    result = [0, 1]
    for i in range(2, n+1): # list에 0의 값이 포함되어 있기 때문에 자리를 차지해서 +1만큼 계산을 더함.
        result.append(result[i-1] + result[i-2])
        # result.append(result[len(result)-1] + result[len(result)-2])
    return result[-1] # list 의 마지막 값 출력
```





**dictionary 접근**

```python
dict.get(key, default)

d['a'] 			#=> keyError
d.get('a') 		#=> None
```

**dictionary 순회**

```python
dictionary에서 for를 활용하는 4가지 방법
# 0. dictionary 순회 (key 활용)
for key in dict:
    print(key)
    print(dict[key])


# 1. `.keys()` 활용
for key in dict.keys():
    print(key)
    print(dict[key])


# 2. `.values()` 활용
# 이 경우 key는 출력할 수 없음
for val in dict.values():
    print(val)


# 3. `.items()` 활용	튜플로 구성된 결과
for key, val in dict.items():
    print(key, val)
```



```python
# Key가 숫자인 딕셔너리를 만들고 싶다면, 아래와 같이 사용해야합니다.
print(dict([(1, 1), (2, 2)]))
print(dict(((1,1), (2,2))))

{1: 1, 2: 2}
{1: 1, 2: 2}
```



print 활용하기

```python
print('첫번째 문장')
print('두번째 문장', end='_')
print('세번째 문장', '네번째 문장')
print('다섯번째 문장', '마지막 문장', sep='/', end='끝!')

첫번째 문장
두번째 문장_세번째 문장 네번째 문장
다섯번째 문장/마지막 문장끝!
```

```python
print('hi', '안녕', 'Guten Tag', 'gonnichiwa', sep=',')
```



join

```python
numbers = [1, 2, 3]
s_number =''.join(str(i) for i in numbers)
print(s_number)

123
```



map & lambda

```python
# 세제곱의 결과를 나타내는 함수가 있습니다.
def cube(n):
    return n ** 3

numbers = [1, 2, 3]

new_numbers = list(map(cube, numbers))
new_numbers2 = list(map(lambda x : x**3 , numbers))

print(new_numbers)
print(new_numbers2)
```



List comprehension

```python
numbers = [1, 2, 3]

[x for x in numbers if x % 2 ]

[1, 3]
```

```python
a = [x for x in range(3)]
b = [x**2 for x in [1,2,3,4,5,6]]
c = [x**2 for x in [1,2,3,4,5,6] if x%2]

print(a)
print(b)
print(c)

[0, 1, 2]
[1, 4, 9, 16, 25, 36]
[1, 9, 25]
```



Dictionary comprehension

```python
##### Dictionary comprehension
{key : value for <변수> in <iterable>}

{key : value for <변수> in <iterable> if <조건식>}

iterable에서 dict를 생성할 수 있습니다.
```

```python
{키: 값 for 요소 in iterable}

dict({키: 값 for 요소 in iterable})
```

```python
cubic_dict = {}

for number in range(1,4):
    cubic_dict[number] = number**3
cubic_dict

# Dictionary Comprehension
{number:number**3 for number in range(1,4)}

{1: 1, 2: 8, 3: 27}
{1: 1, 2: 8, 3: 27}
```

zip

```python
girls = ['jane', 'ashley', 'mary']
boys = ['justin', 'eric', 'david']

new_list = list(zip(girls, boys))
print(new_list)

[('jane', 'justin'), ('ashley', 'eric'), ('mary', 'david')]
```



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



**String interpolation**

```python
#%-formating
print('%s, %.2f를 %d라고 해도 될까?' %(a, c, b))

#str.format()
print('{}, {}를 {}라고 해도 될까?'.format(a, c, b))

#f-string
print(f'{a}, {c}를 {b}라고 해도 될까?')

hi, 3.14를 3라고 해도 될까?
hi, 3.14를 3라고 해도 될까?
hi, 3.14를 3라고 해도 될까?
```



#### Conditional Expression

조건 표현식

**삼항 연산자(Ternary Operator)**라고 부르기도 한다.

```python
true_value if <조건식> else false_value

## 절대값
num = int(input('숫자를 입력하세요 : '))

if num >= 0:
    value = num
else:
    value = -num

value = num if num >= 0 else -num # conditional expression으로 나타낸 것
print(value)
```



#### 반복 제어

##### break

반복문을 종료

for문이나 while문에서 빠져나간다.

```python
n = 0
while True:
    if n == 3:
        break
    print(n)
    n += 1
    
0
1
2    
```

```python
for i in range(0,10):
    if i>1:
        print('0과 1만 필요해!')
        break
    print(i)   
    
0
1
0과 1만 필요해!    
```



##### continue

continue문은 continue 이후의 코드를 수행하지 않고, **다음 요소부터 계속(continue)하여** 반복을 수행

```python
for i in range(6):
    if i % 2 == 0:
        continue
        # continue 이후의 코드는 실행되지 않습니다.
    print(f'{i}는 홀수다.')
    
1는 홀수다.
3는 홀수다.
5는 홀수다.    
```



##### pass

아무것도 하지 않는다.

들여쓰기 이후 문장이 필요하나, 프로그램이 특별히 할 일이 없을 때 자리를 채우는 용도로 사용할 수 있다.



pass 와 continue의 차이

```python
# pass
# 0부터 4의 범위를 순회하며 출력하는 반복문 안에서
# 3이 나오는 경우 pass 하는 조건문을 작성해봅시다.

for i in range(0,5):
    if i == 3:
        pass
    print(i)
    
0
1
2
3
4

# continue
# 0부터 4의 범위를 순회하며 출력하는 반복문 안에서 
# 3이 나오는 경우 continue 하는 조건문을 작성해봅시다.

for i in range(0,5):
    if i == 3:
        continue
    print(i) 
    
0
1
2
4    
```



##### for-else

끝까지 반복문을 실행한 이후에 else문을 실행한다.

break를 통해 중간에 종료되는 경우 else문은 실행되지 않는다.

```python
name = 'apple'
for i in name:
    if i == 'b':
        print('b!')
        break
else:
    print('b가 없습니다.')
    
b가 없습니다.
```

```python
for char in 'banana':
    if char == 'b':
        print('b!')
        break
else:
    print('b가 없습니다.')
    
b!    
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



chr(a)는 숫자를 아스키로

ord(a)는 아스키를 숫자로
