[toc]



# Data

## 순서가 있는 데이터 구조

### String Type

Sequence of characters

* 모든 문자는 str타입



문자열은 '나 "를 활용하여 표기

* 문자열을 묶을 때 동일한 문장부호를 활용
* PEP8에서는 소스코드 내에서 하나의 문장부호를 선택하여 유지하도록 함



#### 문자열 조회/탐색

| 문법        | 설명                                                         |
| ----------- | ------------------------------------------------------------ |
| s.find(x)   | x의 첫 번째 위치를 반환. 없으면, -1을 반환                   |
| s.index(x)  | x의 첫 번째 위치를 반화. 없으면, 오류 발생                   |
| s.isalpha() | 알파벳 문자 여부<br />* 단순 알파벳이 아닌 유니코드 상 Letter (한국어도 포함) |
| s.isupper() | 대문자 여부                                                  |
| s.islower() | 소문자 여부                                                  |
| s.istitle() | 타이틀 형식 여부                                             |

**is가 붙어있다면 boolean 생각하기**



`.find(x)`

x의 **첫 번째 위치**를 반환합니다. 만일 리스트 내에 x가 없으면, `-1`을 반환합니다.

```python
a = 'apple'
```

```python
# find 메서드로 a 문자열에 'p'가 있는지 찾아봅시다.
a.find('p')

1
```

```python
# find 메서드로 a 문자열에 'z'가 있는지 찾아봅시다.
a.find('z')

-1
```



`.index(x)`

x의 **첫 번째 위치**를 반환합니다. 만일 x가 리스트 내에 없으면, 오류가 발생합니다.

```python
a = 'apple'
```

```python
# index 메서드는 찾고자 하는 문자가 문자열 내에 있을 경우, 첫 번째 위치를 반환합니다.
# index 메서드로 a 문자열에서 'p'의 위치를 확인해봅시다.

a.index('p')

1
```

```python
# 찾고자 하는 문자가 문자열 내에 없을 경우, 오류가 발생합니다.
# index 메서드로 a문자열에서 'z'의 위치를 찾고, 오류를 확인해봅시다.

a.index('z')
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
Input In [35], in <module>
      1 # 찾고자 하는 문자가 문자열 내에 없을 경우, 오류가 발생합니다.
      2 # index 메서드로 a문자열에서 'z'의 위치를 찾고, 오류를 확인해봅시다.
----> 4 a.index('z')

ValueError: substring not found
```



`.startswith(x)`, `/.endswith(x)`

`.startswith(x)` : 문자열이 x로 시작하면 True를 반환하고 아니면 False를 반환합니다. 

`.endswith(x)` : 문자열이 x로 끝나면 True를 반환하고 아니면 False를 반환합니다.



#### 검증 메소드

문자열 관련 검증 메소드

```python
'abc'.isalpha()
'ㄱㄴㄷ'.isalpha()

True
True

'Ab'.isupper()
'ab'.islower()
'Title Titile!'.istitle()

False
True
True
```

```python
.isdecimal() ⊆ .isdigit() ⊆ .isnumeric()
```



#### 문자열 변경 메소드

| 문법                         | 설명                                       |
| ---------------------------- | ------------------------------------------ |
| s.replace(old,new[,count])   | 바꿀 대상 글자를 새로운 글자로 바꿔서 반환 |
| s.strip([chars])             | 공백이나 특정 문자를 제거                  |
| s.split([chars])             | 공백이나 특정 문자를 기준으로 분리         |
| 'separator'.join([iterable]) | 구분자로 iterable을 합침                   |
| s.capitalize()               | 가장 첫 번째 글자를 대문자로               |
| s.title()                    | '나 공백 이후를 대문자로                   |
| s.upper()                    | 모두 대문자                                |
| s.lower()                    | 모두 소문자                                |
| s.swapcase()                 | 대<->소문자 변경하여                       |

**.replace(old, new[,count])**

* 바꿀 대상 글자를 새로운 글자로 바꿔서 반환
* count를 지정하면, 해당 개수만큼만 시행

```python
a = 'yaya!'
b = 'wooooowoo'

# replace 메서드를 통해 a의 글자 y를 h로 변경해봅시다.
a.replace('y','h')

'haha!'

# replace 메서드를 통해 b의 글자 o 2개를 _로 변경해봅시다.
b.replace('oo','_')

'w__ow_'
```



**.strip([chars])**

특정한 문자들을 지정하면

* 양쪽을 제거하거나(strip), 왼쪽을 제거하거나(Istrip), 오른쪽을 제거(rstirp)

문자열을 지정하지 않으면 공백을 제거함

```python
a = '   hello!  \n'
b = 'hihihihahahahihi'
c = 'monty python'

# strip 메서드로 a의 양쪽 공백을 제거해봅시다.
a.strip()

'hello!'

# lstrip 메서드로 a의 왼쪽 공백을 제거해봅시다.
a.lstrip()

'hello!  \n'

# rstrip 메서드로 b의 오른쪽에서부터 글자 hi를 제거해봅시다.
b.rstrip('hi')

'hihihihahaha'

# `chars` 파라미터를 지정한 경우, 모든 조합을 이용하여 제거합니다.
# rstrip 메서드로 c의 오른쪽에서부터 글자 ' python'을 제거해봅시다.
c.rstrip('python')

'monty '
```



**.split([chars])**

문자열을 특정한 단위로 나눠 **리스트**로 반환

```python
a = 'a_b_c'

# split 메서드로 _를 기준으로 문자열을 나누어 리스트로 반환해봅시다.
a.split('_')

a = '1 2 3 4 5 6'
print(list(map(int, a.split())))
map(int, input().split())

['a', 'b', 'c']
```

```python
# 사용자의 입력값을 받아 i에 저장합니다.
# 입력받은 문자열을 split 메서드로 공백을 기준으로 나누어 리스트로 반환해봅시다.
i = input().split()
print(i)

123 4 5 6 7
['123', '4', '5', '6', '7']
```



**'separator'.join([iterable])**

**반복가능한(iterable) 컨테이너 요소들**을 separator(구분자)로 합쳐 문자열 반환

```python
'!'.join('happy')
' '.join(['3', '5'])

'h!a!p!p!y'
'3 5'
```



예시

```python
msg = 'hI! Everyone, I\'m happy'
print(msg)
print(msg.capitalize())
print(msg.title())
print(msg.upper())
print(msg.lower())
print(msg.swapcase())

hI! Everyone, I'm happy
Hi! everyone, i'm happy
Hi! Everyone, I'M Happy		#\'뒤도 capital
HI! EVERYONE, I'M HAPPY
hi! everyone, i'm happy
Hi! eVERYONE, i'M HAPPY
```



### List

: 순서를 가지는 0개 이상의 객체를 참조하는 자료형

**순서가 있는 가변자료형**

대괄호 [] 혹은 list()을 통해 생성



#### 리스트 메소드

| 문법                   | 설명                                                         |
| ---------------------- | ------------------------------------------------------------ |
| L.append(x)            | 리스트 마지막에 항목 x를 추가                                |
| L.insert(i, x)         | 리스트 인덱스 i에 항목 x를 삽입                              |
| L.remove(x)            | 리스트 가장 왼쪽에 있는 항목(첫 번째) x를 제거<br />항목이 존재하지 않을 경우, ValueError |
| L.pop()                | 리스트 가장 오른쪽에 있는 항목(마지막)을 반환 후 제거        |
| L.pop(i)               | 리스트의 인덱스 i에 있는 항목을 반환 후 제거                 |
| L.extend(m)            | 순회형 m의 모든 항목들의 리스트 끝에 추가 (+=과 같은 기능)   |
| L.index(x, start ,end) | 리스트에 있는 항목 중 가장 왼쪽에 있는 항목 x의 인덱스를 반환 |
| L.reverse()            | 리스트를 거꾸로 정렬                                         |
| L.sort(...)            | 리스트를 정렬 (개개변수 이용가능)                            |
| L.count(x)             | 리스트에서 항목 x가 몇 개 존재하는지 갯수를 반환             |

**.append(x)**

리스트에 값을 추가함

```python
cafe = ['starbucks', 'tomntoms', 'hollys']
print(cafe)
cafe[2:2] = ['x','a','c']
print(cafe)

['starbucks', 'tomntoms', 'hollys']
['starbucks', 'tomntoms', 'x', 'a', 'c', 'hollys']
```



**.extend(iterable)**

리스트에 iterable의 항목을 추가함

```python
cafe.extend(['wcafe', '빽다방'])
print(cafe)

# += 연산자로 cafe에 ['mc_cafe', 'droptop']를 추가해봅시다.
# 앞서 배운 list concatenate와 동일합니다.
cafe += ['mc_cafe', 'droptop']
print(cafe)

['starbucks', 'tomntoms', 'x', 'a', 'c', 'hollys', 'banapresso', 'wcafe', '빽다방']
['starbucks', 'tomntoms', 'x', 'a', 'c', 'hollys', 'banapresso', 'wcafe', '빽다방', 'mc_cafe', 'droptop']
```

cf)

```python
alpha = ['a'] + ['b']
print(alpha)

['a', 'b']
```



##### .append vs .extend

```python
city = ['boston', 'seoul', 'newyork']

city.append(['brisbane'])
print(city)

city.extend(['sydney'])
print(city)
```

[출력 결과]

```python
['boston', 'seoul', 'newyork', ['brisbane']]

['boston', 'seoul', 'newyork', ['brisbane'], 'sydney']
```

.append의 경우 list안에 값을 추가하는 것으로 'brisbane'을 담은 list를 추가한다.

.extend의 경우 list 자체를 추가하는 것으로 'bristbane'의 값이 list에 추가된다.



**.insert(i,x)**

정해진 위치 `i`에 값x을 추가합니다.

```python
# insert 메서드로 cafe 첫번째에 문자열 start를 넣어봅시다.
cafe = ['starbucks', 'tomntoms']
cafe.insert(0,'start')
print(cafe)

['start', 'starbucks', 'tomntoms']
```

```python
# insert 메서드로 cafe 마지막에 문자열 end를 넣어봅시다.
# 마지막 위치는 len함수를 이용합니다.
cafe.insert(len(cafe), 'end')
print(cafe)

['start', 'starbucks', 'tomntoms', 'end']
```

```python
# insert 메서드로 cafe 길이보다 큰 인덱스에 문자열 !를 넣어봅시다.
# 리스트의 길이를 넘어서는 인덱스는 마지막에 아이템이 추가됩니다.
cafe.insert(100,'!')
print(cafe)

['start', 'starbucks', 'tomntoms', 'end', '!']
```

<u>a.insert(0, x)는 리스트의 처음에 x를 삽입</u>

<u>a.insert(len(a), x) 는 a.append(x) 와 같다.</u>



**.remove(x)**

리스트에서 값이 x인 것 삭제

```python
numbers = [1, 2, 3, 1, 2]

# remove 메서드로 1을 삭제 해봅시다.
numbers.remove(1)
print(numbers)

[2, 3, 1, 2]
```

```python
# remove 메서드로 1을 한 번 더 삭제 해봅시다.
numbers.remove(1)
print(numbers)

[2, 3, 2]
```

```python
# remove는 값이 없으면 오류가 발생합니다.
# remove 메서드로 1을 한 번 더 삭제하여, 확인해봅시다.
numbers.remove(1)
print(numbers)

---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
Input In [37], in <module>
      1 # remove는 값이 없으면 오류가 발생합니다.
      2 # remove 메서드로 1을 한 번 더 삭제하여, 확인해봅시다.
----> 4 numbers.remove(1)
      5 print(numbers)

ValueError: list.remove(x): x not in list
```



**.pop([i])**

정해진 위치 i에 있는 값을 삭제하고, 그 항목을 반환함

i가 지정되지 않으면, 마지막 항목을 삭제하고 반환함

```python
numbers = [1, 2, 3, 4, 5, 6]
```

```python
# pop 메서드로 가장 앞에 있는 숫자를 삭제해봅시다.
# 삭제후 numbers를 출력해봅시다.
numbers.pop(0)
print(numbers)

[2, 3, 4, 5, 6]
```

```python
# pop 메서드로 가장 마지막에 있는 숫자를 삭제하고 결과를 a에 저장합니다.
# 삭제된 숫자와 결과를 모두 출력해봅시다.
a = numbers.pop()
print(a)
print(numbers)

6
[2, 3, 4, 5]
```



**.clear()**

```python
numbers = [1, 2, 3, 4, 5, 6]

# clear 메서드로 리스트의 모든 항목을 삭제합니다.
numbers.clear()
print(numbers)

[]
```



**.index(x)**

x값을 찾아 해당 index 값을 반환

```python
a = [1, 2, 3, 4, 5]
# index 메서드로 숫자 3이 있는 위치를 반환합니다.

a.index(3)
a.index(100)

2
ValueError                                Traceback (most recent call last)
Input In [111], in <module>
      1 # index는 찾는 값이 없으면 오류가 발생합니다.
      2 # index 메서드로 숫자 100이 있는 위치를 확인해봅시다.
----> 4 a.index(100)

ValueError: 100 is not in list
```



**.count(x)**

원하는 값의 개수를 반환

```python
a = [1, 2, 5, 1, 5, 1]
print(a.count(1))

3
```

```python
# 원하는 값을 모두 삭제하려면 다음과 같이 할 수 있습니다.
a = [1, 2, 1, 3, 4]
target_value = 1
for i in range(a.count(target_value)):
    a.remove(target_value)
print(a)

[2, 3, 4]
```



**.sort()**

내장함수 `sorted()` 와는 다르게 **원본 list를 변형**시키고, **`None`**을 return

파라미터로는 `key`와 `reverse`가 있습니다.

```python
lotto = [30, 41, 31, 25, 20, 29]
print(lotto)
print(lotto.sort())
print(lotto)

[14, 19, 15, 31, 40, 44]
None
[14, 15, 19, 31, 40, 44]
```



##### .sort() vs sorted()

 ```python
sample_list = [1, 5, 11, 2, 3, 555]

#sorted()
sorted_sample = sorted(sample_list)
print(sorted_sample)
print(sample_list)

#.sort()
print(sample_list.sort())
print(sample_list)
 ```

[출력 결과]

```python
[1, 2, 3, 5, 11, 555]
[1, 5, 11, 2, 3, 555]

None
[1, 2, 3, 5, 11, 555]
```

cf) sort, sorted 둘 다 매개변수에 reverse=False 로 기본값 인자로 설정됨 

​	 내림차순: reverse 매개변수를 True 로 설정

​	 sort와 마찬가지로, 파라미터 `key`와 `reverse`가 있음

`key`

```python
a = [ [7, 8, 9, 11], [1, 2, 29], [4, 5]]

a.sort()
print(a)

a.sort(key=lambda x : x[-1])
print(a)

[[1, 2, 29], [4, 5], [7, 8, 9, 11]]
[[4, 5], [7, 8, 9, 11], [1, 2, 29]]
```



**.reverse**

list의  element들을 제자리에서 반대로 뒤집음(정렬하는 것이 아님)

```python
classroom = ['Tom', 'David', 'Justin']
print(classroom)

# reverse 메서드로 리스트를 역순으로 만들어줍니다.
print(classroom[::-1])
print(classroom.reverse())
print(classroom)

['Tom', 'David', 'Justin']
['Justin', 'David', 'Tom']
None
['Justin', 'David', 'Tom']
```



##### .reverse() vs reversed()

 `.reverse()` 는 내장함수 `reversed()` 와는 다르게 **원본 list를 변형**시키고, **`None`**을 리턴

```python
lst = ['a', 'b', 'c']
# reverse
lst_reverse = lst.reverse()
print(lst_reverse)
print(lst)

# reversed
lst_reversed = reversed(lst)
print(lst_reversed)
print(list(lst_reversed))
print(lst)

None
['c', 'b', 'a']

<list_reverseiterator object at 0x0000016E73F3CFD0>
['a', 'b', 'c']
['c', 'b', 'a']
```



### Tuple

: 순서를 가지는 0개 이상의 객체를 참조하는 자료형

**순서가 있는 불변 자료형(immutable)**

소괄호 () 혹은 tuple()을 통해 생성



#### 튜플 관련 메소드

* 튜플은 변경할 수 없기 때문에 값에 영향을 미치지 않는 메소드만을 지원
* 리스트 메소드 중 항목을 변경하는 메소드들을 제외하고 대부분 동일



**.index(x[, start[, end]])**

튜플에 있는 항목 중 값이 x 와 같은 첫 번째 인덱스를 돌려준다.

해당하는 값이 없으면, ValueError를 발생한다.

```python
a = ('hello','python','python','django','web')
print(a.index('python'))
print(a.index('algorithm'))

1

---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
Input In [132], in <module>
      1 # index는 찾는 값이 없으면 오류가 발생합니다.
      2 # index 메서드로 algorithm의 위치를 확인하세요.
----> 4 a.index('algorithm')

ValueError: tuple.index(x): x not in tuple
```



**.count(x)**

튜플에서 x 가 등장하는 횟수를 돌려준다.

```python
a = ('hello','python','python','django','web')
print(a.count('python'))

2
```



## 순서가 없는 데이터 구조

### Set

: 순서없이 0개 이상의 해시가능한 객체를 참조하는 자료형

cf) 해시가능 : 해시함수를 통과하면 숫자가 나옴. input값이 같으면 나오는 숫자가 동일

​						이 숫자를 이용해 데이터 상에 있는 위치를 구분

해시 가능한 객체(immutable)만 담을 수 있음

**담고있는 객체를 삽입 변경, 삭제 가능 = 가변 자료형(mutable)**

수학에서의 집합과 동일한 구조를 가짐

* 집합 연산 가능
* 중복된 값이 존재하지 않음

중괄호 {} 혹은 set()을 통해 생성



#### 셋 메소드

| 문법           | 설명                                                         |
| -------------- | ------------------------------------------------------------ |
| s.copy()       | 셋의 얕은 복사본을 반환                                      |
| s.add(x)       | 항목 x가 셋 s에 없다면 추가                                  |
| s.pop()        | 셋 s에서 랜덤하게 항목을 반환하고, 해당 항목을 제거<br />set이 비어 있을 경우, KeyError |
| s.remove(s)    | 항목 x를 셋 s에서 삭제<br />항목이 존재하지 않을 경우, KeyError |
| s.discard(x)   | 항목 x가 셋 s에 있는 경우, 항목 x를 셋s에서 삭제             |
| s.update(t)    | 셋 t에 있는 모든 항목 중 셋s에 없는 항목을 추가              |
| s.clear()      | 모든 항목을 제거                                             |
| s.isdisjoint() | 셋 s가 셋 t의 서로 같은 항목을 하나라도 갖고 있지 않은 경우, True반환 |
| s.issubset()   | 셋 s가 셋 t의 하위 셋인 경우, True 반환                      |
| s.issuperset() | 셋 s가 셋 t의 상위 셋인 경우, False 반환                     |

**.add(elem)**

```python
a = {'사과', '바나나', '수박'}
print(a)
a.add('딸기')
print(a)

{'사과', '바나나', '수박'}
{'사과', '바나나', '딸기', '수박'}
```



**update(\*other)**

```python
a = {'사과', '바나나', '수박'}
a.update({'토마토', '토마토', '딸기'},{'포도', '레몬'})
print(a)

{'포도', '토마토', '사과', '레몬', '딸기', '바나나', '수박'}
```



**.remove(elem)**

셋에서 삭제하고, 없으면 KeyError

```python
a = {'사과', '바나나', '수박'}
print(a)
a.remove('사과')
print(a)
a.remove('애플')
print(a)

{'사과', '바나나', '수박'}
{'바나나', '수박'}
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
Input In [58], in <module>
      6 a.remove('사과')
      7 print(a)
----> 8 a.remove('애플')
      9 print(a)

KeyError: '애플'
```



**.discard()**

셋에서 삭제하고 없어도 에러가 발생하지 않음

```python
a = {'사과', '바나나', '수박'}
a.discard('포도')
a.discard('수박')
print(a)

{'바나나', '사과'}
```



##### .discard(elem) vs .remove(elem)

```python
# .discard(elem)
a = {10, 20, 30}
a.discard(10)
print(a)
a.discard(10)
print(a)

{20, 30}
{20, 30}
```

```python
# .remove(elem)
a = {10, 20, 30}
a.remove(10)
print(a)
a.remove(10)
print(a)

{20, 30}
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
Input In [11], in <module>
      2 a.remove(10)
      3 print(a)
----> 4 a.remove(10)
      5 print(a)

KeyError: 10
```





**.pop()**

**<u>임의</u>**의 원소를 제거해 반환

```python
a = {'사과','바나나','수박'}
print(a)
a.pop()
print(a)

{'바나나', '사과', '수박'}
{'사과', '수박'}

a = {'1', '2', '3'}
print(a)
a.pop()
print(a)

{'2', '3', '1'}
{'3', '1'}
```





##### 셋.pop() vs 리스트.index()

Set의 .pop(): 임의의 원소를 제거해 반환

List의 .indext(): 기본은 마지막



### Dictionary

: 순서 없이 key-value 쌍으로 이루어진 Object를 참조하는 자료형



Dictionary의 key는 해시가능한 immutable(불변 자료형)만 가능

* String, Integer, Float, Boolean, Tuple, Range

Dictionary의 value는 어떠한 형태도 가능



#### 딕셔너리 메소드

| 문법          | 설명                                                         |
| ------------- | ------------------------------------------------------------ |
| s.clear       | 모든 항목을 제거                                             |
| d.copy()      | 딕셔너리 d의 얕은 복사본을 반환                              |
| d.keys()      | 딕셔너리 d의 모든 키를 담은 뷰를 반환                        |
| d.values()    | 딕셔너리 d의 모든 값을 담은 뷰를 반환                        |
| d.items()     | 딕셔너리 d의 모든 키-값의 쌍을 담은 뷰를 반환                |
| d.get(k)      | 키 k의 값을 반환하는데, 키 k가 딕셔너리 d에 있을 경우 None을 반환 |
| d.get(k, v)   | 키 k의 값을 반환하는데, 키 k가 딕셔너리 d에 없을 경우 v을 반환 |
| d.pop(k)      | 키 k의 값을 반환하고 키 k인 항목을 딕셔너리 d에서 삭제하는데,<br />키 k가 딕셔너리 d에 없을 경우 KeyError를 발생 |
| d.pop(k, v)   | 키 k의 값을 반환하고 키 k인 항목을 딕셔너리 d에서 삭제하는데,<br />키 k가 딕셔너리 d에 없을 경우 v를 반환 |
| d.update(...) | 딕셔너리 d의 값을 매핑하여 업데이트                          |



**.get(key[,default])**

key를 통해 value를 가져옴

KeyError가 발생하지 않으며, default 값을 설정할 수 있음**(기본: None)**

```python
my_dict = {'apple':'사과', 'banana':'바나나'}
my_dict['pineapple']

---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
Input In [60], in <module>
      1 # get 메서드 없이 딕셔너리 my_dict의 key 'pineapple'의 value를 출력하는 코드를 실행시켜 오류를 확인해봅시다.
----> 3 my_dict['pineapple']

KeyError: 'pineapple'
```

```python
my_dict = {'apple':'사과', 'banana':'바나나'}
print(my_dict.get('pineapple'))
print(my_dict.get('apple'))
print(my_dict.get('pineapple',0))

None
'사과'
0
```



**.pop(key[,default])**

key가 딕셔너리에 있으면 제거하고 해당 값을 반환

그렇지 않으면 default를 반환

**default값이 없으면 KeyError발생**

```python
my_dict = {'apple':'사과', 'banana':'바나나'}
data = my_dict.pop('apple')
print(data, my_dict)

사과 {'banana': '바나나'}
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

```python
my_dict = {'apple':'사과', 'banana':'바나나'}
data = my_dict.pop('pineapple',0)
print(data, my_dict)

0 {'apple': '사과', 'banana': '바나나'}
```



##### list vs set vs dict

list.pop() - 마지막, index 가능

set.pop() - random(임의의)

dict.pop() - key기준



**.update()**

값을 제공하는 key, value로 덮어쓴다.

```python
my_dict = {'apple':'사과', 'banana':'바나나'}
my_dict.update(apple='사과')		# parameter의 이름 x = 5의 x처럼
print(my_dict)
```



##### .setdefault(key[, default])

`dict.get()`method와 비슷한 동작을 하는 메서드로, key가 딕셔너리에 있으면 value를 돌려준다.

get과 다른 점은 key가 딕셔너리에 없을 경우, default 값을 갖는 key 를 삽입한 후 default 를 반환한다는 점입니다. 만일 default가 주어지지 않을 경우, None 을 돌려준다.

```python
my_dict = {'apple': '사과', 'banana' : '바나나', 'melon' : '멜론'}
my_dict.setdefault('apple')
my_dict.setdefault('pineapple', '파인애플')
print(my_dict)

{'apple': '사과', 'banana': '바나나', 'melon': '멜론', 'pineapple': '파인애플'}
```



##### .pop(key[, default])

key가 딕셔너리에 있으면 제거하고 그 값을 돌려줍니다. 그렇지 않으면 default를 반환한다.

default가 없는 상태에서 해당 key가 딕셔너리에 경우, KeyError가 발생한다.

```python
my_dict = {'apple': '사과', 'banana': '바나나'}
my_dict.pop('apple')
print(my_dict)
my_dict.pop('melon')

{'banana': '바나나'}
KeyError                                  Traceback (most recent call last)
Input In [167], in <module>
      1 # 제거하고자 하는 key가 딕셔너리에 없으면 KeyError가 발생합니다.
      2 # 실행시켜 오류를 확인해봅시다.
----> 3 my_dict.pop('melon')

KeyError: 'melon'

print(my_dict.pop('melon',0))

0
```



##### .update([other])

other 가 제공하는 key,value 쌍으로 딕셔너리를 덮어씁니다. `other` 는 다른 딕셔너리나 key/value 쌍으로 되어있는 모든 iterable을 사용 가능

keyword argument로 업데이트 하는 방법

- 키워드 인자가 지정되면, 딕셔너리는 그 key/value 쌍으로 갱신

```python
my_dict = {'apple': '사과', 'banana': '바나나', 'melon': '멜론'}
my_dict.update({'apple':'사과아'})
print(my_dict)

d = {'mango': '망고', 'watermelon': '수박'}
my_dict.update(d)
print(my_dict)

{'apple': '사과아', 'banana': '바나나', 'melon': '멜론'}
{'apple': '사과아', 'banana': '바나나', 'melon': '멜론', 'mango': '망고', 'watermelon': '수박'}
```





## Shallow Copy & Deep Copy

### Assignment

대입 연산자 (=)

* 리스트 복사 확인하기

```python
original_list = [1, 2, 3]
copy_list = original_list
print(original_list, copy_list)

[1, 2, 3] [1, 2, 3]
```

```python
copy_list[0] = 'hello'
print(original_list, copy_list)

['hello', 2, 3] ['hello', 2, 3]
```

대입 연산자(=)를 통한 복사는 해당 객체에 대한 객체 참조를 복사



### Shallow copy

Slice 연산자 활용하여 같은 원소를 가진 리스트지만 연산된 결과를 복사 (다른 주소)

```python
a = [1, 2, 3]
b = a[:]		# b = list(a)
print(a, b)
b[0] = 5
print(a, b)

[1, 2, 3] [1, 2, 3]
[1, 2, 3] [5, 2, 3]
```



**주의사항**

복사하는 리스트의 원소가 주소를 참조하는 경우

2차원 리스트와 같이 mutable 객체 안에 mutable 객체가 있는 경우 문제발생

```python
a = [1, 2, ['a', 'b']]
b = a[:]
print(a,b)
b[2][0] = 0
print(a,b)

[1, 2, ['a', 'b']] [1, 2, ['a', 'b']]
[1, 2, [0, 'b']] [1, 2, [0, 'b']]
```



### Deep copy

만일 중첩된 상황에서 복사를 하고 싶다면, `깊은 복사(deep copy)` 필요

깊은 복사는 새로운 객체를 만들고 원본 객체 내에 있는 객체에 대한 복사를 재귀적으로 삽입

즉, 내부에 있는 모든 객체까지 새롭게 값이 변경

```python
import copy
a = [1, 2, ['a', 'b']]
b = copy.deepcopy(a)
print(a,b)
b[2][0] = 0
print(a,b)

[1, 2, ['a', 'b']] [1, 2, ['a', 'b']]
[1, 2, ['a', 'b']] [1, 2, [0, 'b']]
```



#### Grid

```python
from pprint import pprint
a= [[0]*10 for _ in range(10)]
pprint(a)

[[0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]]

a[0][0] = 10
pprint(a)

[[10, 0, 0, 0, 0, 0, 0, 0, 0, 0],
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]]
```

