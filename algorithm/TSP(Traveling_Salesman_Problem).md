### Traveling Salesman Problem

TSP(Traveling Salesman Problem) 외판원 문제

조합 최적화 문제의 일종

**정의**

여러 도시들이 있고 한 도시에서 다른 도시로 이동하는 비용이 모두 주어진다.

모든 도시들을 단 한 번만 방문하고 원래 시작점으로 돌아오는 최소 비용의 이동 순서를 구한다.



#### Solution

##### 완전탐색, **동적 계획법**...



**BOJ_2098**

**시간 초과 코드**

```python
import sys

def dfs(now, cost, visited):
    global ans
    if len(visited) == N:
        if road[now][visited[0]] != 0:
            cost += road[now][visited[0]]
            ans = min(ans, cost)
            return
    for i in range(N):
        if i not in visited and road[now][i] and cost < ans:
            visited.append(i)
            dfs(i, cost + road[now][i], visited)
            visited.pop()

# 도시의 수 N
N = int(sys.stdin.readline())

road = [list(map(int, sys.stdin.readline().split())) for _ in range(N)]

ans = 16000000
for i in range(N):
    dfs(i, 0, [i])
print(ans)
```



**Pass Code**

1. 방문여부 Bitmask

   visited 변수에 2진수로 도시를 표현

   0001(2) => 0번 도시를 방문했다는 의미

2. 현재도시에서의 최소비용 DP

   `dp[current][visit] = 미방문 도시를 거쳐 다시 돌아오는 최소 비용`

3. 도시 방문 DFS

```python
import sys

def dfs(x, visited):
    # 이미 확인한 경로
    if dp[x][visited] != 0:
        return dp[x][visited]
    # 모두 방문한 경우
    if visited == (1 << (N - 1)) - 1:
        # 원래 도시로 돌아 올 수 있다.
        if W[x][0]:
            return W[x][0]
        # 원래 도시로 돌아 올 수 없다.
        else:
            return float('inf')
    # 최소값을 float('inf')로 초기화
    min_cost = float('inf')
    # 시작 도시인 1을 제외하고 모든 도시를 방문
    for i in range(1, N):
        # 길이 없거나 이미 방문했다면
        if W[x][i] == 0 or visited & (1 << i-1):
            continue
        # 위 조건으로 경로를 확인하여 비용 계산
        D = W[x][i] + dfs(i, visited | (1 << (i -1)))
        # min_cost와 D 중 작은 값을 min_cost에 할당
        min_cost = min(min_cost, D)
    # dp[x][visited]에 min_cost 할당
    dp[x][visited] = min_cost
    # min_cost return
    return min_cost

# 도시의 수 N
N = int(sys.stdin.readline())

# 비용 행렬 W
W = [list(map(int, sys.stdin.readline().split())) for _ in range(N)]
# 비용을 담아줄 리스트 dp
dp = [[0]*(1<<N) for _ in range(N)]
# 시작 도시 0과 방문정보 0을 매개변수로 dfs 실행 후 return 값 출력
print(dfs(0, 0))
```

