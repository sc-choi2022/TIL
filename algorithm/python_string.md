[toc]



# String

각 문자에 대해서 대응되는 숫자를 정해 놓고 이것을 메모리에 저장하는 방법 사용

영어

: 대소문자 합쳐 52개 6비트(64가지)면 모두 표현 가능 => 코드체계



### ASCII

문자 인코딩 표준: ASCII(American Standard Code for information Interchange)

7bit 인코딩으로 128문자를 표현하며 33개의 출력 불가능한 제어 문자들과 공백을 비롯한 95개의 출력 가능한 문자들로 이루어져 있다.

* 출력 가능 아스키 문자(32 ~ 126)

확장 아스키는 표준 문자 이외의 악센트 문자, 도형 문자, 특수 문자, 특수 기호 등 부가적인 문자를 128개 추가할 수 있게 하는 부호이다.

* 표준 아스키: 7bit 사용
* 확장 아스키: 1B의 8bit 모두 사용
* 확장 부호는 표준 아스키와 같이 서로 다른 프로그램이나 컴퓨터 사이의 교환 불가
* 확장 아스키는 프로그램이나 컴퓨터 또는 프린터가 해독할 수 있도록 설계되어야한다.



### 유니코드

다국어 처리를 위해 만든 표준

유니코드도 다시 Character Set으로 분류

* UCS-2(Universal Character Set 2)
* UCS-4(Universal Character Set 4)
* 유니코드를 저장하는 변수의 크기를 정의
* 바이트 순서를 표준화하지 못해 각 경우를 구분해서 구현하는 문제 발생
* 유니 코드의 적당한 외부 인코딩이 필요



**endian**

big-endian:

큰 단위가 앞에 나오는 것

**12, 34, 56**			(직관적으로 보기 좋음)

(낮은 주소)12, 34, 56(높은 주소)

little-endian:

작은 단위가 앞에 나오는 것

**12, 34, 56**			(계산에 용이)

(낮은 주소)56, 34, 12(높은 주소)

두개를 한쌍인 경우가 많다.

무엇을 저장할 때: 앞 :arrow_right: 뒤 또는 뒤 :arrow_right: 앞 방향으로 쌓을 수 있을 것



#### 유니코드 인코딩 (UTF: Unicode Transformation Format)

* UTF-8 (in web) **가변적**
  * MIN: 8bit, MAX: 32bit( 1 Byte*4)
* UTF-16 (in windows, java)
  * MIN: 16bit, MAX: 32bit( 2 Byte*2)
* UTF-8 (in unix)
  * MIN: 32bit, MAX: 32bit( 4 Byte*1)



**Python 인코딩**

* 2.x 버전 - ASCII -> #-\*-coding:utf-8 -\*- (첫 줄에 명시)
* 3.x 버전 - 유니코드 UTF-8 생략가능
* 다른 인코딩 방식으로 처릿 첫 줄에 작성하는 위 항목에  원하는 인코딩 방식을 지정해주면 된다.



## 문자열

### 문자열의 분류

문자열(String)

* fixed length
* variable length
  * length controlled (java 언어에서의 문자열)
  * delimited (c 언어에서의 문자열)



**참고**

java에서 String 클래스에 대한 메모리 배치 예

* String에는 데이터 type 특징도 포함된다. 예) size

C언어에서 문자열 처리

* 문자열은 문자들의 배열 형태로 구현된 응용 자료형
* 문자배열에 문자열을 저장할 때는 항상 마지막에 끝을 표시하는 널 문자('\\0')을 넣어줘야 한다.
* 문자열 처리에 필요한 연산을 함수 형태로 제공한다.



```python
s1 = list(input())
s2 = input()
print(s1)
print(s2)
print(s1[0])
print(s2[0])
s2[0] = 'd' # 불가능 String iterable, immutable

# 출력 결과
['s','t','r']
str
s
s
```



#### strlen() 함수 만들어 보기

def strlen(a): # '\\0'을 만나면 '\\0'을 제외한 글자수를 리턴

while을 써서 함수 완성

```python
def mystrlen(s):
    i = 0
    while s[!] !='\0':
        i += 1
    return i

a = ['a', 'b', 'c', '\0']
print(mystrlen(a))
```

cf)

```python
print('a', end='')
print('\n', end='')
print('b')

# 출력결과
a
b
```



#### Java(객체지향 언어)에서의 문자열 처리

* 문자열 데이터를 저장, 처리해주는 클래스를 제공한다.

* String클래스를 사용한다.

  `String str="abc";` 또는 `String str = new String("abc")`

* 문자열 처리에 필요한 연산을 연산자, 메소드 형태로 제공한다.

  -+, length(), replace(), split(), substring()

  * 보다 풍부한 연산을 제공한다.



#### Python에서의 문자열 처리

* char 타입 없다.
* 텍스트 데이터의 취급방법이 통일되어 있다.



* 문자열 기호
* '(홑따옴표), "(쌍따옴표), '''(홑따옴표 3개), ""''(쌍따옴표 3개)
* \+ 연결(Concatenation)
  * 문자열 + 문자열: 이어 붙여주는 역할
* \* 반복
  * 문자열 * 수: 수만큼 문자열이 반복

* 문자열은 시퀀스 자료형으로 분류되고, 시퀀스 자료형에서 사용할 수 있는 인덱싱, 슬라이싱 연산들을 사용할 수 있음
* 문자열 클래스에서 제공되는 메소드
  * replace(), split(), isalpha(), find()
* 문자열은 튜플과 같이 요소값을 변경 할 수 없음(immutable)



#### C와 Java의 String 처리의 기본적인 차이점

* c는 아스키 코드로 저장한다.
* java는 유니코드(UTF16, 2byte)로 저장한다.
* Python은 유니코드(UTF8)로 저장한다.

**C**

```c
char * name = "홍길동"
int count = strlen(name);
printf("%d", count);
```

6이 출력된다.



**Java**

```python
String name = "홍길동";
System.outprintln(name.length());
```

3이 출력된다.



**Python**

```python
name = "홍길동"
print(len(name))
```

3이 출력된다.



### 문자열 뒤집기

자기 문자열에서 뒤집는 방법

* swap을 위한 임시 변수가 필요하며 반복 수행을 **문자열 길이의 반만** 수행

새로운 빈 문자열을 만들어 소스의 뒤에서부터 읽어서 타켓에 쓰는 방법



**Python은 reverse 함수 혹은 slice notation을 이용하여 구현**

```python
s = 'Reverse this strings'
s = s[::-1]
s.reverse()	# string에서는 동작안함
```



### 문자열 비교

c strcmp()함수를 제공한다.

Java에서는 equals() 메소드를 제공한다.

* 문자열 비교에서 == 연산은 메모리 참조가 같은지를 묻는 것

Python에서는 ==연산자와 is연산자를 제공한다.

* == 연산자는 내부적으로 특수 메서드 \_\_eq\_\_()를 호출

```python
s1 = 'abc'
s2 = 'abc'
s3 = 'def'
s4 = s1
s5 = s1[:2] + 'c'	# slicing을 하면 새로 만들어진다.

print(s2 == s1)
print(s2 is s1)
print(s3 == s1)
print(s4 == s1)
print(s5)
print(s5 == s1)	# 내용 동일하다면 True
print(s5 is s1) # 참조하는 것이 동일하다면 True

# 출력결과
True
True
False
True
abc
True
False
```



다음 C코드를 참고해 문자열 비교함수를 만들어보자

* 문자열이 같으면 0 리턴
* str1이 str2보다 사전 순서상 앞서면 음수 혹은 -1 리턴
* str1이 str2보다 사전 순서상 나중이면 양수 혹은 1 리턴

```c
int my_strcmp(const char *str1, const char *str2)
{
    int i = 0;
    while(str1[i] != '\0')
    {
        if(str1[i] != str2[i]) break;
        i++;
    }
    return (str1[i] - str2[i])
}
```

```python
a = 'ab'
b = 'abc'
c = 'de'
d = 'Abc'

print(a<b)
print(a>b)
print(a<c)
print(a>c)
print(a<d)
print(a==d)

# 출력 결과
True
False
True
False
False
False
```

```python
def my_strcmp(s1, s2):
    if s1<s2:
        return -1
    elif s1>s2:
        return 1
    else: return 0
```



### 문자열 숫자를 정수로 변환하기

C언어에서는 atoi()함수를 제공한다. 역함수로는 itoa()가 있다.

java에서는 숫자 클래스의 parse메소드를 제공한다.

* 예: Integer.parseInt(String)
* 역함수로는 toString() 메소드를 제공한다.

파이썬에서는 숫자와 문자변환 함수를 제공한다.

* 예) int("123"), float("3.14"), str(123), repr(123)

```python
def atoi(s):
    i = 0
    for x in s:
        i = i*10 + ord(x)-ord('0')
	return i        
```

**cf) itao() 구현**



## 패턴 매칭

고지식한 패턴 검색 알고리즘(index 연산의 연습으로 반드시 할 수 있어야한다.)

카프-라비 알고리즘

KMP 알고리즘

보이어-무어 알고리즘



### 고지식한 알고리즘(Brute Force)

본문 문자열을 청므부터 끝까지 차례대로 순회하면서 패턴 내의 문자들을 일일이 비교하는 방식으로 동작

<u>**현재 단계에서 반드시 할 줄 알아야 하는 것**</u>

* index에 대해 생각해야 한다.

```python
p = 'is'
t = 'This is a book!'
M = len(p)
N = len(t)

def BruteForce(p,t):
    i = 0	# t의 index
    j = 0	# p의 index
    while j<M and i<N:
        if t[i] != p[j]:
            i = i - j
            j = -1
		i = i + 1
        j = j + 1
	if j == M:
        return i-M	# 검색 성공
    else:
        return -1	# 검색 실패
```

```python
def BruteForce(p,t):
    n = len(t)
	m = len(p)

    i = j = 0
    for i in range(n-m+1):
        for j in range(m):
            if t[i+j] != p[j]:
                break
		else:
            return 1
```



**시간 복잡도**

최악의 경우 시간 복잡도는 텍스트이 모든 위치에서 패턴을 비교 필요

<u>O(MN)</u>



비교횟수를 줄이는 방법?

### KMP 알고리즘

불일치가 발생한 텍스트 스트링의 앞 부분에 어떤 문자가 있는지를 미리 알고 있으므로, 불일치가 발생한 앞 부분에 대하여 다시 비교하지 않고 매칭을 수행

패턴을 전처리하여 배열 next[M]을 구해서 잘못된 시작을 최소화함

* next[M]: 불일치가 발생했을 경우 이동할 다음 위치



**시간 복잡도**

<u>O(M+N)</u>



**매칭이 실패했을 때 돌아갈 곳을 계산한다.**

패턴의 각 위치에 대해 매칭에 실패했을 때 돌아갈 곳을 준비해 둔다.

이전 자리까지의 일치하는 개수를 count = 비교할 패턴 위치

짧은 쪽인 패턴을 찾는 것이 필요, 패턴을 찾은 개수를 넣을 리스트를 M+1개로 준비

```python
def kmp(t, p):
    N = len(t)
    M = len(p)
    lps = [0] * (M+1)
    # preprocessing
    j = 0 # 일치한 개수 == 비교할 패턴 위치
    lps[0] = -1
    for i in range(1, M):
        lps[i] = j
        if p[i] == p[j]:
            j += 1
		else:
            j = 0
	lps[M] = j
    print(lps)
    i = 0
    j = 0
    while i<N and j<= M:
        if j==-1 or t[i] == p[j]:	# 첫글자가 불일치했거나, 일치하면
            i += 1
            j += 1
		else:
            j = lps[j]
		if j==M:
            print(i-M, end=' ')
            j = lps[j]
print()
return

t = 'zzzabcdabcdabcefabcd'
p = 'abcdabcef'
kmp(t,p)

# 출력 결과
[-1, 0, 0, 0, 0, 1, 2, 3, 0, 0]
7
```



### 보이어-무어 알고리즘

**교수님 예시 코드 있음**

오른쪽에서 왼쪽으로 비교

대부분의 상용 소프트웨어에서 채택하고 있는 알고리즘

보이어-무어 알고리즘은 패턴에 오른쪽 끝에 있는 문자가 불일치하고 이 문자가 패턴내에 존재하지 않는 경우, 이동 거리는 무려 패턴의 길이 만큼이 된다.

* 패턴 내에 일치하는 문자가 두개 있는 경우 기본적으로 뒤에 나오는 것



#### 문자열 매칭 알고리즘 비교

찾고자 하는 문자열 패턴의 길이 m, 총 문자열 길이 n

고지식한 패턴 검색 알고리즘: 수행시간 O(mn) **최악의 경우**

카프-라빈 알고리즘: 수행시간 Θ(n) **평균적으로**

KMP 알고리즘: 수행시간 Θ(n)



**보이어-무어 알고리즘**

앞에 두 매칭 알고리즘의 공통점: 텍스트 문자열을 적어도 한번씩은 훑는다는 것이다. 따라서 최선의 경우에도 Ω(n)

보이어-무어 알고리즘은 텍스트 문자를 다 보지 않아도 된다.

발상의 전환: 패턴의 오른쪽부터 비교

최악의 경우 수행시간: O(mn)

입력에 따라 다르지만 일반적으로 Θ(n)보다 시간이 덜 든다.



## 참고

### 문자열 암호화

#### 시저 암호(Caesar cipher)

줄리어스 시저가 사용했다고 하는 암호

시저 암호에서는 평문에서 사용되고 있는 알파벳을 일정한 문자 수만큼 [평행이동] 시킴으로써 암호화를 행한다.



#### 문자 변환표를 이용한 암호화(단일 치환 암호)

단순한 카이사르 암호화보다 훨씬 강력한 암호화 기법



#### 단일 치환 암호의 복호화

복호화 하기 위해서는 모든 키의 조합(key space)가 필요하다.



#### bit열의 암호화

배타 논리합(exclusive-or) 연산 사용



### 문자열 압축

#### BMP 파일포맷 압축 방법

#### 허프만 코딩 알고리즘