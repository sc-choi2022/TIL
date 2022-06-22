### Euclidean Algorithm

유클리드 호제법

Algorithm for the greatest common divisor. 

최대 공약수와 관계된 알고리즘

2개의 자연수의 최대 공약수를 구하는 알고리즘

호제법은 두 수가 상대방의 수를 나누어 결국 원하는 수를 얻는 알고리즘을 말한다.

자연수 a, b(a>b)에 대해 a를 b로 나눈 나머지를 r이라고 하면 a와 b의 최대공약수는 b와 r의 최대공약수와 같다.

이 성질을 반복하여 나머지가 0이 되었을 때 나누는 수가 a와 b의 최대공약수이다.



**Wikipedia의 예시**

a = 1071, b = 462

1071 = 2 * 462 + 147

462 = 3 * 147 + 21

147 = 7 * 21 + 0

나머지가 0이 되는 21이 1071와 462의 최대 공약수가 된다.



**BOJ_1934**

```python
import math
import sys
# 테스트 케이스 수
T = int(sys.stdin.readline())

for _ in range(T):
    # 최소공배수를 구해야하는 수 A, B
    A, B = map(int, sys.stdin.readline().split())

    # 유클리드 호제법을 활용하기 위해
    # 첫 나눗셈을 진행한다.
    # 나머지는 remainder, 나눠지는 수는 number
    remainder = max(A,B) % min(A,B)
    number = min(A, B)
    while True:
        # 나머지가 0이되면 최대 공약수인 number를 활용하여 최대공약수 출력 
        # while문을 break
        if remainder == 0:
            print(number * A//number * B//number)
            break
        # number, remainder를 재 정의한다.
        number, remainder = remainder, number % remainder
```

