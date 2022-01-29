```python
class Person:
    pass

a = Person()						# Person() : class
a = list(map(int,input().split())	# list() : class
a = 'hello'							# 'hello' : str class의 instance
a.capitalize()						# str class의 method capitalize()
a = 123							
b = str(a)							# b는 str class의 instance
[1, 2, 3].append(4)					# list의 instance [1, 2, 3]
         							# list의 method append()
         
(1+2j).real							# complex의 instance 1+2j
         							# complex의 attribute real
```



```python
class Daejeon3:
    ban = '3반'				   # class 변수
    
	def __init__(self,name):
		self.nickname = name	# self.name = name이 같을 필요없다
        						# self.nickname attribute에 name을 넣어주겠다.
	def hi(self):
		print(f'hi, 나는 {self.nickname}이야')	# {name}은 되지 않는다.

        
jun = Daejeon3('jun')
print(jun.nickname)
jun.age = 20					# Daejeon3 class 안 instance jun안에 attribute
jun.ban = '3'
print(jun.age)

kang = Daejeon3('kang')
print(jun.ban)
print(kang.ban)

jun
20
3
3반
```

```python
class Daejeon3:
    ban = '3반'
       
    def __init__(self,name, age, ban):
        self.name = name
        self.age = age
        self.ban = ban
    
    def __del__(self):
        print('죽음')
    
    @classmethod
    def class_method(cls):
        print(cls.ban)
        
    def instance_method(self):
        print(self.ban)
        pass
        
jun = Daejeon3('jun', 20, '아직 몰라')
jun.class_method()
jun.instance_method()

3반
아직 몰라
```



**classmethod를 왜 쓰는가?**

```python
class Daejeon3:
    cnt = 0
    
    def __init__(self):
        Daejeon3.cnt +=1
        
    def func(self):
        print(self.cnt)

jun = Daejeon3()
kang = Daejeon3()
jun.func()
kang.func()

jun.cnt = 10
jun.func()				# instance jun의 cnt을 사용
kang.func()				# class의 cnt 사용

2
2
10
2
```



**정리**

```python
class Person:
    
    pass
    # 여기에는 클래스 변수가 온다
    
    def __init__(self, *arg): # 셀프는 instance 그 자제이다.
        # 여기에는 instatnce 변수가 온다.
        # args가 instance 변수로 사용 가능하다.
        
    def func(self): # 자동적으로 instance가 input으로 주어지는 함수
        pass
    
    @staticmethod
    def func1():	# input이 없는 함수, 호출시 self나 cls가 자동적으로 붙는 것과 다름
        pass		# 우리가 아는 함수도 동일하나 class에 묶여 있다.
    
    @classmethod
    def func2():	# staticmethod와 동일하나 첫번째 인자로 class가 들어온다.
        pass
    
    # 첫번째 인자로 self가 들어온다면 instance method
```



**classmethod & staticmethod**

```python
class Person:
    population = 0
    
    @staticmethod
    def add_population():
        Person.population += 1
```

```python
Person.add_population()
print(Person.population)

# 실행할수록 증가
```

```python
class Student(Person):
    population = 0
```

```python
Student.add_population()
print(Student.add_population)

# 실행해도 계속 0으로 변하지 않는다.
```

만약 classmethod일 경우

```python
class Person:
    population = 0
    
    @classmethod
    def add_population(cls):
        cls.population += 1
        
class Student(Person):
    population = 0

Person.add_population()
print(Person.population)

Student.add_population()
print(Student.add_population)

# 실행할수록 증가
```

