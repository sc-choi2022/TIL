### Operator

연산자

**Arithmetic Operator**(산술 연산자)

**Comparison Operator**(비교 연산자)

**Logical Operator**(논리 연산자)

**In-place Operator**(복합 연산자)

**Identity Operator**(식별 연산자)

**Membership Operator**(멤버십 연산자)

**Sqeuence Type Operator**(시퀀스형 연산자)

**Indexing/Slicing**(기타)



#### Arithmetic Operator

기본적인 사칙연산 및 수식 계산

| 연산자 |          내용          |
| :----: | :--------------------: |
|   +    |          덧셈          |
|   -    |          뺄셈          |
|   *    |          곱셈          |
|   /    | 나눗셈 <u>\* float</u> |
|   //   |           몫           |
|   **   |        거듭제곱        |
|   %    |         나머지         |
| divmod |   몫, 나머지 * tuple   |



```python
print(5 / 2)
print(4 / 2)
print(5 // 2)
print(int(5/2))
print(5 % 2)
print(divmod(5, 2))

quotient, remainder = divmod(5, 2)
print(quotient, remainder)

2.5
2.0
2
2
1
(2, 1)
2 1
```



#### Comparison Operator

값을 비교하여, True / False 값을 리턴함

| 연산자 |            내용             |
| :----: | :-------------------------: |
|   <    |            미만             |
|   <=   |            이하             |
|   >    |            초과             |
|   >=   |            이상             |
|   ==   |            같음             |
|   !=   |          같지않음           |
|   is   |    객체 아이덴티티(OOP)     |
| is not | 객체 아이덴티티가 아닌 경우 |

\* OOP 객체 아이덴티티 : 메모리의 저장된 위치가 동일한 가를 확인하는 것



```python
print(3 > 6)
print(3.0 == 3)
print(3 >= 0)
print('3' != 3)
print('Hi' == 'hi')

# variable가 비어 있는지 확인할 때 x is None을 권장
x = 3
print(x is None)

False
True
True
True
False

False
```



#### Logical Operator

일반적으로 비교연산자와 함께 사용됨

| 연산자  |              내용              |
| :-----: | :----------------------------: |
| A and B |     A와 B 모두 True : True     |
| A or B  |    A와 B 모두 False : False    |
|   Not   | True를 False로, False를 True로 |



**and**

```python
print(True and True)
print(True and False)
print(False and True)
print(False and False)

True
False
False
False
```



**or**

```python
print(True or True)
print(True or False)
print(False or True)
print(False or False)

True
True
True
False
```



**not**

```python
print(not True)
print(not 0)

False
True
```



논리 연산자는 비교 연산자와 함께 사용 가능합니다.

```python
num = 100
num >= 100 and num % 3 == 1
```



Logical Operator 단축평가

```python
print('a' and 'b')

b

print('a' or 'b')

a

vowels = 'aeiou'
print('a' and 'b' in vowels)
print('b' and 'a' in vowels)

False
True

print(3 and 5)
print(3 and 0)
print(0 and 3)
print(0 and 0)

5
0
0
0

print(5 or 3)
print(3 or 0)
print(0 or 3)
print(0 or 0)

5
3
3
0
```



#### In-place Operator

복합 연산자는 연산과 대입이 함께 이뤄짐

| 연산자  |    내용    |
| :-----: | :--------: |
| a += b  | a = a + b  |
| a -= b  | a = a - b  |
| a *= b  | a = a * b  |
| a /= b  | a = a / b  |
| a //= b | a = a // b |
| a %= b  | a = a % b  |
| a **= b | a = a ** b |

```python
cnt = 0
while cnt < 5:
    print(cnt)
    cnt += 1
    
0
1
2
3
4    
```



#### Identity Operator

is 연산자를 통해 동일한 Object인지 확인

OOP에서 추가 학습

```python
a = 3
b = 3
print(a is b)
print(id(a))
print(id(b))

True
1337067727216
1337067727216
```

```python
a = 257
b = 257
print(a is b)
print(id(a))
print(id(b))

False
1337183723696
1337183724048
```



#### Membership Operator

in과 not in 으로 포함 여부 확인

```python
list_a = [3,2]
print(1 in list_a)

False
```

```python
tuple_a = (1, 2, 'hi')
print(5 in tuple_a)

False
```

```python
print(-3 in range(3))

False
```

```python
print('a' in 'apple')

True
```

```python
print('b' in 'apple')

False
```



#### Sqeuence Type Operator

##### 산술연산자 (+)

Sqeuence을 연결(concatenation)할 수 있습니다.

```python
tuple_a = (1,2)
tuple_b = ('a',)
tuple_c = tuple_a + tuple_b
print(tuple_c)

(1, 2, 'a')
```

```python
print(range(1)+range(2,5))

TypeError                                 Traceback (most recent call last)
Input In [161], in <module>
----> 1 print(range(1)+range(2,5))

TypeError: unsupported operand type(s) for +: 'range' and 'range'
```

```python
print('12'+'a')

12a
```



##### 반복 연산자 (*)

Sqeuence을 반복할 수 있습니다.

```python
list_zero = [0]
print(list_zero*8)

[0, 0, 0, 0, 0, 0, 0, 0]
```

```python
tuple_a = (1,2,)
print(tuple_a * 3)

(1, 2, 1, 2, 1, 2)
```

```python
print(range(1)*3)

TypeError                                 Traceback (most recent call last)
Input In [165], in <module>
----> 1 print(range(1)*3)

TypeError: unsupported operand type(s) for *: 'range' and 'int'
```

```python
'hi' * 3

'hihihi'
```



#### Indexing/Slicing

`[]`를 통한 값을 접근하고, `[:]`을 통해 슬라이싱할 수 있습니다.



##### Indexing

Sqeuence의 특정 Index 값에 접근 할 수 있습니다.

해당 인덱스가 없는 경우 IndexError가 발생합니다. 

```python
list_a = [1,2,3]
print(list_a[2])

3
```

```python
tuple_a = (1,2,3,)
print(tuple_a[0])

1
```

```python
r = range(3)
print(r[2])

2
```

```python
str_a = 'abc'
print(str_a[0])

a
```

```python
str_a = 'apple'
print(str_a[99])

IndexError                                Traceback (most recent call last)
Input In [1], in <module>
      1 str_a = 'apple'
----> 2 print(str_a[99])

IndexError: string index out of range
```



##### Slicing

Sequence[start:end[:step]]

Sqeuence의 특정 단위로 슬라이싱 할 수 있습니다.

```python
print([1, 2, 3, 4][1:4])
print((1, 2, 3)[:2])
print(range(10)[5:8])
print('abcd'[2:4])

[2, 3, 4]
(1, 2)
range(5, 8)
cd
```



시퀀스를 `k` 간격으로 슬라이싱 할 수 있습니다.

```python
print([1, 2, 3, 4][0:4:2])

[1, 3]

s = 'abcdefghi'
print(s[:3])
print(s[5:])
print(s[::])
print(s[::-1])


abc
fghi
abcdefghi
ihgfedcba
```

```python
print([1, 2, 3, 5][0:4:2])
print((1, 2, 3, 5)[0:4:2])
print(range(10)[1:5:3])
print('abcdefg'[1:3:2])

[1, 3]
(1, 3)
range(1, 5, 3)
b
```

```python
s = 'abcdefghi'
print(s[2:5])
print(s[-6:-2])
print(s[2:-4])

cde
defg
cde
```



##### set 연산자

```python
A_set = {1, 2, 3, 4}
B_set = {1.0, 2, 3.0, 'Hello', (1, 2, 3)}

print(A_set | B_set) # | 합집합
print(A_set & B_set) # & 교집합
print(A_set - B_set) # - 차집합
print(A_set ^ B_set) # ^ 대칭차
```



#### 연산자 우선순위

1. `()`을 통한 grouping
2. Slicing
3. Indexing
4. 제곱연산자 `**`
5. 단항연산자 `+`, `-` (음수/양수 부호)
6. 산술연산자 `*`, `/`, `%`
7. 산술연산자 `+`, `-`
8. 비교연산자, `in`, `is`
9. `not`
10. `and`
11. `or`

```python
'apple'[0] in 'sales' and -3**3*0 > 4%2

False
```

