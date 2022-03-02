# Stack

## Stack1

물건을 쌓아 올리듯 자료를 쌍아 올린 형태의 자료구조이다.

스택에 저장된 자료는 선형 구조를 갖는다.

cf)

* 선형구조: 자료 간의 관계가 1대1의 관계를 갖는다.
  * 예: list, stack, queue, linked list

* 비선형구조: 자료 간의 관계가 1대N의 관계를 갖는다.
  * 예: graph, tree


스택에 자료를 삽입하거나 스택에서 자료를 꺼낼 수 있다.

**마지막에 삽입한 자료를 가장 먼저 꺼낸다. 후입선출**

<u>**LIFO, Last-In-First-Out**</u>

예) 스택에 1,2,3 순으로 자료를 삽입한 후 꺼내면 역순 3,2,1순으로 꺼낼 수 있다.



### Stack의 구현

스택을 프로그램에서 구현하기 위해서 필요한 자료구조와 연산

* 자료구조: 자료를 선형으로 저장할 저장소
  * 배열을 사용할 수 있다.
  * 저장소 자체를 스택이라고 부르기도 한다.
  * 스택에서 마지막 삽입된 원소의 위치를 **top**이라 부른다. (stack pointer)
* 연산
  * 삽입: 저장소에 자료를 저장한다. 보통 **push**라고 부른다.
  * 삭제: 저장소에서 자료를 꺼낸다. 꺼낸 자료는 삽인한 자료의 역순으로 꺼낸다. 보통 **pop**이라고 부른다.
  * 스택이 공백인지 아닌지를 확인하는 연산 **.isEmpty**
  * 스택의 top에 있는 item(원소)을 반환하는 연산 **.peek**



#### Stack의 push algorithm

appen 메소드를 통해 리스트이 마지막에 데이터를 삽입

```python
def push(item):
    s.append(item)
```

[참고]

```python
def push(item, size):
    global top
    top += 1
    if top==size:
        print('overflow!')
	else:
        stack[top] = item
        
size = 10
stack = [0]*size
top = -1

push(10)
top += 1		# push(20)
stack[top] = 20
```

cf) 

append, pop은 리스트에서 시간이 올래걸리는 방법

크기를 정해놓고 하는 것이 더 빠르다.



#### Stack의 pop algorithm

```python
def pop():
    if len(s) == 0:
        # underflow
        return
    else:
        return s.pop(-1)
```

[참고]

```python
def pop():
    global top
    if top == -1:
        print('underflow') # for debugging
        return 0
    else:
        top -= 1
        return stack[top+1]
    
print(pop())

if top > -1:	# pop()
    top -= 1
    print(stack[top+1])
```



#### Stack 구현 고려 사항

1차원 배열을 사용하여 구현할 경우 구현이 용이하다는 장점이 있지만 스택의 크기를 변경하기가 어렵다는 단점이 있다.



이를 해결하기 위한 방법으로 저장소를 동적으로 할당하여 스택을 구현하는 방법이 있다. **동적 연결리스트**를 이용하여 구현하는 방법을 의마한다. 구현이 복잡하다는 단점이 있지만 메모리를 효율적으로 사용한다는 장점을 가진다.



#### Stack의 응용1 : 괄호검사

괄호의 종류: 대괄호 ('[', ']'), 중괄호 ('{', '}'), 소괄호('(', ')')

**조건**

① 왼쪽 괄호의 개수와 오른쪽 괄호의 개수가 같아야 한다.

② 같은 괄호에서 왼쪽 괄호는 오른쪽 괄호보다 먼저 나와야한다.

③ 괄호 사이에는 포함 관계만 존재한다.



**Stack을 이용한 괄호 검사**

**괄호를 조사하는 알고리즘 개요**

문자열에 있는 괄호를 차례대로 조사하면서 왼쪽 괄호를 만나면 스택에 삽입하고, 오른쪽 괄호를 만나면 스택에서 top괄호를 삭제한 후 오른쪽 괄호와 짝이 맞는지 검사한다.

이 때, 스택이 비어 있으면 조건 1 또는 조건 2에 위배되고 괄호의 짝이 맞지 않으면 조건 3에 위배된다.

마지막 괄호까지를 조사한 후에도 스택에 괄호가 남아 있으면 조건 1에 위배된다.



#### Stack의 응용2 : function call

프로그램에서의 함수 호출과 복귀에 따른 수행 순서를 관리

* 가장 마지막에 호출된 함수가 가장 먼저 실행을 완료하고 복귀하는 후입선출 구조이므로, 후입선출 구조의 스택을 이용하여 수행순서 관리
* 함수 호출이 발생하면 호출한 함수 수행에 필요한 지역변수, 매개변수 및 수행 후 복귀할 주소등의 정보를 스택 프레임(stack frame)에 저장하여 시스템 스택에 삽입
* 함수의 실행이 끝나면 시스템 스택의 top 원소(stack frame)를 삭제(pop)하면서 프레임에 저장되어 있던 복귀주소를 확인하고 복귀
* 항수 호출과 복귀에 따라 이 과정을 반복하여 전체 프로그램 수행이 종료되면 시스템 스택은 공백 스택이 된다.
* 



### 재귀호출

자기 자신을 호출하여 순환 수행되는 것

함수에서 실행해야 하는 작업의 특성에 따라 일반적인 호출방식보다 재귀호출방식을 사용하여 함수를 만들면 프로그램의 크기를 줄이고 간단하게 작성



재귀호출의 예) factorial

* n에 대한 factorial: 1부터 n까지의 모든 자연수를 곱하여 구하는 연산

```python
n! = n *(n-1)!
(n-1)! = (n-1)*(n-2)!
...
1! = 1
```

* 마지막에 구한 하위 값을 이용하여 상위 값을 구하는 작업 반복



피보나치

재귀로 복사

### Memoization

: 컴퓨터 프로그램을 실행할 때 이전에 계산한 값을 메모리에 저장해서 매번 다시 계산하지 않도록 하여 전체적인 실행속도를 빠르게 하는 기술이다. 동적 계획법의 핵심이 되는 기술이다.



앞의 예에서 피보나치 수를 구하는 함수를 재귀함수로 구현한 알고리즘은 문제점이 있다.

<u>"엄청난 중복 호출이 존재한다는 것"이다.</u>

* 피보나치 수열의 Call Tree

피보나치 수를 구하는 알고리즘에서 fibo(n)의 값을 계산하자마자 저장하면(memoize), 실행시간을 Θ(n)으로 줄일 수 있다.

Memoization방법을 적용한 알고리즘

```python
# memo를 위한 배열을 할당하고, 모두 0으로 초기화 한다.
# memo[0]을 0으로 memo[1]는 1로 초기화 한다.

def fibo1(n):
    global memo
    if n>= 2 and len(memo) <=n:
        memo.append(fibo1(n-1) + fibo1(n-2))
	return memo[n]

memo = [0, 1]
```



### DP(Dynamic Programming)

동적 계획(Dynamic Programming) 알고리즘은 그리디 알고리즘과 같이 **최적화 문제**를 해결하는 알고리즘이다.

동적 계획 알고리즘은 먼저 입력 크기가 작은 부분 문제들을 모두 해결한 후에 그 해들을 이용하여 보다 큰 크기의 부분 문제들을 해결하여, 최종적으로 원래 주어진 입력의 문제를 해결하는 알고리즘이다.



#### 피보나치 수 DP 적용

피보나치 수는 부분 문제의 답으로부터 본 문제의 답을 얻을 수 있으므로 최적 부분 구조로 이루어져 있다.

**1. 문제를 부분 문제로 분할한다.**

* Fibonacci(n)함수는 Fibonacci(n-1)과 Fibonacci(n-2)의 합
* Fibonacci(n-1)은 Fibonacci(n-2)과 Fibonacci(n-3)의 합
* Fibonacci(2)은 Fibonacci(1)과 Fibonacci(0)의 합
* Fibonacci(n)은 Fibonacci(n-1), Fibonacci(n-2), ..., Fibonacci(1), Fibonacci(0)의 부분집합으로 나뉜다.

**2. 부분 문제로 나누는 일을 끝냈으면 가장 작은 부분 문제부터 해를 구한다.**

**3. 그 결과는 테이블에 저장하고, 테이블에 저장된 부분 문제의 해를 이용하여 상위 문제의 해를 구한다.**

| 테이블 인덱스 | 저장되어 있는 값 |
| :-----------: | ---------------- |
|      [0]      | 0                |
|      ...      | ...              |
|      [n]      | fibo[n]          |

**피보나치 수 DP 적용 알고리즘**

```python
def fibo2(n):
    f = [0, 1]
    
    for i in range(2, n+1):
        f.append(f[i-1] + f[i-2])
        
	return f[n]        
```



#### DP의 구현 방식

* recursive 방식: fib1()
* iterative 방식: fib2()



* memoization을 재귀적 구조에 사용하는 것보다 반복적 구조로 DP를 구현하는 것이 성능 면에서 보다 효율적이다.
* 재귀적 구조는 내부에 시스템 호출 스택을 사용하는 오버헤드가 발생하기 때문이다.



### DFS(깊이우선탐색)

비선형구조인 그래프 구조는 그래프로 표현된 모든 자료를 빠짐없이 검색하는 것이 중요함.

두가지 방법

* 깊이 우선 탐색(Depth First Search, DFS)
* 너비 우선 탐색(Breadth First Search, BFS)



시작 정점의 한 방향으로 갈 수 있는 경로가 있는 곳까지 깊이 탐색해 가다가 더이상 갈 곳이 없게 되면, 가장 마지막에 만났던 갈림기길 간선이 있는 정점으로 되돌아와서 다른 방향의 정점으로 탐색을 계속 반복하여 결국 모든 정점을 방문하는 순회방법

가장 마지막에 만났던 갈림길의 정점으로 되돌아가서 다시 깊이 우선 탐색을 반복해야 하므로 **후입선출 구조의 스택 사용**



#### DFS 알고리즘

**1** 시작 정점 v를 결정하여 방문한다.

**2** 정점 v에 인접한 정점 중에서

1. 방문하지 않은 정점 w가 있으면, 정점 v를 스택에 push하고 정점 w를 방문한다.
2. 방문하지 않은 정점이 없으면, 탐색의 방향을 바꾸기 위해서 스택을 pop하여 받은 가장 마지막 방문 정점을 v로 하여 다시 2.를 반복한다.

**3** 스택이 공백이 될때까지 **2**를 반복한다.



**길찾기 문제- DFS**

```python
# 10번의 테스트 케이스를 진행하기 위한 for문
for _ in range(10):
    # 테스크 케이스 번호와 길의 총 개수를 각각 case와 N에 할당
    case, N = map(int, input().split())
    # 순서쌍에 대한 정보를 arr에 모두 할당
    arr = list(map(int, input().split()))
    # 순서쌍의 정보를 확인하여 입력할 리스트 grid 생성
    grid = [[0]*100 for _ in range(100)]

    # arr에 담긴 값을 각 정점과 도착하는 정점의 번호로 구분하여 순서쌍 위치에 1을 할당
    for i in range(0, N*2, 2):
        grid[arr[i]][arr[i+1]] = 1

    # 스택을 담을 리스트 stack과 방문정보를 저장할 visted 리스트 초기화
    stack = []
    visited = []

    # 출발점이 0으로 지정되어 있기 때문에 stack과 visted에 0을 추가
    stack.append(0)
    visited.append(0)

    # 답으로 출력할 ans를 초기화
    ans = 0
    # stack이 empty가 될 때까지
    while stack:
        # stack에 top에 있는 값을 temp에 할당
        temp = stack[-1]

        # 0~99까지의 노드에서
        for node in range(100):
            # grid의 값이 1이며 방문정보가 없는 노드를 stack과 vistied에 추가
            if grid[temp][node] == 1 and node not in visited:
                stack.append(node)
                visited.append(node)
                break
        # for문의 반복이 끝날 때까지 break되지 않았다면 top 노드에서 갈수 있는 모든 node를 간 것이므로
        # stack의 top값을 pop
        else:
            stack.pop()

        # 도착 지점인 99에 방문한 기록이 있다면
        if 99 in visited:
            # ans에 1을 할당하고 while문을 탈출
            ans = 1
            break
    # 테스트 케이스 번호와 답을 출력
    print(f'#{case} {ans}')
```

