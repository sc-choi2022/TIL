### 구간 합(Prefix Sum)

수열에서 특정 구간의 합

연속적으로 나열된 N개의 수가 있을 경우, 나열된 수의 특정 구간에 속한 모든 수의 합



가장 간단한 방법으로는 for문을 사용해서도 충분히 구할 수 있지만 시간 복잡도를 생각했을 때 적절하지 않을 수 있다.

구간 합 알고리즘은 **O(1)**의 성능을 갖는다.



```
A(i) + A(i+1) + ... + A(j-1) + A(j) = S(j) - S(i-1)
= (A(i) + A(i+1) + ... + A(j-1) + A(j)) % m = S(j) - S(i-1) % m

(S(j) - S(i-1)) % m = 0
S(j) % m = S(i-1) % m
```



#### 사용

모든 구간합을 구한다.

구간 합들의 나머지를 나머지 배열에 넣는다. (배열의 인덱스가 나머지를 의미한다)

조합론으로 mC2를 해준다. (나머지 배열의 크기 m에서 나머지가 같은 2개를 뽑아서 조합하는 의미)



#### 예시 문제

BOJ_10986

```python
import sys

# 주어지는 수의 개수 N, 나누어 떨어지는 기준 수 M
N, M = map(int, sys.stdin.readline().split())

# N개의 숫자를 담은 리스트 lst
lst = list(map(int, sys.stdin.readline().split()))

# 구간의 개수 ans
ans = 0

# M으로 나누었을 떄 나머지를 담을 리스트 remainder
remainder = [0 for i in range(M)]
# 누적합을 담을 변수 presum
presum = 0

remainder[0] = 1

for i in range(N):
    # 누적합을 생성하고
    presum += lst[i]
    # 그 누적합의 나머지를 remainder리스트에 나머지값을 인덱스로 추가해준다.
    remainder[presum % M] += 1

# 나머지를 담은 리스트 remainder에서 조합으로 2개를 뽑는 방법으로 값을 ans에 누적해준다.
for i in remainder:
    ans += i*(i-1)//2

# ans 출력
print(ans)
```

