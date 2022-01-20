

## Container

여러 개의 값을 담을 수 있는 객체

<u>서로 다른 자료형을 저장</u> 가능



#### Container분류

Container

* Sequence Container(시퀀스형,순서가 있는(ordered) 데이터)
  * List(가변형)
  * Tuple(불변형)
  * Range(불변형)
  * String(불변형)
* Non-sequence Contatiner(순서가 없는(unodered) 데이터)
  * Set(가변형)
  * Dictionary(가변형)

**순서가 있다(orderd) != 정렬되어 있다(sorted)**

순서가 있다 예) 2314

정렬되어 있다 예) 1234 or 4321



#### Sequence Container

특정 위치의 데이터를 가리킬 수 있습니다.

##### List

: 순서를 가지는 0개 이상의 객체를 참조하는 자료형

**순서가 있는 가변자료형**

대괄호 [] 혹은 list()을 통해 생성

```python
my_list = []
my_place = ['서울','경기','대전']
your_list = list(my_list)
```



List는 순서를 가지고 있기 때문에 Index를 통해 접근 가능하다.

```python
print(my_place[1])

경기
```



예시

```python
basket = ['A','B',['apple','kiwi','mango']]
print(len(basket))
print(basket[2])
print(basket[2][1])
print(basket[2][-1][2])

3
['apple', 'kiwi', 'mango']
kiwi
n
```



##### Tuple

: 순서를 가지는 0개 이상의 객체를 참조하는 자료형

**순서가 있는 불변 자료형(immutable)**

소괄호 () 혹은 tuple()을 통해 생성

```python
my_tuple = (1,2,3,4)
```



**Tuple 생성 주의사항**

* 항목이 하나로 구성된 tuple은 생성 시 값 뒤에 쉼표를 작성

```python
a = (1)
print(type(a))

<class 'int'>

a = 1,
print(type(a))

<class 'tuple'>

b = 1, 2, 3,
print(type(b))

<class 'tuple'>
```



* 항목이 여러개로 구성된 tuple은 생성 시 값 뒤에 쉼표가 불필요

Tuple는 순서를 가지고 있기 때문에 Index를 통해 접근 가능하다.

```python
a = ('a','b','c')
print(a[2])

c
```



예시

```python
# 함수에서 복수의 값을 반환하는 경우에 tuple로 처리
x, y = 1, 2
print(x,y)

1 2
```



##### Range

: 정수의 시퀀스를 나타내기 위해 사용함.



range(n) :  0부터 n-1까지의 정수 시퀀스

range(n,m) : n부터 m-1까지의 정수 시퀀스

range(n,m,s) : n부터 m-1까지 s씩 증가시킨 정수 시퀀스

```python
range(4)
print(list(range(4))) # 담긴 숫자를 확인하기 위한 방법, 실제 사용에서는 list 불필요
print(type(range(4)))

[0, 1, 2, 3]
<class 'range'>
```



예시

```python
print(list(range(3)))
print(list(range(6,1,-1)))
print(list(range(1,3,-1)))
print(list(range(6,1,1)))

[0, 1, 2]
[6, 5, 4, 3, 2]
[]
[]
```



#### Packing / Unpacking Operator

모든 Sequence Container은 Packing / Unpacking Operator * 를 사용하여 객체의 패킹 또는 언패킹이 가능하다.

cf) * : asterisk



##### Packing

대입문의 좌변 변수에 위치

우변의 Object 수가 좌변의 Variable 수 보다 많을 경우 객체를 순서대로 대입

나머지 항목들은 모두 asterisk 기호 표시된 변수에 **list**로 대입

```python
x, *y = 1, 2, 3, 4
print(x)
print(type(x))

print(y)
print(type(y))

1
<class 'int'>
[2, 3, 4]
<class 'list'>
```



##### Unpacking

argument 이름이 *로 시작하는 경우, argument unpacking이라고 한다.



\* Packing의 경우, list로 대입

\* Unpacking의 경우, **tuple** 형태로 대입

```python
def multiply(x, y, z):
    return x * y * z

numbers = [1, 2, 3]
print(multiply(*numbers))

6
```



###### \* 기호의 구분

Packing / Unpacking 연산자 *

* *가 대입식의 좌측에 위치하는 경우
* *가 단항 연산자로 사용되는 경우
  * 단항 연산자 : 하나의 항을 대상으로 연산이 이루어지는 연산자

산술연산자로서의 *

* *가 이항 연산자로 사용되는 경우
  * 이항 연산자 : 두 개의 항을 대상으로 연산이 이루어지는 연산자



### Non-sequence Contatiner

##### Set

: 순서없이 0개 이상의 해시가능한 객체를 참조하는 자료형

cf) 해시가능 : 해시함수를 통과하면 숫자가 나옴. input값이 같으면 나오는 숫자가 동일

​						이 숫자를 이용해 데이터 상에 있는 위치를 구분

해시 가능한 객체(immutable)만 담을 수 있음

**담고있는 객체를 삽입 변경, 삭제 가능 = 가변 자료형(mutable)**

수학에서의 집합과 동일한 구조를 가짐

* 집합 연산 가능
* 중복된 값이 존재하지 않음

중괄호 {} 혹은 set()을 통해 생성

**<u>빈 Set을 만들기 위해서는 반드시 set()을 활용</u>**

```python
a = {1,2,3}
print(type(a))

blank = {}
print(type(blank))

blank = set()
print(blank)

<class 'set'>
<class 'dict'>
set()
```



Set은 순서를 가지고 있지 않기 때문에 Index를 통해 접근 불가능하다.

```python
print({1,2,3}[0])

TypeError                                 Traceback (most recent call last)
Input In [9], in <module>
----> 1 print({1,2,3}[0])

TypeError: 'set' object is not subscriptable
```



Set의 활용

Set을 활용하면 다른 Container의 중복된 값을 제거할 수 있다.

**<u>Set을 사용하는 순간 순서가 사라진다.</u>**

```python
area_list = ['서울', '서울', '경기', '대전', '대전']
len(set(area_list))

3
```



Set 집합 연산자

```python
set_a = {1, 2, 3}
set_b = {3, 6, 9}
s1 = set_a - set_b
print(s1)

{1, 2}
```

```python
set_a = {1, 2, 3}
set_b = {3, 6, 9}
a1 = set_a | set_b
print(a1)

{1, 2, 3, 6, 9}
```

```python
set_a = {1, 2, 3}
set_b = {3, 6, 9}
b1 = set_a & set_b
print(b1)

{3}
```



##### Dictionary

: 순서 없이 key-value 쌍으로 이루어진 Object를 참조하는 자료형



Dictionary의 key는 해시가능한 immutable(불변 자료형)만 가능

* String, Integer, Float, Boolean, Tuple, Range

Dictionary의 value는 어떠한 형태도 가능



중괄호 {} 혹은 dict()을 통해 생성

key를 통해 value에 접근

```python
dict_a = {}
print(type(dict_a))

dict_b = dict()
print(type(dict_b))

dict_c = {'a':'사과', 'b':'벌', 'c':'사탕'}
print(dict_c)
print(dict_c['c'])

<class 'dict'>
<class 'dict'>
{'a': '사과', 'b': '벌', 'c': '사탕'}
사탕
```



<u>dictionary에 중복된 key는 존재할 수 없습니다.</u>

```python
dict_a = {1: 1, 2: 2, 3: 3, 1: 4}
print(dict_a)

{1: 4, 2: 2, 3: 3}
```



dictionary의 .keys() 메소드를 활용하여 key를 확인

```python
area = {'서울':'02','경기':'031'}
print(area.keys())
print(type(area.keys()))

dict_keys(['서울', '경기'])
<class 'dict_keys'>
```



dictionary의 .values() 메소드를 활용하여 value를 확인

```python
area = {'서울':'02','경기':'031'}
print(area.values())
print(type(area.values()))

dict_values(['02', '031'])
<class 'dict_values'>
```



dictionary의 .items() 메소드를 활용하여 key, value를 확인

```python
area = {'서울':'02','경기':'031'}
print(area.items())
print(type(area.items()))

dict_items([('서울', '02'), ('경기', '031')])
<class 'dict_items'>
```

