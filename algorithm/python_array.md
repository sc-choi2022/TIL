[toc]

## Algorithm

알고리즘: 유한한 단계를 통해 문제를 해결하기 위한 절차나 방법

#### 알고리즘을 표현하는 방법

의사코드(슈도코드, Pseudocode)와 순서도



#### 무엇이 좋은 알고리즘인가?

정확성: 얼마나 정확하게 동작하는가

작업량: 얼마나 적은 연산으로 원하는 결과를 얻어내는가

메모리 사용량: 얼마나 적은 메모리를 사용하는가

단순성: 얼마나 단순한가

최적성: 더 이상 개선할 여지없이 최적화되었는가



#### 시간 복잡도(Time Complexity) 

알고리즘의 작업량을 표현할 때 시간복잡도로 표현한다

* 실제 걸리는 시간을 측정
* 실행되는 명령문의 개수를 계산



#### 빅-오(O) 표기법(Big-Oh Notation)

시간 복잡도 함수 중에서 가장 큰 영향력을 주는 n에 대한 항만을 표시

계수(Coefficient)는 생략하여 표시

예) n개의 데이터를 입력 받아 저장한 후 각 데이터에 1씩 증가시킨 후 각 데이터를 화면에 출력하는 알고리즘의 시간복잡도는 어떻게 되나? **O(n)**



## Array 

배열: 일정한 자료형의 변수들을 하나의 이름으로 열거하여 사용하는 자료구조



### 필요성

프로그램 내에서 여러 개의 변수가 필요할 때 효율적으로 자료에 접근 가능

하나의 선언을 통해 둘 이상의 변수를 선언 가능

단순히 다수의 변수 선언을 의미하는 것이 아닌 다수의 변수로는 하기 힘든 작업을 배열을 활용해 쉽게 가능



### 1차원 배열의 선언

별도의 선언 방법이 없으면 변수에 처음 값을 할당할 때 생성



**1차원 배열 선언의 예**

```python
Arr = list()
Arr = []
Arr = [1, 2, 3]
Arr = [0]*10
```



**1차원 배열의 접근**

Arr[0] = 10; //'배열 Arr의 0번 원소에 10을 저장'

Arr[index] = 20; // '배열 Arr의 index번 원소에 20을 저장'



**배열 활용 예제: Gravity**



## Sort

2개 이상의 자료를 특정 기준에 의해 작은 값부터 큰 값(오름차순: ascending), 혹은 그 반대의 순서대로(내림차순: descending) 재배열하는 것

키

* 자료를 정렬하는 기준이 되는 특정 값



**대표적인 정렬 방식의 종류**

* 버블 정렬 (Bubble Sort)
* 카운팅 정렬 (Counting Sort)
* 선택 정렬 (Selection Sort)
* 퀵 정렬 (Quick Sort)
* 삽입 정렬 (Insertion Sort)
* 병합 정렬 (Merge Sort)



### 버블 정렬 (Bubble Sort)

인접한 두 개의 원소를 비교하며 자리를 계속 교환하는 방식

**정렬과정**

1. 첫 번째 원소부터 인접한 원소끼리 계속 자리를 교환하면서 맨 마지막자리까지 이동한다.
2. 한 단계가 끝나면 **가장 큰 원소가 마지막 자리**로 정렬된다.

교환하며 자리를 이동하는 모습이 물 위에 올라오는 거품 모양과 같다고 하여 버블 정렬이라고 한다.



**시간 복잡도**

<u>O(n**2)</u>

```python
def BubbleSort(a, N): # a: 정렬할 List, N: 원소 수
    for i in range(N-1, 0, -1): # 범위의 끝까지
        for j in range(0,i):
            if a[j] > a[j+1]:
                a[j], a[j+1] = a[j+1], a[j]
```



### 카운팅 정렬(Counting Sort)

항목들의 순서를 결정하기 위해 집합에 각 항목이 몇 개씩 있는지 세는 작업을 하여 선형 시간에 정렬하는 효율적인 알고리즘

2022.02.09



**제한 사항**

* 정수나 정수로 표현할 수 있는 자료에 대해서만 적용가능
  * 각 항목의 발생 회수를 기록하기 위해, 정수 항목으로 인덱스 되는 카운트들의 배열을 사용하기 때문
* 카운트들을 위한 충분한 공간을 할당하려면 집합 내의 가장 큰 정수를 아는 것 필요



**시간 복잡도**

<u>O(n+k)</u>

```python
def countingSort(arr): # 기준에 따라 index가 달라진다 확인 필요!
    size = len(arr)
    output = [0] * size

    # count 리스트 준비 
    count = [0] * 10 # 0~9인 경우 예시

    # 각 원소의 숫자를 count 리스트에 저장 
    for m in range(0, size):
        count[arr[m]] += 1

    # 항목의 앞에 위치할 항목의 개수를 반영하기 위한 for문
    for m in range(1, 10):
        count[m] += count[m - 1]
        
	# 원소의 index를 확인하고 output 리스트에 index위치에 할당하고 count리스트 값 1 감소
    # while문을 활용하여 size만큼만 진행
    m = size - 1
    while m >= 0:
        output[count[arr[m]] - 1] = arr[m]
        count[arr[m]] -= 1
        m -= 1

    for m in range(0, size):
        arr[m] = output[m]
        
	# for문 활용시
    for i in range(len(output)-1, -1, -1):
        count[arr[i]] -= 1
        output[count[arr[i]]] = A[i]
```



### Baby-gin Game

* 완전 검색(Exaustice Search)
  * Brute-force 혹은 generate-and-test 기법이라고도 불림
  * 모든 경우의 수를 테스트한 후 최종 해법을 도출
  * 일반적으로 경우의 수가 상대적으로 작을 때 유용
* 순열(Permutation)
  * 서로 다른 것들 중 몇 개를 뽑아서 한 줄로 나열하는 것
  * 서로 다른 n개 중 r개를 택하는 순열: nPr
  * nPr = n * (n-1) * ... * (n -4 + 1)
  * nPn = n! = Factorial



### 탐욕(Greedy) 알고리즘

최적해를 구하는데 사용되는 근시안적인 방법

일반적으로 머릿속에 떠오르는 생각을 검증 없이 바로 구현하면 Greedy 접근



동작 과정

1. 해 선택: 현재 상태에서 부분 문제의 최적 해를 구한 뒤, 이를 부분해 집합(Solution Set)에 추가
2. 실행 가능성 검사: 새로운 부분해 집합이 실행 가능한지를 확인. 문제의 제약 조건을 위반하는 지 검사
3. 해 검사: 새로운 부분해 집합이 문제의 해가 되는지 확인. 
4. 아직 전체 문제의 해가 완성되지 않았다면 해 선택부터 다시 시작



활용 1

```python
num = 456789
c = [0] * 12

for i in range(6):
    c[num%10] += 1
    num //= 10	# 정수형으로 나누는 것
    
while num>0:
    c[num%10]
    num //= 10
```



활용2

```python
# 6개 숫자로 이루어져있지만 12개를 만드는 이유
# index error를 만들지 않기 위해
i = 0
tri = run = 0
while i < 10:
    if c[i] >= 3: # triplete 조사 후 데이터 삭제
        c[i] -= 3
        tri += 1
        continue;
	if c[i] >= 1 and c[i + 1] >= 1 and c[i + 2] >= 1: # run 조사 후 데이터 삭제
        c[i] -= 1
        c[i+1] -= 1
        run += 1
        continue;
	i += 1
if run + tri == 2 :
    print('Baby Gin')
else:
    print('Lose')
```



**자주 실수하는 오답**

* 입력받은 숫자를 정렬하고 앞뒤 3자리씩 끊어서 run 및 triplet을 확인하는 방법
* 탐욕 알고리즘적인 접근은 해답을 찾아내지 못하는 경우가 있으므로 유의 필요



## Array 2

### 2차원 배열의 선언

* 1차원 List를 묶어놓은 List
* 2차원 이상의 다차원 List는 차원에 따라 Index를 선언
* 2차원 List의 선언: 행의 개수, 열의 개수를 필요로 함
* Python 에서는 데이터 초기화를 통해 변수선언과 초기화가 가능

```python
arr = [[0,1,2,3],[4,5,6,7]]
```



참고

```python
N = int(input())
arr = [list(map(int,input().split())) for _ in range(N)]

N = int(input())
arr = [list(map(int,input())) for _ in range(N)]

arr1 = [0]*N + [list(map(int, input().split())) for _ range(N)] + [0]*N
```



### 배열 순회

n * m 배열의 n*m개의 모든 원소를 빠짐없이 조사하는 방법



#### 행 우선 순회

```python
# i: 행의 좌표, j: 열의 좌표
for i in range(n):
    for j in range(m):
        Array[i][j]
```



#### 열 우선 순회

```python
# i: 행의 좌표, j: 열의 좌표
for j in range(n):
    for i in range(m):
        Array[i][j]
```



#### 지그재그 순회

```python
# i: 행의 좌표, j: 열의 좌표
for i in range(n):
    for j in range(m):
        Array[i][j + (m-1-2*j) * (i%2)]
```



#### 델타를 이용한 2차 배열 탐색

2차 배열의 한 좌표에서 4방향의 인접 배열 요소를 탐색하는 방법

```python
# NxM 배열
di = [0, 1, 0, -1]
dj = [1, 0, -1, 0]
for k in range(4):
    ni = i + di[k]
    nj = j + dj[k]
    if 0<=ni<=N and 0<=nj<M: #유효 인덱스
        arr[ni][nj]
```

```python
# python only
for di, dj in [(0,1),(1,0),(0,-1),(-1,0)]:
    ni = i + di
    nj = j + dj
    if 0<=ni<N and 0<=nj<M: #유효 인덱스
        arr[ni][nj]
        
# 바로 움직이는 것이 아니라 ni, nj를 이용하여 움직인다.   
```

복잡한 방향의 델타도 생각해보자

**8방향**

```python
di = [1, 1, 1, 0, 0, -1, -1, -1]
dj = [0, -1, 1, 1, -1, 0, 1, -1]
```



#### 전치 행렬

```python
# i : 행의 좌표, len(arr)
# j : 열의 좌표, len(arr[0])
arr = [[1,2,3],[4,5,6],[7,8,9]]	# 3*3 행렬

for i in range(3):
    for j in range(3):
        if i < j:	# 제약 사항 필요
            arr[i][j], arr[j][i] = arr[j][i], arr[i][j]
```

```python
# zip과 map을 활용하여 전치행렬
lst = [[1,2,3],[4,5,6],[7,8,9]]
lst1 = list(map(list,zip(*lst)))
# zip만 있어도 전치행렬 만들 수 있다.
# zip object로 나오게 된다.
lst2 = zip(*lst)
```



#### 추가

```python
lst = [[1,2,3],[4,5,6],[7,8,9]]
lst1 = list(map(list,zip(*lst[::-1])))	# 오른쪽으로 뒤집음
lst1 = list(map(list,zip(*lst)))[::-1]	# 왼쪽으로 뒤집음
lst1 = list(map(list,zip(*lst[::-1])))[::-1]	# 점대칭
```



### 부분집합 생성

#### 부분집합(Subset Sum)의 수

집합의 원소가 n개일 때, 공집합을 포함한 부분집합의 수는 2**n개 이다.



#### 비트 연산자

비트연산자

| 연산자 | 의미                                 |
| ------ | ------------------------------------ |
| &      | 비트 단위로 AND 연산                 |
| \|     | 비트 단위로 OR 연산                  |
| <<     | 피연산자의 비트 열을 왼쪽으로 이동   |
| >>     | 피연산자의 비트 열을 오른쪽으로 이동 |

**<< 연산자**

1 << n :2**n 즉, 원소가 n개일 경우의 모든 부분집합의 수를 의미한다.

**& 연산자**

i & (1<<j): i의 j번째 비트가 1인지 아닌지를 검사한다.



cf)

```python
# 10(2) = 1010
print(bin(10))
print(bin(10<<1))	# *2 한 것과 동일
print(bin(10<<2))
print(bin(10>>2))

# 출력 값
0b1010
0b10100
0b101000
0b10
```





**부분집합 코드**

```python
A = [1, 2, 3]
bit = [0]*3
for i in range(2):
    bit[0] = i
    for j in range(2):
        bit[1] = j
        for k in range(2):
            bit[2] = k
            print(bit)	# 여기까지 bit 채워짐
            for p in range(3):
                if bit[p]:	# [0]: 공집합이 아니라면
                    print(A[p], end = ' ')
                    print()
```

```python
arr = [3, 6, 7, 1, 5, 4]
n = len(arr)	# 원소의 개수

for i in range(1<<n):		# 1<<n: 부분 집합의 개수
    for j in range(n):		# 원소의 수만큼 비트를 비교
        if i&(1<<j):		# i의 j번 비트가 1인 경우
            print(arr[j], end= '')	# j번 원소 출력
	print()            
print()            
```

```python
arr = [1, 2, 3]
subsets = [[]]

for num in arr:
    size = len(subsets)
    for y in range(size):
        subsets.append(subsets[y]+[num])
print(Subsets)        
```



### 검색(Search)

저장되어 있는 자료 중에서 원하는 항목을 찾는 작업

목적하는 탐색 키를 가진 항목을 찾는 것

* 탐색 키(search key): 자료를 구별하여 인식할 수 있는 키

검색의 종류

* 순차 검색(sequential search)
* 이진 검색(binary search)
* 해쉬(hash)



#### 순차 검색(sequential search)

일렬로 되어 있는 자료를 순서대로 검색하는 방법

* 가장 간단하고 직관적인 검색 방법
* 배열이나 연결 리스트 등 순차구조로 구현된 자료 구조에서 원하는 항목을 찾을 때 유용
* 알고리즘이 단순하여 구현 쉽지만 **검색 대상의 수가 많은 경우**에는 **수행시간이 급격히 증가하여 비효율적**



두 가지 경우

* 정렬되어 있지 않은 경우
* 정렬되어 있는 경우



##### 정렬되어 있지 않은 경우

첫 번째 원소부터 순서대로 검색 대상과 키 값이 같은 원소가 있는지 비교

키 값이 동일한 원소를 찾으면 그 원소의 인덱스 반환

자료구조의 마지막에 이를 때까지 검색 대상을 찾지 못하면 검색 실패



**찾고자 하는 원소의 순서에 따라 비교회수가 결정됨**

* 정렬되지 않은 자료에서의 순차 검색의 평규 비교 회수
* = (1/n)*(1+2+3+...+n) = (n+1)/2
* 시간 복잡도: O(n)

```python
def sequentialSearch(a, n, key):
    i = 0
    while i<n and a[i] !=key:	#인덱스 범위(반드시 먼저), key 유무
        i = i + 1
	if i<n:
        return i
    else:
        return -1
```



##### 정렬되어 있는 경우

검색과정

자료가 오름차순으로 정렬된 상태에서 검색을 실시한다고 가정

자료를 순차적으로 검색하면서 키 값을 비교하여, 원소의 키 값이 검색 대상의 키 값보다 크면 찾는 원소가 없다는 것이므로 더 이상 검색하지 않고 검색 종료



**찾고자 하는 원소의 순서에 따라 비교회수가 결정됨**

* 정렬이 되어있으므로, 검색 실패를 반환하는 경우 평균 비교회수가 반으로 준다.
* 시간 복잡도: O(n)

```python
def sequentialSearch2(a, n, key):
    i = 0
    while i<n and a[i]<key:
        i = i+1
	if i<n and a[i] == key:
        return i
    else:
        return -1
```



#### 이진 검색(Binary Search)

자료의 가운데에 있는 항목의 키 값과 비교하여 다음 검색의 위치를 결정하고 검색을 계속 진행하는 방법

* 목적 키를 찾을 때까지 이진 검색을 순환적으로 반복 수행함으로써 검색 범위를 반으로 줄여 보다 빠르게 검색을 수행

**이진 검색을 하기 위해서는 자료가 정렬된 상태여야 한다.**



**검색 과정**

1. 자료의 중앙에 있는 원소를 고른다.

2. 중앙 원소의 값과 찾고자 하는 목표 값을 비교한다.

3. 목표 값이 중앙 원소의 값보다 작으면 자료의 왼쪽 반에 대해서 새로 검색을 수행하고, 크다면 자료의 오른쪽 반에 대해서 새로 검색을 수행한다.
4. 찾고자 하는 값을 찾을 때까지 1~3의 과정을 반복한다.



**시간 복잡도**

O(logN)

**구현**

검색범위의 시작점과 종료점을 이용하여 검색을 반복 수행한다.

이진 검색의 경우, 자료에 삽입이나 삭제가 발생했을 때 배열의 상태를 항상 정렬 상태로 유지하는 추가 작업이 필요하다.

```python
def binarySearch(a, N, key):
    start = 0
    end = N-1
    while start <= end:
        middle = (start + end)//2
        if a[middle] == key:	# 검색 성공
            return True
        elif a[middle] > key:
            start = middle - 1
        else:
            start = middle + 1
	return False            	# 검색 실패
```

cf) 재귀 함수 이용

```python
def binarySearch2(a, start, end, key):
    if start > end:
        return False
    else:
        middle = (start + end)//2
        if key == a[middle]:
            return True
        elif key < a[middle]:
            return binarySearch2(a, start, middle-1, key)
        elif key a[middle] > key:
            return binarySearch2(a, middle+1, end, key)
```



#### 인덱스

Database에서 유래

테이블에 대한 동작 속도를 높여주는 자료 구조

인덱스를 저장하는데 필요한 디스크 공간은 보통 테이블을 저장하는데 필요한 디스크 공간보다 작다. 보통 인덱스는 키-필드만 가지고 있고, 테이블의 다른 세부 항목들을 가지고 있지 않기 때문이다.



#### 선택 정렬(Selection Sort)

Bubble sort와 비교할 수 있어야한다.

|                  | Bubble sort                                         | Selection Sort                                      |
| ---------------- | --------------------------------------------------- | --------------------------------------------------- |
| 시간 복잡도      | O(n**2)                                             | O(n**2)                                             |
| 한 단계가 끝나면 | **가장 큰 원소가 마지막 자리**로 정렬               | **가장 작은 원소가 맨 앞 자리**로 정렬              |
| 반복 구간        | 처음 위치를 제외한 나머지 리스트 대상               | 마지막 위치를 제외한 나머지 리스트 대상             |
| 구간             | 구간의 시작: 항상 i <br/>구간의 끝: 반복마다 앞으로 | 구간의 시작: 반복마다 뒤로<br/>구간의 끝은 항상 N-1 |
| 교환의 횟수      | 선택 정렬보다 많다.                                 | 버블(, 삽입) 정렬보다 작다.                         |



**정렬 과정**

1. 주어진 리스트 중에서 최소값을 찾는다.
2. 그 값을 리스트의 맨 앞에 위치한 값과 교환한다.
3. 맨 처음 위치를 제외한 나머지 리스트를 대상으로 위 과정을 반복한다.



**시간 복잡도**

<u>O(n**2)</u> (이중 for문)



**구현**

```python
def selectionSort(a, N):
    for i in range(N-1):
        minIdx = i
        for j in range(i+1, N):
            if a[minIdx] > a[j]:
                minIdx = j
		a[i], a[minIdx] = a[minIdx], a[i]                
```



#### 셀렉션 알고리즘(Selection Algorithm)

저장되어 있는 자료로부터 k번째로 큰 혹은 작은 원소를 찾는 방법

* 최소값, 최대값 혹은 중간값을 찾는 알고리즘을 의미하기도 한다.



**선택 과정**

셀렉션은 아래와 같은 과정을 통해 이루어진다.

1. 정렬 알고리즘을 이용하여 자료 정렬
2. 원하는 순서에 있는 원소 가져옴



**k번째로 작은 원소를 찾는 알고리즘**

1번부터 k번째까지 작은 원소들을 찾아 배열의 앞쪽으로 이동시키고, 배열의 k번째를 반환한다.

k가 비교적 작을 때 유용하며 O(kn)의 수행시간을 필요로 한다.

```python
def select(arr, k):
    for i range(0, k):
        minIdx = 0
        for j in range(i+1, len(arr)):
            if arr[minIdx] > arr[j]:
                minIdx = j
		arr[i], arr[minIdx] = arr[minIdx], arr[i]
	return arr[k-1]        
```

