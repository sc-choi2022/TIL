[toc]



# OOP

객체지향 프로그래밍 



**파이썬은 모두 객체(object)로 이뤄져 있다.**

### 객체

객체(object)는 특정 타입의 인스턴스(instance)이다.



int의 instance : 120, 900, 5

string의 instance : 'hello', 'bye'

list의 instance : [232, 89, 1], []



객체(object)의 특징

* 타입(type) : 어떤 연산자(operator)와 조작(method)가 가능한가?
* **속성(attribute) : 어떤 상태(데이터)를 가지는가?**
* **조작법(method) : 어떤 행위(함수)를 할 수 있는가?**

객체(Object) = 속성(Attribute) + 기능(Method)



### 객체지향 프로그래밍

: 프로그램을 여러 개의 독립된 객체들과 그 객체들 간의 상호작용으로 파악하는 프로그래밍 방법



절차지향 프로그래밍

```python
a = [1, 2, 3]
a = sorted(a)
a = reversed(a)
```

```python
a = 10
b = 30
square1_area = a * b
square1_circumference = 2 * (a + b)

c = 300
d = 20
square2_area = c * d
square2_circumference = 2 * (c + d)
```



객체지향 프로그래밍

: 데이터와 기능(method) 분리, 추상화된 구조(interface)

```python
a = [1, 2, 3]
a.sort()
a.reverse()
```

```python
def area(x, y):
    return x * y

def circumference(x, y):
    return 2 * (x + y)

a = 10
b = 30
c = 300
d = 20

square1_area = area(a, b)
square1_circumference = circumference(a, b)
square2_area = area(c, d)
square2_circumference = circumference(c, d)
```



객체지향 프로그래밍 : 데이터와 기능(메소드) 분리, 추상화된 구조(인터페이스)

```python
class Rectangle:
    def __init__(self, x, y):	#self는 r1, r2같은 instance (실습)
        self.x = x
        self.y = y
    def area(self):
        return self.x * self.y
    def circumference(self):
        return 2 * (self.x + self.y)
    
r1 = Rectangle(10, 30)
r1.area()						# area는 r1에 종속되어 있다.
r1.circumference()

r2 = Rectangle(300, 20)
r2.area()
r2.circumference()
```



사각형 - **클래스(class)**

각 사각형 (R1, R2) - **인스턴스(instance)**

사각형의 정보 - **속성(attribute)**

* 가로 길이, 세로 길이

사각형의 행동 - **메소드(method)**

* 넓이를 구한다. 높이를 구한다.



### 객체지향의 장점

프로그램을 **유연하고 변경이 용이**하게 만들기 때문에 대규모 소프트웨어 개발에 많이 사용된다.

프로그래밍을 더 배우기 쉽게 하고 **소프트웨어 개발과 보수를 간편하게** 한다.

**직관적인 코드 분석**을 가능하게 한다.



## OOP 기초

### 기본 문법

클래스 정의

```python
class MyClass:
    pass
```



인스턴스 생성

```python
my_instance = MyClass()
```



메소드 호출

```python
my_instance.my_method()
```



속성

```python
my_instance.my_attribute
```



### 클래스와 인스턴스

클래스 : 객체들의 분류(class)

인스턴스 : 하나하나의 실체/예(instance)

```python
class Person:
    pass
type(Person)
person1 = Person()
isinstance(person1, Person)
type(person1)

type
True
__main__.Person
```

Python은 모든 것이 Object, 모든 Object는 특정 타입의 instance



속성

특정 데이터 타입/클래스의 객체들이 가지게 될 상태/데이터를 의미

```python
class Person:
    def __init__(self, name):
        self.name = name
        
person1 = Person('지민')
person1.name

'지민'
```



메소드

특정 데이터 타입/클래스의 객체에 공통적으로 적용 가능한 행위(함수)

```python
class Person:
    def talk(self):
        print('안녕')
        
    def eat(self, food):
        print(f'{food}를 냠냠')
        
person1 = Person()
person1.talk()
person1.eat('피자')
person1.eat('치킨')

'안녕'
'피자를 냠냠'
'치킨를 냠냠'
```



### 객체 비교하기

**==**

동등한(equal)

변수가 참조하는 객체가 <u>동등한(내용이 같은) 경우</u> True

두 객체가 같아 보이지만 실제로 동일한 대상을 가리키고 있다고 확인해 준 것은 아님



**is**

동일한(identical)

두 변수가 <u>동일한 객체를 가리키는 경우</u> True



```python
a = [1, 2, 3]
b = [1, 2, 3]
print(a == b, a is b)

b = a
print(a == b, a is b)

True False
True True

# cf) None의 비교 if a is None
```



## Instance

### 인스턴스 변수

<u>인스턴스가 개인적으로 가지고 있는 속성(attribute)</u>

각 인스턴스들의 <u>고유한 변수</u>



생성자 메소드(__init__에서 self.\<name>으로 정의

인스턴스가 생성된 이후 \<instance>.\<name>으로 접근 및 할당

```python
class Person:
    def __init__(self, name):
        self.name = name		# 인스턴스 변수 정의
        
john = Person('john')
print(john.name)
john.name = 'John Kim'
print(john.name)

'john'
'John Kim'
```



### 인스턴스 메소드

인스턴스 변수를 사용하거나, 인스턴스 변수에 값을 설정하는 메소드

클래스 내부에 정의되는 메소드의 기본

호출 시, 첫번째 인자로 <u>인스턴스 자기자신(self)이 전달됨</u>

\* Method는 class에 묶여있어 class만 사용할 수 있는 함수

```python
class MyClass:
    def instance_method(self, arg1, ...):
        my_instance = MyClass()
        my_instance.instance_method(...)
```



### self

<u>인스턴스 자기자신</u>

Python에서 인스턴스 메소드는 호출 시 첫번째 인자로 <u>인스턴스 자신이 전달</u>되게 설계

* 매개변수 이름으로 <u>self</u>를 첫번재 인자로 정의
* 다른 단어로 써도 작동하지만, <u>python의 암묵적인 규칙</u>

```python
class Person:
    def test(Self):
        return self

p1 = Person()
p1.test()
p1
Person.test(p1)

<__main__.Person at 0x1ecf08103a0>
<__main__.Person at 0x1ecf08103a0>
<__main__.Person at 0x1ecf08103a0>	# 내부적으로 이렇게 실행
```



### 생성자(constructor) 메소드

인스턴스 객체가 생성될 때 자동으로 호출되는 메소드

인스턴스 변수들의 초깃값을 설정

* 인스턴스 생성
* \__init__ 메소드 자동 호출



```python
class Person:
    def __init__(self):
        print('인스턴스가 생성되었습니다.')
        
person1 = Person()

인스턴스가 생성되었습니다.
```

```python
class Person:
    def __init__(self, name):
        print(f'인스턴스가 생성되었습니다.{name}')
        
person1 = Person('지민')

인스턴스가 생성되었습니다.지민
```



### 소멸자(destructor) 메소드

인스턴스 객체가 소멸(파괴)되기 직전에 호출되는 메소드

```python
class Person:
    def __init__(self):
        print('응애')
    def __del__(self):
        print('인스턴스가 사라졌습니다.')
        
person1 = Person()
del person1

응애
인스턴스가 사라졌습니다.
```



### 매직 메소드

Double underscore(__)가 있는 메소드는 특수한 동작을 위해 만들어진 메소드로, 스페셜 메소드 혹은 매직 메소드라고 불림

특정 상황에 자동으로 불리는 메소드

```python
__str__(self)	# print함수를 사용시 __str__의 방법이 호출(informal)
__len__(self)	
__repr__(self)	# formal, 정보를 주는 것(developer에게)
__lt__(self)	#<
__le__(self)	#<=
__eq__(self)	#==
__gt__(self)	#>
__ge__(self)	#>=
__ne__(self)	#!=
```



객체의 특수 조작 행위를 지정(함수, 연산자 등)

`__str__`

: 해당 객체의 출력 형태를 지정

* 프린트 함수를 호출할 대, 자동으로 호출
* 어떤 인스턴스를 출력하면 `__str__`의 return 값이 출력

`__gt__`

: 부등호 연산자(>, greater than)

```python
class Circle:
    def __init__(self, r):		#init은 예외적으로 return을 사용안함
        self.r = r
    def area(self):
        return 3.14* self.r * self.r
    def __str__(self):
        return f'[원] radius: {self.r}'
    def __gt__(self, other):
        print(f'{self.r}/{other.r}')
        return self.r > other.r
    
c1 = Circle(10)
c2 = Circle(1)
print(c1)
print(c2)
c1 > c2
c1 < c2

[원] radius: 10
[원] radius: 1
10/1
1/10
True
False
```



## 클래스

### 클래스 변수

한 클래스의 모든 instance가 똑같은 값을 가지고 있는 속성



클래스의 이름 대신 인스턴스 이름을 쓰면?

* 인스턴스 변수



클래스 속성(attribute)

* 한 클래스의 모든 인스턴스라도 똑같은 값을 가지고 있는 속성

클래스 선언 내부에서 정의

\<classname>.\<name>으로 접근 및 할당

```python
class Circle:
    pi = 3.14

c1 = Circle()
c2 = Circle()

print(Circle.pi)
print(c1.pi)
print(c2.pi)

3.14
3.14
3.14
```



### 인스턴스 메소드

self 매개변수를 통해 동일한 객체에 정의된 속성 및 다른 메소드에 자유롭게 접근 가능

클래스자체에도 접근 가능 → <u>인스턴스 메소드가 클래스 상태를 수정</u>할 수도 있음



### 클래스 메소드

클래스가 사용할 메소드

@classmethod 데코레이터를 사용하여 정의

* 데코레이터 : 함수를 어떤 함수로 꾸며서 새로운 기능을 부여

호출 시, 첫번째 인자로 클래스(cls)가 전달됨

```python
class MyClass:				# 클래스 이름 : pascal_case
    var = 'Class 변수'
    @classmethod
    def class_method(cls):	# 함수 이름 : snake_case
        print(cls.var)
        return cls
    
MyClass.class_method()
MyClass

Class 변수
__main__.MyClass
__main__.MyClass
```



### 스태틱 메소드

스태틱 메소드

* 인스턴스 변수, 클래스 변수를 전혀 다루지 않는 메소드

언제 사용하는가?

* 속성을 다루지 않고 단지 기능(행동)만을 하는 메소드를 정의할 때, 사용

클래스가 사용할 메소드

@staticmethod 데코레이터를 사용하여 정의

호출 시, **어떠한 인자도 전달되지 않음(클래스 정보에 접근/수정 불가)**

```python
class MyClass:
    @staticmethod
    def static_method():
        return 'static'        
MyClass.static_method() 

'static'
```



```python
class MyClass:
    
    # 함수는 기본적으로 local scope
    # 내부에서 활용하고 싶으면 parameter로 받도록 정의
    
    # instance method : instance를 조작하고 싶다.
    # (python 제작자) 함수 내부에 instance를 던져주도록 설계
    # method를 정의할 때 self로 받도록
    def instance_method(self):
        return self
   	
    # class method : class를 조작하고 싶다.
    # (python 제작자) 함수 내부에 클래스를 던져주도록 설계
    # method를 정의할 때 cls를 받도록
    @classmethod
    def class_method(cls):
        print(cls.var)
        return cls
    
    # static method : class나 instance를 조작할 생각은 없는데 
    #				  함수를 만들어야한다.
    @staticmethod
    def static_method():
        return ''
```



### instance와 class 간의 이름 공간(namespace)

클래스를 정의하면, 클래스와 해당하는 이름 공간 생성 **python tutor참고**

인스턴스를 만들면, 인스턴스 객체가 생성되고 이름 공간 생성

인스턴스에서 특정 속성에 접근하면, 인스턴스-클래스 순으로 탐색



```python
#Person 정의
class Person:
    name = 'unknown'
    
    def talk(self):
        print(self.name)
        
p1 = Person()
p1.talk()
```

```python
# p2 인스턴스 변수 설정 전/후

p2 = Person()
p2.talk()
p2.name = 'Kim'
p2.talk()

print(Person.name)
print(p1.name)
print(p2.name)
```



### 정리

클래스 구현

* 클래스 정의
* 데이터 속성 정의 (객체의 정보는 무엇인지)
* 메소드 정의(객체를 어떻게 사용할 것인지)

클래스 활용

* 해당 객체 타입의 인스턴스 생성 및 조작



## 메소드

### 메소드 정리

Instance Method

self 매개변수를 통해 동일한 객체에 정의된 속성 및 다른 메소드에 자유롭게 접근 가능

클래스자체에도 접근 가능 → <u>인스턴스 메소드가 클래스 상태를 수정</u>할 수도 있음



Class Method

클래스를 가리키는 cls 매개 변수를 받음

cls 인자에만 접근할 수 있기 때문에 객체 인스턴스 상태를 수정할 수 없음



Static Method

임의개수의 매개변수를 받을 수 있지만, self나 매개변수는 사용하지 않음

객체 상태나 클래스 상태를 수정할 수 없음

일반 함수처럼 동작하지만 클래스의 이름공간에 귀속 됨

* 주로 해당 클래스로 한정하는 용도로 사용

```python
class MyClass:
    def method(self):
        return 'instance method', self
    @classmethod
    def classmethod(cls):
        return 'Class method', cls
    def staticmethod():
        return 'static method'
    
# instance method를 호출한 결과
obj = MyClass()
obj.method()
MyClass.method(obj)

# class자체에서 각 method를 호출하는 경우
Myclass.Classmethod()
MyClass.staticmethod()
MyClass.method()		#instance method는 호출할 수 없음

# instance는 클래스 메소드와 스태틱 메소드 모두 접근할 수 있음
obj.Classemethod()
MyClass.classmethod()
obj.staticmethod()
```



# 객체지향의 핵심개념

객체지향의 핵심 4가지

추상화

상속

다형성

캡슐화



## 추상화

현실 세계를 프로그램 설계에 반영

```python
# 학생(Student)을 표현하기 위한 클래스를 생성합니다.
class Student:
    def __init__(self, name, age, gpa):
        self.name = name
        self.age = age
        self.gpa = gpa
    def talk(self):
        print(f'반갑습니다.{self.name}입니다.')
    def study(self):
        self.gpa += 0.1
```

```python
# 교수(professor)을 표현하기 위한 클래스를 생성합니다.
class Professor:
    def __init__(self, name, age, department):
        self.name = name
        self.age = age
        self.department = department
    def talk(self):
        print(f'반갑습니다.{self.name}입니다.')
    def teach(self):
        self.age += 1
```

```python
class Person:
    
    def __init__(self, name, age):
        self.name = name
        self.age = age
        
    def talk(self):
        print(f'반갑습니다. {self.name}입니다.')
```



## 상속

: 두 클래스 사이 부모 - 자식 관계를 정립하는 것

클래스는 상속이 가능함

- **모든 python class는 object를 상속 받음**

```python
class ChildClass(ParentClass):
    pass
```



하위 클래스는 상위 클래스에 정의된 속성, 행동, 관계 및 제약 조건을 모두 상속 받음

부모클래스의 속성, 메소드가 자식 클래스에 상속되므로, 코드 재사용성이 높아짐

```python
class Person:    
    def __init__(self, name, age):
        self.name = name
        self.age = age
        
    def talk(self):
        print(f'반갑습니다. {self.name}입니다.')

class Professor(Person):
    def __init__(self, name, age, department):
        self.name = name
        self.age = age
        self.department = department
 
class Student(Person):
    def __init__(self, name, age, gpa):
        self.name = name
        self.age = age
        self.gpa = gpa
    def talk(self):
        print(f'{self.name}입니다. 교수님 ^^7')
        
p1 = Professor('박교수', 50, '컴퓨터공학과')
s1 = Student('김학생', 20, 3.5)

# 부모 Person 클래스의 talk 메서드를 활용
p1.talk()

# 부모 Person 클래스의 talk 메서드를 표현한다.
s1.talk()

반갑습니다. 박교수입니다.
김학생입니다. 교수님 ^^7
```



### 상속 관련 함수와 메소드

#### islnstance(object, classinfo)

* classinfo의 instance거나 subclass*인 경우 True

```python
# 상속 없는 경우
class Person:
    pass
class Professor:
    pass
class Student:
    pass

# 인스턴스 생성
p1 = Professor()
s1 = Student()

print(isinstance(p1, Person))
print(isinstance(p1, Professor))
print(isinstance(p1, Student))
print(isinstance(s1, Person))
print(isinstance(s1, Professor))
print(isinstance(s1, Student))

False
True
False
False
False
True
```

```python
# 상속 없는 경우
class Person:
    pass
class Professor(Person):
    pass
class Student(Person):
    pass

# 인스턴스 생성
p1 = Professor()
s1 = Student()

print(isinstance(p1, Person))
print(isinstance(p1, Professor))
print(isinstance(p1, Student))
print(isinstance(s1, Person))
print(isinstance(s1, Professor))
print(isinstance(s1, Student))

True
True
False
True
False
True
```



#### issubclass(class, classinfo)

* class가 classinfo의 subclass면 True
* classinfo는 클래스 객체의 튜플일 수 있으며, classinfo의 모든 항목을 검사

```python
print(issubclass(bool, int)) # True
print(issubclass(bool, float)) # False
print(issubclass(bool, (int, float))) # True
print(issubclass(bool, (float, int))) # True
# 둘 중하나가 True면 True가 나온다.
# in which case return True if class is a subclass of any entry in classinfo.
```



#### super()

* 자식클래스에서 부모클래스를 사용하고 싶은 경우
* super()를 사용할 경우 모두 다 받아와서 덮어씌우는 형태로 작성

<u>추가 기능을 구현하고 싶을 때</u>

```python
class Person:    
    def __init__(self, name, age, number, email):
        self.name = name
        self.age = age
        self.number = number
        self.email = email
        
class Student(Person):
    def __init__(self, name, age, number, email, student_id):
        self.name = name
        self.age = age
        self.number = number
        self.email = email
        self.student_id = student_id
```

```python
class Person:    
    def __init__(self, name, age, number, email):
        self.name = name
        self.age = age
        self.number = number
        self.email = email
        
class Student(Person):
    def __init__(self, name, age, number, email, student_id):
        #Person 클래스
        super().__init__(name, age, number, email)
        self.student_id = student_id
```



#### 상속 관련 정리

Python의 모든 클래스는 object로부터 상속됨

부모 클래스의 모든 **요소(속성, 메소드)가 상속**됨

**super()**를 통해 부모 클래스의 요소를 호출할 수 있음

메소드 오버라이딩을 통해 자식클래스에서 **재정의** 가능함

상속관계에서의 이름 공간은 instance, 자식 class, 부모 class 순으로 탐색



#### 다중 상속

두개 이상의 클래스를 상속 받는 경우

상속 받은 모든 클래스의 요소를 활용 가능함

중복된 속성이나 메서드가 있는 경우 <u>상속 순서에 의해 결정</u>됨

```python
class Person:
    def __init__(self, name):
        self.name = name

    def greeting(self):
        return f'안녕, {self.name}'
    
class Mom(Person):
    gene = 'XX'
    
    def swim(self):
        return '엄마가 수영'

class Dad(Person):
    gene = 'XY'
    
    def walk(self):
        return '아빠가 걷기'
    
class FirstChild(Dad, Mom):
    def swim(self):
        return '첫째가 수영'
    
    def cry(self):
        return '첫째가 응애'

baby1 = FirstChild('아가')
baby1.cry()		#'첫째가 응애'
baby1.swim()	#'첫째가 수영'
baby1.walk()	#'아빠가 걷기'
baby1.gene		#'XY'	Dad이 먼저 적혀있기 때문
```

```python
class SecondChild(Mom, Dad):
    def walk(self):
        return '둘째가 걷기'
    
    def cry(self):
        return '둘째가 응애'

baby2 = SecondChild('아가')
baby2.cry()		#'둘째가 응애'
baby2.swim()	#'엄마가 수영'
baby2.walk()	#'둘째가 걷기'
baby2.gene		#'XX'	Mom이 먼저 적혀있기 때문
```



#### 상속 관련 함수와 메소드

mro 메소드 (Method Resolution Order)

* 해당 인스턴스의 클래스가 어떤 부모 클래스를 가지는 지 확인하는 메소드
* 기존의 인스턴스 → 클래스 순으로 이름 공간을 탐색하는 과정에서 상속 관계에 있으면 인스턴스→ 자식 클래스 → 부모 클래스로 확장

```python
FirstChild.mro()
SecondChild.mro()

[__main__.FirstChild, __main__.Dad, __main__.Mom, __main__.Person, object]
[__main__.SecondChild, __main__.Mom, __main__.Dad, __main__.Person, object]
```



## 다형성

다형성(Polymorphism)이란?

* 여러 모양을 뜻하는 그리스어
* <u>동일한 메소드가 클래스에 따라 다르게 행동할 수 있음을 의미</u>
* 즉, 서로 다른 클래스에 속해있는 객체들이 <u>동일한 메시지에 대해 다른 방식으로 응답될 수 있음</u>



### 메소드 오버라이딩

상속 받은 메소드를 재정의

* 클래스 상속 시, 부모 클래스에서 정의한 메소드를 자식 클래스에서 변경
* 부모 클래스의 메소드 이름과 기본 기능은 그대로 사용하지만, 특정 기능을 바꾸고 싶을 때 사용
* 상속받은 클래스에서 같은 이름의 메소드로 덮어씀
* 부모 클래스의 메소드를 실행시키고 싶은 경우 super를 활용

```python
class Person:
    def __init__(self, name):
        self.name = name
        
	def talk(self):
        print(f'반갑습니다. {self.name}입니다.')
       
# 자식 클래스 - Professor
class Professor(Person):
    def talk(self):
        print(f'{self.name}일세.')
        
# 자식 클래스 - Student
class Student(Person):
    super().talk()
    print(f'저는 학생입니다.')
    
p1 = Professor('김교수')
p1.talk()

s1 = Student('이학생')
s1.talk()
```



## 캡슐화

객체의 일부 구현 내요에 대한 외부로부터 직접적인 액세스를 차단

* 예시 : 주민등록번호

<u>파이썬에서 암묵적으로 존재하지만, 언어적으로는 존재하지 않음</u>

```python
class Person:
    
    def get_name(self):
        return self.name
    
    def set_name(self, name):
        self.name = name
  
p2 = Person()
p2.set_name('한솔')
p2.get_name()

'한솔'
```



### 접근제어자 종류

Public Access Modifier : 어디서나

Protected Access Modifier : 상속관계

Private Access Modifier : 본인



#### Public Member

언더바가 없이 시작하는 메소드나 속성

어디서나 호출이 가능, 하위 클래스 **override** 허용

일반적으로 작성되는 메소드와 속성의 대다수를 차지

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = 30
        
# Person 클래스의 인스턴스인 p1은 name, age 모두 접근 가능합니다.

p1 = Person('김싸피', 30)
print(p1.name)
print(p1.age)

김싸피
30
```



#### Protected Member

**언더바 1개**로 시작하는 메소드나 속성

암묵적 규칙에 의해 부모 클래스 내부와 자식 클래스에서만 호출 가능

**하위 클래스 override 허용**

*밖에서 필요없는 정보이지만 메소드 내부에서는 그 정보를 사용해야할 수 있다.*

*이를 언급하기 위해서 Protected Member로 언더바 1개를 사용해서 표현*

*직접 호출할 필요없이 사용한 것을 가공해서 보여줄 것으로 숨겨두는 것*

*이를 개발자가 사용자나 다른 개발자에게 알려주는 것*

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self._age = age
        
    def get_age(self):
        return self._age
    
# 인스턴스를 만들고 get_age 메서드를 활용하여 호출할 수 있습니다.
# 실행시켜 확인해보세요.
p1 = Person('김싸피', 30)
p1.get_age()

# _age에 직접 접근하여도 확인이 가능합니다.
# python에서는 암묵적으로 활용될 뿐입니다.
p1._age

30
30
```



### Private Member

**언더바 2**개로 시작하는 메소드나 속성

<u>본 클래스 내부에서만 사용이 가능</u>

<u>하위클래스 상속 및 호출 불가능(오류)</u>

<u>외부 호출 불가능(오류)</u>

*하위클래스에게 사용하지 못함을 직접적으로 언급하는 것*

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.__age = age
        
    def get__age(self):
        return self.__age

# 인스턴스를 만들고 get__age 메서드를 활용하여 호출할 수 있습니다.
# 실행시켜 확인해보세요.
p1 = Person('김싸피', 30)
p1.get__age()

# __age에 직접 접근이 불가능합니다.
p1.__age    

30
AttributeError                            Traceback (most recent call last)
Input In [112], in <module>
     12 p1.get__age()
     14 # __age에 직접 접근이 불가능합니다.
---> 15 p1.__age

AttributeError: 'Person' object has no attribute '__age'
```



### getter 메소드와 setter 메소드

**변수**에 <u>접근할 수 있는 메소드</u>를 별도로 생성

* getter method : 변수의 값을 읽는 메소드
  * @property 데코레이터 사용
* setter method : 변수의 값을 설정하는 성격의 메소드
  * @변수.setter 사용

```python
class Person:
    def __init__(self, age):
        self._age = age
        
    @property
    def age(self):
        return self._age
    
    @age.setter
    def age(self, new_age):
        if new_age <= 19:
            raise ValueError('Too Young For enter')
            return    
        self._age = new_age
```

```python
p1 = Person(10)
p1.age()

TypeError                                 Traceback (most recent call last)
Input In [124], in <module>
      1 p1 = Person(10)
----> 2 p1.age()

TypeError: 'int' object is not callable
```

```python
p1.age # method를 정의했는데 속성처럼 쓰이도록 한다.

10
```

```python
# Person의 인스턴스를 만들어서 나이에 접근하면 정상적으로 출력됩니다.
p1 = Person(20)
print(p1.age)

20
```

```python
# p1 인스턴스의 나이를 다른 값으로 바꿔도 정상적으로 반영됩니다.
p1.age = 33
print(p1.age)

33
```

```python
# setter 함수에는 '나이가 19살 이하면 안된다는' 조건문이 하나 걸려있습니다.
# 따라서 나이를 19살 이하인 값으로 변경하게 되면 오류가 발생합니다.
p1.age = 19
print(p1.age)
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
Input In [128], in <module>
----> 1 p1.age = 19
      2 print(p1.age)

Input In [123], in Person.age(self, new_age)
      9 @age.setter
     10 def age(self, new_age):
     11     if new_age <= 19:
---> 12         raise ValueError('Too Young For enter')
     13         return
     15     self._age = new_age

ValueError: Too Young For enter
```



python문서 확인하면 도움될 것
