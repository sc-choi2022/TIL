# Contol Statement

제어문

Python은 기본적으로 위에서부터 아래로 순차적으로 명령을 수행

특정 상황에 따라 코드를 선택적으로 실행(분기/ 조건)하거나 계속하여 실행 (반복)하는 제어가 필요함.

* flow chart로 표현이 가능함.
* 순차적인 코드의 흐름을 제어하는 것



### Conditional Statement

#### if

조건문은 True/False을 판단할 수 있는 조건식과 함께 사용

```python
if <expression>:
    <코드 블럭>
else:			# else에는 expression이 들어갈 수 없다.
    <코드 블럭>
```

expression에는 일반적으로 참/거짓에 대한 조건식

**들여쓰기**를 유의



```python
a = 5
if a > 5:
    print('5 초과')
else:
    print('5 이하')
print(a)
```



#### elif

```python
if <expression>:
    <코드 블럭>
elif <expression>:
    <코드 블럭>
elif <expression>:
    <코드 블럭>    
elif <expression>:
    <코드 블럭>
else:				# else에는 expression이 들어갈 수 없다.
    <코드 블럭>
```

```python
dust = int(input('점수를 입력하세요 : '))
if dust>150:
    print('매우 나쁨')
elif dust>80:
    print('나쁨')
elif dust>30:
    print('보통')
elif dust<=30:
    print('좋음')
print('미세먼지 확인 완료!')
```



#### Nested Conditional Statement

```python
if <expression>:
    <코드 블럭>
    if <expression>:
        <코드 블럭>
elif <expression>:
    <코드 블럭>
else :
    <코드 블럭>
```

```python
dust = int(input('점수를 입력하세요 : '))
if dust>150:
    print('매우 나쁨')
    if dust>300:
        print('실외 활동을 자제하세요.')
elif dust>80:
    print('나쁨')
elif dust>30:
    print('보통')
elif 0<=dust<=30:
    print('좋음')
elif dust<0:
    print('값이 잘못 되었습니다.')
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



### Loop Statement

반복문



#### While 문

조건식이 참(`True`)인 경우 반복적으로 코드를 실행한다.

종료조건에 해당하는 코드를 통해 반복문을 종료시켜야 함.

```python
while <조건식>:
    <코드 블럭>
```



<u>주의사항</u>

while 문 역시 조건식 뒤에 콜론(:)이 반드시 필요하다

실행될 코드 블럭은 4spaces로 들여쓰기를 한다.
반드시 종료조건을 설정해야 한다.

```python
a = 0
while a<5:
    print(a)
    a = a + 1
print('끝')

0
1
2
3
4
끝
```



#### for 문

순회가능한 객체(iterable)의 요소들를 모두 순회하면 종료 (별도의 종료조건이 필요 없음)

```python
for <임시변수> in <순회가능한데이터(iterable)>:
    <코드 블럭>
```



```python
for a in range(1,3):
    print(a)
print('끝')

1
2
끝
```



##### Dictionary 순회

dictionary는 기본적으로 key를 순회하며, key를 통해 값을 활용

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



##### Enumerate 순회

인덱스(index)와 값(value)을 함께 활용 가능

```python
members = ['민수', '영희', '철수']

# enumerate() 에 의해 반환되는 인덱스와 값(value)를 함께 출력하는 for 반복문을 작성해봅시다.
for idx, member in enumerate(members):
    print(idx, member)
    
0 민수
1 영희
2 철수

print(enumerate(members))
print(list(enumerate(members)))
print(list(enumerate(members))[0])
print(type(list(enumerate(members))[0]))

<enumerate object at 0x000001576F5F56C0>
[(0, '민수'), (1, '영희'), (2, '철수')]
(0, '민수')
<class 'tuple'>
```



##### List Comprehension

List Comprehension은 표현식과 제어문을 통해 리스트를 생성한다.

여러 줄의 코드를 한 줄로 줄일 수 있다.

```python
[expression for 변수 in iterable]

list(expression for 변수 in iterable)
```

```python
cubic_list = []
for number in range(1, 4):
    cubic_list.append(number ** 3)
print(cubic_list)

[1, 8, 27]
```



##### Dictionary comprehension

```python
{key : value for <변수> in <iterable>}

{key : value for <변수> in <iterable> if <조건식>}
```

```python
iterable에서 dict를 생성할 수 있습니다.

{키: 값 for 요소 in iterable}

dict({키: 값 for 요소 in iterable})
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

