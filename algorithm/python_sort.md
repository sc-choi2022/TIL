# Sort

### Merge Sort

```python
def merge_sort(lst):
    if len(lst) == 1:
        return lst

    middle = len(lst)//2

    left = lst[:middle]
    right = lst[middle:]

    left = merge_sort(left)
    right = merge_sort(right)

    return merge(left, right)


def merge(left, right):

    result = []

    while left or right:

        if left and right:
            if left[0] <= right[0]:
                result.append(left.pop(0))
            else:
                result.append(right.pop(0))
        elif left:
            result.extend(left)
            break
        elif right:
            result.extend(right)
            break

    return result
```



cf) slicing

```python
a = [1,2,3,4,5]
b = [8,9,0]

a[2:2] = b
# [1,2,8,9,0,3,4,5]
a[2:4] = b
# [1,2,8,9,0,5]
```



### Quick Sort

**Youtube**

```python
def hoare(A, l, r):
    p = A[l]
    i, j = l, r
    while i <= j:
        while i<= j and A[i] <= p:
            i += 1
        while i<= j and A[j] >= p:
            j -= 1
        if i < j:
            A[i], A[j] = A[j], A[i]
    A[l], A[j] = A[j], A[l]
    return j

def qsort(A, l, r):
    if l < r:
        s = hoare(A, l, r)
        qsort(A, l, s-1)
        qsort(A, s+1, r)

A = [7, 1, 1, 1, 7]
N = len(A)
qsort(A, 0, N-1)
print(A)
```



**Webex**

```python
def quick_sort(lst, l, r):

    if l < r:
        pivot = partition(lst, l, r)
        quick_sort(lst, l, pivot-1)
        quick_sort(lst, pivot+1, r)
        
def hoare_partition(lst, l, r):
    pivot = lst[l]
    i = l
    j = r
    while i <= j:
        
        while i <= j and lst[i] <= pivot:
        # while not (lst[i] > pivot):
            i += 1
        while i <= j and lst[j] >= pivot:
            j -= 1
        if i < j:
            lst[i], lst[j] = lst[j], lst[i]
	lst[l], lst[j] = lst[j], lst[l]
    return j

def lomuto_partition(lst, l, r):
    pivot = lst[r]
    i = l-1
    for j in range(l,r):
        if lst[j] <= pivot:
            i += 1
            lst[j], lst[i] = lst[i], lst[j]

    lst[r], lst[i+1] = lst[i+1], lst[r]
    return i+1
```

**Pythonic method**

```python
lst = [1,2,3,4,5,6,7,8,9,0]
pivot = 6
left = [x for x in lst if x < pivot]
right = [x for x in lst if x > pivot]

left + [pivot] + right
```



**이진 탐색 트리**

탐색작업을 효율적으로 하기 위한 자료구조

모든 원소는 서로 다른 유일한 키를 갖느다.

key(왼쪽 서브트리) < key(루트 노드) < key(오른쪽 서브트리)

왼쪽 서브트리와 오른쪽 서브트리도 이진 탐색 트리다.

중위 순회하면 오름차순으로 정렬된 값을 얻을 수 있다.



삭제 : 

리프노드이면 지운다.

삭제할 노드가 리프 노드가 아닌 경우 차수가 1인 경우: 삭제, 서브 트리 이동

삭제할 노드가 리프 노드가 아닌 경우 차수가 2인 경우: 삭제, 후보 찾아 이동



**힙**

**완전 이진 트리**에 있는 노드 중에서 키 값이 가장 큰 노드나 키 값이 가장 작은 노드를 찾기 위해서 만든 자료구조

최대 힙

키 값이 가장 큰 노드를 찾기 위한 완전 이진 트리

부모 노드의 키 값> 자식 노드의 키 값

루트 노드: 키 값이 가장 큰 노드



최소 힙

키 값이 가장 작은 노드를 찾기 위한 완전 이진 트리

부모 노드의 키 값< 자식 노드의 키 값

루트 노드: 키 값이 작은 큰 노드



삭제 : 힙에서는 루트 노드의 원소만을 삭제할 수 있다.

```python
def del():
    t = tree[1] # 최상위 정보
    # 트리의 상위의 값과 마지막 값의 교환
    swap(tree[1], tree[lastP])
    lastP -= 1
    p = 1
    c = 더 큰 값을 갖는 자식 노드
    while 자식노드가 존재하고 tree[p] < tree[c]: # 부모노드의 값 < c의 값
        swap(tree[p], tree[c])	# swap(부모노드의 값, c의 값)
        p = c
        c = p의 큰 값을 갖는 자식 노드
        return
    return

def ins(value):
    lastP += 1
    tree[lastP] = value
    c = lastP
    p = lastP//2
    while tree[p] < tree[c]: #부모노드의 값 < 자식노드(c)의 값
        swap(tree[p], tree[c])
        c = p
        p = c//2
```



**최대힙의 삽입연산**

마지막 노드 추가

마지막 노드에 저장

부모 >  자식 또는 부모가 없을 때까지

부모와 자식의 자리를 바꾼다.

last는 몇개의 정점을 가지고 있는지 알기 위함



시험대비

테트로미노

어떤 그리드 안에서 모양으로 숫자를 더해서 가장 큰 숫자를 찾는것

모양을 한 묶음, 파리퇴치와 같이, index를 어떻게 다루면 좋을까

DFS 길찾아가는 방법으로 나올 것 + 알파의 제약조건 있음

서술형

heap에 대해서 나온다.

최대와 최소를 찾기 위해 쓰는 것

**heap은 완전이진트리**

완전이진트리
포화이진 트리의 노드 번호 1번부터 n번까지 빈자리가 없는 이진 트리
배열로 사용을 한다.(표현할 수 있다)

특징 : 나의 부모는 나의 절반이라는 과정이 있었다.

최대 힙, 최소 힙이 존재한다.

부모 자식간의 대소관계

(나의 왼쪽, 오른쪽 자식과의 관계는 이진탐색트리)

삽입을 어떻게 하는 건지

1. 빈자리에 넣는다. (완전이진트리이기 때문에 빈자리가 한개)
2. 넣고 부모와 비교를 한다. c = n, p=n//2
3. 최대힙이면 c, p 중 큰 것을 p에 저장
4. 안 바뀌거나 부모가 없을 때까지(index가 1이 될 때 까지)

삭제

삭제는 루트 노드에서만 가능하다.

(최대 힙이라면 최대값, 최소값이라면 최소값)

1. 루트 노드 값 삭제
2. 완전이진트리의 특징을 유지하기 위해서 가장 뒤에 있는 노드의 값을 올린다.
3. p와 c를 비교하여 가장 큰애를 올린다.
4. 더 이상 자식 노드가 없고 자신이 가장 클 때까지

pseudo코드를 쓰는 문제가 있는데 코드로 작성하지 않아도 된다.



```python
case = [
    # case 1
    [[0, 0], [0, 1], [0, 2], [0, 3]],
    [[0, 0], [1, 0], [2, 0], [3, 0]],

    # case 2
    [[0, 0], [0, 1], [1, 0], [1, 1]],

    # case 3
    [[0, 0], [1, 0], [2, 0], [2, 1]],
    [[0, 0], [1, 0], [0, 1], [0, 2]],
    [[0, 0], [0, 1], [1, 1], [2, 1]],
    [[0, 0], [0, 1], [0, 2], [-1, 2]],
    [[0, 0], [0, 1], [-1, 1], [-2, 1]],
    [[0, 0], [1, 0], [1, 1], [1, 2]],
    [[0, 0], [0, 1], [1, 0], [2, 0]],
    [[0, 0], [0, 1], [0, 2], [1, 2]],

    # case 4
    [[0, 0], [1, 0], [1, 1], [2, 1]],
    [[0, 0], [0, 1], [-1, 1], [-1, 2]],
    [[0, 0], [0, 1], [-1, 1], [1, 0]],
    [[0, 0], [0, 1], [1, 1], [1, 2]],

    # case 5
    [[0, 0], [0, 1], [-1, 1], [1, 1]],
    [[0, 0], [0, 1], [-1, 1], [0, 2]],
    [[0, 0], [1, 0], [1, 1], [2, 0]],
    [[0, 0], [0, 1], [0, 2], [1, 1]]
]

def tetro(i, j):
    global ans
    for x in range(19):
        Sum = 0
        for y in range(4):
            temp = case[x][y]
            ni = i + temp[0]
            nj = j + temp[1]
            if 0<= ni < N and 0<= nj < M:
                Sum += arr[ni][nj]
            else:
                break
        ans = max(ans, Sum)
    return

N, M = map(int, input().split())
arr = [list(map(int, input().split())) for _ in range(N)]

ans = 0
for i in range(N):
    for j in range(M):
        tetro(i, j)

print(ans)
```

----------------------------

힙, 완전 이진트리
부모자식간의 대소, 특징, 최대힙, 최소힙, 삽입의 차이

완전이진트리
포화이진 트리의 노드 번호 1번부터 n번까지 빈자리가 없는 이진 트리
배열로 사용을 한다.

이진 탐색 트리 vs 힙
이진 탐색 트리: 나를 기준으로 왼쪽, 오른쪽 대소관계
힙 : 부모 자식간에 대소관계가 존재 -> 가지고 탐색하기 어렵다.
	완전이진트리로 많이 사용한다.
힙 삽입, 삭제 연산

트리와 그래프
부모가 하나 싸이클이 없다. 부모가 자식에게만 연결관계가 존재한다.  -> 트리

연결리스트를 사용하는 장점
연결리스트는 나의 데이터와 왼쪽, 오른쪽 정보만 가지고 있다.
연결관계가 변경될 때 수정이 용이하다

----

3번

Heap
완전이진트리에 있는 노드 중에서 키 값이 가장 크거나 가장 작은 노드를 찾기 위해 만들어진 자료구조
부모 자식간의 대소관계가 존재한다.

최대힙
키값이 가장 큰 노드를 찾기 위한 완전이진트리
부모노드의 키값이 자식노드의 키값보다 큰 것
루트 노드는 키값이 가장 큰 노드이다.

최소힙
키 값이 가장 작은 노드를 찾기 위한 완전이진트리
부모노드의 키값이 자식노드의 키값보다 작다.

완전이진트리는 포화 이진트리의 1~n까지의 노드에서 빈자리가 없는 이진트리
특징: 부모노드는 자식노드//2 이다.

삽입
(최대힙)
1. 가장 마지막 노드에 값을 넣는다.
2. 부모노드와 키값을 비교한다. 자식 c, 부모 p = c//2
3. c, p중 큰 값을 p에 저장한다.
4. 부모노드가 없거나 부모노드의 키값이 커질때 까지 2,3번을 반복한다.

(최소힙)
1. 가장 마지막 노드에 키값을 넣는다.
2. 부모노드와 값을 비교한다. 부모노드 p = c//2, 자식 노드 c
3. p와 c 중 작은 값을 p에 저장한다.
4. 부모노드가 없거나 부모노드의 키값이 자식노드의 키값과 교환하지 않아도 될때까지 2-3번을 반복한다.

삭제
힙에서의 삭제는 루트노드에서만 일어난다.

1. 루트노드의 키값을 삭제한다.
2. 완전이진트리를 유지하기 위해 가장 뒤에 있는 키값을 루트노드의 키값으로 넣는다.
3. 부모노드 p와 자식 노드c를 비교하여 자식노드 중 키값이 가장 크고 p보다 큰 키값을 p노드의 키값과 바꾼다.
4. 자식 노드가 없고 키값을 바꿀 수 없을 때까지 2, 3번을 계속한다.

```python
def del():
    t = tree[1] # 최상위 정보
    # 트리의 상위의 값과 마지막 값의 교환
    swap(tree[1], tree[lastP])
    lastP -= 1
    p = 1
    c = 더 큰 값을 갖는 자식 노드
    while 자식노드가 존재하고 tree[p] < tree[c]: # 부모노드의 값 < c의 값
        swap(tree[p], tree[c])	# swap(부모노드의 값, c의 값)
        p = c
        c = p의 큰 값을 갖는 자식 노드
        return
    return

def ins(value):
    lastP += 1
    tree[lastP] = value
    c = lastP
    p = lastP//2
    while tree[p] < tree[c]: #부모노드의 값 < 자식노드(c)의 값
        swap(tree[p], tree[c])
        c = p
        p = c//2
```

