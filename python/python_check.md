Psotional Arguments **Packing/Unpacking**

연산자(*) 

: 여러 개의 Positional Argument를 하나의 필수 parameter로 받아서 사용

연산자(**)

: 함수가 임의의 개수 Argument를 Keyword Argument로 호출될 수 있도록 지정

Argument들은 딕셔너리로 묶여 처리되며, parameter에 **를 붙여 표현

```python
def amy(a, b=1, c=2, *args, **kwags):
    print(a,b,c)
    print(args)
    print(kwags)
    
amy(1,2,3,3,6,9,x = 10, y=11)
```

[출력 결과]

```python
1 2 3
(3, 6, 9)
{'x': 10, 'y': 11}
```



**Scope**

```python
a=1
def func_1():
    a=2
    func_2()
    
def func_2():
    print(a,end='')
    
func_1()
print(a)
```

```python
11
```



**String index**

```python
string = 'i am happy person'
result = ''
for idx, value in enumerate(string):
    if idx%2:
        result += value
    else:
        result += value.upper()

print(result)
```

```python
I Am hApPy pErSoN
```



**List.extend()**

```python
name = ['ace','bell','carin']
name.extend('david')
print(name)
print(len(name))
```

```python
['ace', 'bell', 'carin', 'd', 'a', 'v', 'i', 'd']
8
```



**dictionary enumerate()**

```python
s_dict={}
for i in enumerate(range(3)):
    s_dict[i[0]]=i[1]
    
print(sum(s_dict.values()))
```

```python
3
```

