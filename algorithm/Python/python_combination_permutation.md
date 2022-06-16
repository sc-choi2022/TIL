## combination

조합(*n*C*r*): 

n개의 원소를 갖는 집합에서 r개의 원소를 선택하는 것, 순서 관계 없다.

```python
def func(idx, n, r, res):
    if idx == r:
        print(res)
        return

    start = 0
    if len(res):
        start = max(res) + 1
        # start = max(res)  # +1이 없다면 중복 허용

    for i in range(start, n):

        res.append(i)
        func(idx+1, n, r, res)
        res.pop()

        # func(idx+1, n, r , res + [i])
        

func(0, 7, 3, [])
```

 ```python
 lst = [1, 2, 3, 4, 5]
 
 def func(combi):
     if len(combi) == r:
         print(combi)
         return
     
     if combi:
     	tmp_max = max(combi)
         
     for i in lst:        
         if i not in combi:
             if combi and i <= tmp_max:
                 continue
 			combi.append(i)
             func(combi)
             combi.pop()
             
 func([])            
 ```

```python
lst = [1, 2, 3, 4, 5]

def combi2(combi, idx):
    if len(combi) == r:
        print(combi, idx)
        return
    
    for i in range(idx + 1, len(lst)):
        combi.append(lst[i])
        combi2(combi, i)
        combi.pop()
            
combi2([], 0)
```



중복조합(*n*H*r*):

n개의 원소를 갖는 집합에서 r개의 원소를 중복을 허용하며 선택하는 것, 순서 관계 없다.

```python
def func(idx, n, r, res):
    if idx == r:
        print(res)
        return

    start = 0
    if len(res):
        start = max(res)	# +1이 없기 때문에 중복 허용
        # start = max(res)  

    for i in range(start, n):

        res.append(i)
        func(idx+1, n, r, res)
        res.pop()

        # func(idx+1, n, r , res + [i])
        

func(0, 7, 3, [])
```

```python
lst = [1, 2, 3, 4, 5]

def func(combi):
    if len(combi) == r:
        print(combi)
        return
    
    if combi:
    	tmp_max = max(combi)
        
    for i in lst:        
        if i not in combi:
            if combi and i < tmp_max:	# 조합의 코드에서 =가 없다면 중복조합
                continue
			combi.append(i)
            func(combi)
            combi.pop()
            
func([])            
```

```python
lst = [1, 2, 3, 4, 5]

def combi2(combi, idx):
    if len(combi) == r:
        print(combi, idx)
        return
    
    for i in range(idx, len(lst)):
        combi.append(lst[i])
        combi2(combi, i)
        combi.pop()
            
combi2([], 0)
```



## permutation

순열(*n*P*r*)

서로 다른 n개의 원소에서 r개를 **중복없이 순서에 상관있게** 선택하는 혹은 나열

```python
def f(i, r):
    if i==r: 
        print(bit[:r])
        return
    for n in range(4):
        if n not in bit[0:i]:
            bit[i] = n
            f(i+1,r)

N = 4
bit = [0]*N
f(0, N-1)
```

```python
def f(i, N): # 중복있음 i 부분집합에 포함될지 결정할 원소의 인덱스, N 전체 원소개수
    if i==N:
        print(bit)
    else:
        bit[i] = 0
        f(i+1, N)
        bit[i] = 1
        f(i+1, N)
        bit[i] = 2
        f(i+1, N)
        bit[i] = 3
        f(i+1, N)
    return

N = 4
a = [x for x in range(1, N+1)]
bit = [0]*N
cnt = 0
f(0, N)
print('cnt =', cnt)
```

```python
def real(i, N): # 중복없음 i 부분집합에 포함될지 결정할 원소의 인덱스, N 전체 원소개수
    if i==N:
        print(bit)
        return
    else:

        for n in range(4):
            if n not in bit[0:i]:
                bit[i] = n
                bit[i] = n
                real(i + 1, N)
    return

def ncr(i,N):
    if i==N:
        print(bit[:N])
        return
    else:
        for n in range(4):
            if n not in bit[0:i]:
                bit[i] = n
                ncr(i+1, N)


N = 4
a = [x for x in range(1, N+1)]
bit = [0]*N
cnt = 0
real(0, N)
print('cnt =', cnt)
```

```python
def ncr(i,N):
    if i==N:
        print(bit[:N])
        return
    else:
        for n in range(4):
            if n not in bit[0:i]:
                bit[i] = n
                ncr(i+1, N)


N = 4
a = [x for x in range(1, N+1)]
bit = [0]*N
cnt = 0
ncr(0, N-1)
print('cnt =', cnt)
```

```python
lst = [1, 2, 3, 4, 5]

r = 3

def func(perm):
    if len(perm) == r:
        print(perm)
        return
    
    for i in lst:
        if i not in perm:
            perm.append(i)
            func(perm)
            perm.pop()
```



중복 순열

n개의 원소에서 r개를 순서에 상관 있게 뽑는데, **중복을 허락하여** 뽑는 것

```python
def f(i, N): # 중복있음 i 부분집합에 포함될지 결정할 원소의 인덱스, N 전체 원소개수
    if i==N:
        print(bit)
    else:
        bit[i] = 0
        f(i+1, N)
        bit[i] = 1
        f(i+1, N)
        bit[i] = 2
        f(i+1, N)
        bit[i] = 3
        f(i+1, N)
    return
```

```python
lst = [1, 2, 3, 4, 5]

r = 3

def func(perm):
    if len(perm) == r:
        print(perm)
        return
    
    for i in lst:
        perm.append(i)
        func(perm)
        perm.pop()
```



## Itertools

```python
from itertools import combinations, permutations

print(list(permutations(range(5),3)))
print(list(combinations(range(5),3)))
```