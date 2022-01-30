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





**OOP practice**

```python
# kim, kwon, lee # istance
# name, major # instance 변수
# class 3, 2 eyes, 2 legs # class 변수
# eat, walk # method

class Daejeon3:
    # class 바로 아래에서 정의해주는 class 변수
    ban = '대전 3반'
    eyes = '2개'
    
    def __init__(self, name, major):
        self.name = name	#self라는 instance의 name이라는 속성에 name이라는 값을 넣는다.
        self.major = major
```

```python
       
# instance 변수의 두가지 사용방법
# instance 변수는 공통적으로 가지고 있지만 값(value)이 다름
# instance에 접근해서 할당해줘야한다.
jun = Daejeon3('jun', 'math')
print(jun.name)
jun.gender = 'male'
print(jun.gender)

kwon = Daejeon3('kwon','eco')
print(kwon.name)
```

```python
# class 변수 : class내에서 공통적으로 가지고 있고 값(value)이 같음
print(jun.ban)

# namespace를 생각할 때, instance변수 ban에 값을 추가
# classmethod등을 사용해서 class 변수에 접근할 수 있다.
jun.ban = '대전3'
print(jun.ban)
print(Daejeon3.ban)

대전 3반
대전3
대전 3반
```

```python
# 메소드는 변수와 다르게 어떠한 기능을 담당
# 메소드도 함수의 일종이나 class안에 종속되는 함수

def eat(self): # instance가 동작하는 것이기 때문에 self가 필요
    print('냠냠')
    
jun.eat() # 변수와 다르게 불러온다.
```

```python
	def __str__(self):
        return f'내이름은 {self.name}이다'
    
print(jun)

내이름은 jun이다
```

```python 
class Daejeon3:
    # class 바로 아래에서 정의해주는 class 변수
    ban = '대전 3반'
    eyes = '2개'
    
    def __init__(self, name, major):
        self.name = name
        self.major = major
        
    def eat(self):
        print('냠냠')
        
    def get_direct(self):
        return Daejeon3.ban
    
    @classmethod
    def get_cls(cls):
        return cls.ban
 
jun = Daejeon3('jun','math')
jun.ban = '대전3'
print(jun.ban)
print(jun.get_direct())
print(jun.get_cls())

대전3
대전 3반
대전 3반
```



**get_ins 와 get_cls의 차이는 상속을 했을 때 발생**

```python
class Daejeon3:
    # class 바로 아래에서 정의해주는 class 변수
    ban = '대전 3반'
    eyes = '2개'
    
    def __init__(self, name, major):
        self.name = name
        self.major = major
        
    def eat(self):
        print('냠냠')
        
    def get_direct(self):
        return Daejeon3.ban
    
    @classmethod			# Daejeon3의 subclass D3Ace
    def get_cls(cls):
        return cls.ban
 
class D3Ace(Daejeon3):
    ban = '에이스반!'
    pass

choi = D3Ace('choi','mech')
choi.ban = '보충'
print(choi.ban)				# instance choi의 변수
print(choi.get_cls())		# D3Ace class의 변수
print(choi.get_direct())	# Daejeon class의 변수

보충
에이스반!
대전 3반
```

생략을 위해 

데코레이터를 안쓰면 instance method

@classmethod로 쓰면 class method

@staticmethod로 쓰고 정보가 필요없이 어떤 동작이면 static method

```python
@classmethod # 데코레이터로 감싸주게 되면
def ban_cls(cls):
    return cls.ban	

ban.cls()	# 바로 써주면 된다.

def ban_cls(cls):
    return cls.ban

# 데코레이터가 없는 경우
classmethod(ban_cls()) # 이런 것처럼 동작한다.

# 데코레이터가 함수를 인자로 받아서 추가적인 기능을 도와준다.
```



**Private Member를 사용하는 방법**

```python
class Person:
    def __init__(self, namem age = 19):
        self.__name = name
        self.age = age
        
jun = Person('jun')
# print(jun.__name)
print(jun._Person__name)
```



**getter 메소드와 setter 메소드**

```python
class Person:
    def __init__(self, name):
        self._name = name # 캡슐화. 직접적으로 변수이름을 가져오지 않음
        
    def name(self):
        return f'이 아이의 성은 {self._name}'
    
jun = Person('jun')
print(jun.name()) # 메소드

이 아이의 성은 jun
```

``` python
class Person:
    def __init__(self, name):
        self._name = name # 캡슐화. 직접적으로 변수이름을 가져오지 않음
    @property	# @property를 붙여주어 변수로서 활동
    def name(self):
        return f'이 아이의 성은 {self._name}'
    
jun = Person('jun')
print(jun.name)

이 아이의 성은 jun
```

```python
class Person:
    def __init__(self, age):
        self._age = age
    @property	# getter: 저장된 값을 꺼낼때 하는 작업
    def age(self):
        return self._age + 10
    
    @age.setter	# age라는 property의 setter, 넣을 때 하는 작업
    def age(self, new_age):
        self._age = new_age * 10
        
jun = Person(18)
print(jun.age)
jun.age = 100	# setter 작동
print(jun.age)

28
1010	# getter 작동
```

변수명을 사용하면 이러한 추가적인 작업을 할 수 없다.

**_(언더바)**가 없다면 오류발생



**다형성**

```python
class Enter:

    def hello(self):
        print('안녕하세요')
        
class Daejeon(Enter):
    def hello(self):	# 오버라이딩
        super().hello()	# 상속
        print('대전입니다.')
        
kim = Daejeon()
kim.hello()

안녕하세요
대전입니다.
```



**instance간의 상호작용**

```python
class Person:
    def __init__(self, name):
        self.name = name
    
    def hello(self):
        print(f'{self.name} : hello!')
        
    def hello_to(self, other):
        print(f'{self.name} : {other.name} 안녕!')
        
kim = Person('jun')
choi = Person('choi')
kim.hello()
kim.hello_to(choi)

jun : hello!
jun : choi 안녕!
```

