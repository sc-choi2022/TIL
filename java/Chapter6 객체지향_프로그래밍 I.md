### 객체지향_프로그래밍 I

#### 객체지향 언어

빠른 변화에 따라가기 위한 해결책으로 객체지향 언어를 도입

절차적 :arrow_right:객체지향

코드의 재사용성이 높고 유지보수가 용이, 중복 코드 제거

객체지향 언어 = 프로그래밍 언어 + 객체지향개념(규칙)

OOP(Object-Oriented Programming)

객체지향언어의 핵심적인 개념

1. 캡슐화
2. 상속
3. 추상화
4. 다형성 ✔



Q 객체지향 개념은 어떻게 공부해야 하나요?

객체지향개념(규칙)을 외는 것이 필요하다.

코딩을 하는 것에 필요하기 때문에 자주 보면서 외우는 것을 추천

객체지향을 이해한 후에는 JSP, Spring (웹)/ Android(모바일)로 실습하며 익히는 것을 추천한다.



cf) 디자인패턴

객체지향 개념을 이용해서 프로그래밍을 할 때 자주 쓰는 패턴들을 모아둔 것



#### 클래스와 객체

**클래스의 정의**

객체를 정의해 놓은 것

**클래스의 용도**

객체를 생성하는 것에 사용

**객체**

실제로 존재하는 것, 사물 또는 개념

**객체의 용도**

객체가 가지고 있는 기능과 속성에 따라 다르다.

| 클래스      | 객체 |
| ----------- | ---- |
| 제품 설계도 | 제품 |
| TV 설계도   | TV   |



#### 객체의 구성요소 - 속성과 기능

객체 = 속성(변수) + 기능(메서드)

![image-20220806225444539](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220806225444539.png)



#### 객체와 인스턴스

객체 : 모든 인스턴스를 대표하는 일반적 용어

인스턴스 : 특정 클래스로부터 생성된 객체(예: Tv인스턴스)

![image-20220806225606360](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220806225606360.png)



#### 하나의 소스파일에 여러 클래스 작성

![image-20220806225922724](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220806225922724.png)

일반적으로 하나의 소스파일에는 하나의 클래스를 작성한다. (1:1)

![image-20220807024831247](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220807024831247.png)



#### 객체의 생성과 사용

**객체의 생성**

```java
클래스명 변수명;			// 클래스의 객체를 참조하기 위한 참조변수를 선언
변수명 = new 클래스명();	// 클래스의 객체를 생성 후, 객체의 주소를 참조변수에 저장

Tv t;					// Tv클래스 타입의 참조변수 t을 선언
t = new Tv();			// Tv인스턴스를 생성한 후, 생성된 Tv인스턴스의 주소를 t에 저장
```



**객체의 사용**

객체의 변수, 메서드를 사용한다는 의미이다.

```java
t.channel = 7;			// Tv인스턴스의 멤버변수 channel의 값을 7로 한다.
t.channelDown();		// Tv인스턴스의 메서드 channelDown()을 호출한다.
System.out.println("현재 채널은 " + t.channel + " 입니다.");
```



```java
class Tv {
    String color;	// 색깔
    boolean power;	// 전원상태
    int channel;	// 채널
    
    void power() {
        power = !power;
    }
    
    void channelUp() {
        channel++;
    }
    
    void channelDown() {
        channel--;
    }
}
```

1. 클래스 작성
2. 객체 생성
3. 객체 사용



![image-20220904224425056](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220904224425056.png)

```java
class Tv {
    String color;	// 색깔
    boolean power;	// 전원상태
    int channel;	// 채널
    
    void power(){
        power = !power;
    }
    
    void channelUp(){
        channel++;
    }
    
    void channelDown(){
        channel--;
    }
}
```

Tv 객체

✔ 변수 3개 메소드 3개 => 6개의 멤버



```java
Tv t;			// Tv클래스 타입의 참조변수 t를 선언
t = new Tv();	// Tv인스턴스를 생성한 후, 생성된 Tv인스턴스의 주소를 t에 저장

t.channel = 7;	// Tv인스턴스의 멤버변수 channel의 값을 7로 한다.
t.channelDown();// Tv인스턴스의 메소드 channelDown()를 호출한다.

System.out.println("현재 채널은 " + t.channel + " 입니다.");
```



#### 객체의 생성과 사용 - 예제

```java
Tv t1 = new Tv();
Tv t2 = new Tv();
t1.channel = 7;

System.out.println("현재 채널은 " + t1.channel + " 입니다.");	//	7
System.out.println("현재 채널은 " + t2.channel + " 입니다.");	//	0
```

![image-20220907223255210](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220907223255210.png)

각 변수는 별도에 저장공간에 저장된다.



만약`t2 = t1;`이 추가된다면

```java
Tv t1 = new Tv();
Tv t2 = new Tv();
t2 = t1;
t1.channel = 7;
System.out.println("현재 채널은 " + t1.channel + " 입니다.");	//	7
System.out.println("현재 채널은 " + t2.channel + " 입니다.");	//	7
```

![image-20220907223721525](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220907223721525.png)

더이상 참조변수(t2)와 주소(0x200)는 관계가 없게 된다.

객체는 참조변수없이 사용할 수 없다.

사용할 수 없는 메모리는 Garbage Collector가 주기적으로 메모리를 확인하고 메모리에서 제거하여 불필요하게 낭비되는 메모리가 없게한다.

따라서 필요 시 만들어 사용하고 메모리 정리는 Garbage Collector가 하게된다.

✔ 하나의 인스턴스를 여러 개의 참조변수가 가리키는 경우(가능)

✔ 여러개의 인스턴스를 하나의 참조변수가 가리키는 경우(불가능)

![image-20220907224218657](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220907224218657.png)



#### 객체 배열

객체 배열 == 참조변수 배열

```java
Tv tv1, tv2, tv3;
Tv[] tvArr = new Tv[3];	// 길이가 3인 Tv타입의 참조변수 배열

//	객체를 생성해서 배열의 각 요소에 저장
tvArr[0] = new Tv();
tvArr[1] = new Tv();
tvArr[2] = new Tv();

// 한줄로 작성하면
Tv[] tvArr = { new Tv(), new Tv(), new Tv()};
```

![image-20220917215712246](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220917215712246.png)



#### 클래스의 정의

클래스 == 데이터 + 함수

1. 설계도
2. 데이터 + 함수
3. 사용자 정의 타입



**1. 변수**	하나의 데이트를 저장할 수 있는 공간

**2. 배열**	같은 종류의 여러 데이터를 하나로 저장할 수 있는 공간

**3. 구조체**	서로 관련된 여러 데이터(종류 관계X)를 하나로 저장할 수 있는 공간

**4. 클래스**	데이터와 함수의 결합(구조체 + 함)

![image-20220917221335523](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220917221335523.png)

##### 사용자 정의 타입

원하는 타입을 직접 만들 수 있다.

```java
class Time{
    int hour;
    int minute;
    int second;
}

Time t = new Time();
```

![image-20220917221758044](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220917221758044.png)



#### 선언위치에 따른 변수의 종류

![image-20220917221946085](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220917221946085.png)

**영역**

**클래스 영역**

* **instance variable**, 인스턴스 변수
* **class variable**, 클래스 변수(static 변수, 공유변수)

**메서드 영역**

* **local variable**, 지역변수

![image-20220917222519535](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220917222519535.png)

✔ **iv가 생성되는 시기는 인스턴스가 생성되었을 때이다.**

클래스 영역의 변수 - 인스턴스 변수(iv)

클래스 영역의 static이 붙의 변수 - 클래스 변수(cv)



**class variable** & **instance variable**

cv: 객체생성필요x, 아무때나 사용가능

iv: 객체생성필요, 객체생성을 해야 사용가능

객체는 iv변수의 묶음



#### 클래스 변수와 인스턴스 변수

```java
class Card {
    // 개별 속성은 인스턴스 변수
    String kind;	// 무늬
    int number;		// 숫자
    
    // 공통 속성은 클래스 변수
    static int width = 100;		// 폭
    static int height = 250;	// 높이
}
```

```java
// 객체 생성
Card c = new Card();
// 객체 사용 - 인스턴스 변수
c.kind = "HEART";
c.number = 5;
// 객체 사용 - 클래스 변수
// 클래스이름.속성
Card.width = 200;
Card.height = 300;
```



#### 메서드란?

**1. 문장들을 묶어놓은 것**

* 작업단위로 문장들의 묶어서 이름 붙인 것

**2. 값(입력)을 받아서 처리하고, 결과를 반환(출력)**

![image-20220917224623309](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220917224623309.png)

cf)

메서드는 객체지향개념에서 함수를 의미한다.

메서드는 클래스안에 있어야한다.

함수는 클래스에 독립적이다.



##### 메서드의 장점

* 코드의 중복을 줄일 수 있다.
* 코드의 관리가 쉽다.
* 코드를 재사용할 수 있다.
* 코드가 간결해서 이해하기 쉬워진다.



##### 메서드를 작성

* 반복적으로 수행되는 여러 문장을 메서드로 작성한다.
* 하나의 메서드는 한 가지 기능만 수행하도록 작성한다.



**메서드 = 선언부 + 구현부**

![image-20220917225015454](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220917225015454.png)

반환타입: 작업결과 타입

* 반환 타입은 1개

* 반환 타입이 없을 경우 void

매개변수(입력): 작업에 필요한 값들



#### 메서드의 구현부

**지역변수(Iv)**: 메서드 내에 선언된 변수

다른 메서드 영역에서는 매개변수의 이름이 같아도 된다.

매개변수도 지역변수이다.



#### 메서드의 호출

```java
// 메서드이름(값1, 값2, ...);

print99danAll();		// void print99danAll()을 호출
int result = add(3, 5);	
// int add(int x, int y)를 호출하고 결과를 result에 저장
// 작업결과를 사용하기 위해 저장할 변수가 필요하다.
```



#### 메서드의 실행흐름

![image-20220917230401866](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220917230401866.png)



#### return문

실행 중인 메서드를 종료하고 호출한 곳으로 되돌아간다.

✔ 메서드가 작업을 마쳤을 때 return을 사용해야한다.

✔ 반환 타입이 void인 경우 생략가능, 컴파일러가 자동으로 추가한다.

✔ 반환 타입이 void가 아닌 경우, 반드시 return문 필요하다.

```java
int max(int a, int b){
    if(a > b)
        return b;
}
```

위 코드는 에러가 발생한다. false일 때 return문이 없기 때문이다.



#### 반환값

![image-20220919123517023](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220919123517023.png)

반환타입과 return 타입이 일치되거나 자동형변환이 가능해야한다.

예를 들어

* char
* byte
* short



#### 호출 스택(call stack)

스택(stack): 밑이 막힌 상자. 위에 차곡차곡 쌓인다.

**값을 stack에 넣는 경우**

![image-20220919123749161](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220919123749161.png)

**값을 stack에서 꺼내는 경우**

![image-20220919123841086](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220919123841086.png)



호출스택(call stack)

메서드 수행에 필요한 메모리가 제공되는 공간

메서드가 호출되면 호출스택에 메모리 할당, 종료되면 해제된다.

![image-20220919123957692](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220919123957692.png)

![image-20220919124325940](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220919124325940.png)

아래 있는 메서드가 위의 메서드를 호출한 것으로

맨 위의 메서드 하나만 실행 중이고, 나머지는 대기중이다.

![image-20220919124542053](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220919124542053.png)



#### 기본형 매개변수

기본형 매개변수

* 변수의 값을 읽기만 할 수 있다. (read only)
* 변경이 불가능하다.
* 8개 종류

참조형 매개변수

* 변수의 값을 읽고 변경할 수 있다. (read & write)

```java
class Data { int x; }

class Ex6_6 {
    public static void main(String[] args){
        Data d = new Data();
        d.x = 10;
        System.out.println("After change(d.x)");
        System.out.println("main() : x = "+ d.x);
    }
    
    static void change(int x){	// 기본형 매개변수: 읽기만 가능하다.
        x = 1000;
        System.out.println("change() : x = " + x);
    }
}
```

**결과**

✔ 기본형 매개변수: 읽기만 가능하다.

```
main() : x = 10
change() : x = 1000
After change(d.x)
main() : x = 10
```



#### 참조형 매개변수

참조형 매개변수 - 변수의 값을 읽고 변경할 수 있다.(read & write)

```java
class Data2 { int x };

class Ex6_7 {
    public static void main(String[] args){
        Data2 d = new Data2();
        d.x = 10;
        System.out.println("main() : x = " + d.x);
        
        change(d);
        System.out.println("After change(d)");
        System.out.println("main() : x = " + d.x);
    }
    
    static void change(Data2 d){	// 참조형 매개변수
        d.x = 1000;
        System.out.println("change() : x = " + d.x);
    }
}
```

**결과**

```
main() : x = 10
change() : x = 1000
After change(d)
main() : x = 1000
```



#### 참조형 반환타입

```java
class Data2 { int x };

class Ex6_8 {
    public static void main(String[] args){
        Data3 d = new Data3();
        d.x = 10;
        
        Data3 d2 = copy(d);
        System.out.println("d.x ="+d.x);
        System.out.println("d2.x=" + d2.x);
    }
    
    static Data3 copy(Data3 d){
        Data3 tmp = new Data3();	// 새로운 객체 tmp를 생성한다.
        
        tmp.x = d.x;	// d.x의 값을 tmp.x에 복사한다.
        
        return tmp;		// 반환값이 참조형인 경우 : 복사한 객체의 주소를 반환한다.
    }
}
```

✔ static method: 객체 생성없이 호출가능

**결과**

✔ 반환값이 참조형인 경우 : 복사한 객체의 주소를 반환한다.

```
d.x = 10
d2.x = 10
```



#### static 메서드와 인스턴스 메서드

```java
class MyMath2 {
    long a, b;			// iv 인스턴스 변수
    
    long add(){			// 인스턴스 메서드
        return a + b;
    }
    // 클래스 메서드(static 메서드)
    static long add(long a, long b){	// a, b 지역변수(lv)
        return a + b;
    }
}
```



✔ **인스턴스 메서드**: static이 붙지 않은 method

* 인스턴스 생성 후, '참조변수.메서드이름()'으로 호출
* 인스턴스 멤버(iv, im)와 관련된 작업을 하는 메서드
* 메서드 내에서 인스턴스 변수(iv) 사용가능

✔ **클래스 메서드**: static이 붙은 method

* 객체생성없이 '클래스이름.메서드이름()'으로 호출
* 인스턴스 멤버(iv, im)와 관련없는 작업을 하는 메서드
* 메서드 내에서 인스턴스 변수(iv) 사용불가

```java
class MyMathTest2 {
    public static void main(String args[]){
        System.out.println(MyMath2.add(200L, 100L));	// 클래스메서드 호출
        MyMath2 mm = new MyMath2();		// 인스턴스 생성
        mm.a = 200L;
        mm.b = 100L;
        System.out.println(mm.add());	// 인스턴스메서드 호출
    }
}
```



#### static을 언제 붙여야 할까?

![image-20220925215430638](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220925215430638.png)

인스턴스 멤버(iv, im)을 사용하지 않는 메서드에 static을 붙인다.

![image-20220925215528054](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220925215528054.png)



#### 메서드 간의 호출과 참조

static 메서드는 인스턴스 메서드(im)를 사용할 수 없다.

```java
class TestClass {   
    void instanceMethod(){}			// 인스턴스메서드
    static void staticMethod(){}	// static메서드
    
    void instanceMethod2(){			// 인스턴스메서드
        instanceMethod();			// 다른 인스턴스메서드를 호출한다.
        staticMethod();				// static메서드를 호출한다.
    }
    
    static void staticMethod2(){	// static메서드
        instanceMethod();			// !!인스턴스메서드를 호출할 수 없다.
        staticMethod();				// static메서드는 호출할 수 있다.
    }
}
```



static 메서드는 인스턴스 변수(iv)를 사용할 수 없다.

```java
class TestClass2 {
    int iv;			// 인스턴스 변수
    static int cv;	// 클래스 변수
    
    void instanceMethod(){			// 인스턴스 메서드
        System.out.println(iv);		// 인스턴스 변수를 사용할 수 있다.
        System.out.println(cv);		// 클래스 변수를 사용할 수 있다.
    }
    
    static void staticMethod(){		// 클래스 메서드
        System.out.println(iv);		// !! 인스턴스 변수를 사용할 수 없다.
        System.out.println(cv);		// 클래스 변수를 사용할 수 있다.
    }
}
```



Q. static메서드는 static메서드 호출가능?

**YES**

Q. static메서드는 instance변수 호출가능?

**NO**

Q. static메서드는 instance메서드 호출가능?

**NO**

Q. 왜 static메서드는 인스턴스 멤버를 쓸 수 없나요?

**static메서드 호출시 객체(iv묶음)가 없을 수 있기 때문이다.**



#### 오버로딩(overloading)

한 클래스 안에 같은 이름의 메서드 여러 개를 정의하는 것

**오버로딩 성립하기 위한 3가지 조건**

1. 메서드 이름이 같아야한다.
2. 매개변수의 개수 또는 타입이 달라야 한다.
3. 반환 타입은 영향이 없다.

❗ 2번째 조건이 성립하지 않는 경우

```java
int add(int a, int b) { return a+b; }
int add(int x, int y) { return x+y; }
```

✔ ambiguous한 경우는 확인하자

예) The method add(int, long) is ambiguous for the type MyMath3



✔ 오버로딩 가능한 경우의 예

매개변수는 다르지만 같은 의미의 기능 수행

```java
class MyMath3 {
    int add(int a, int b){
        System.out.print("int add(int a, int b) - ");
        return a+b;
    }
    
    long add(long a, long b){
        System.out.print("long add(long a, long b) - ");
        return a+b;
    }
    
    int add(int[] a){			// 배열의 모든 요소의 합을 결과로 돌려준다.
        System.out.print("int add(int[] a) - ");
        int result = 0;
        for(int i=0; i<a.length; i++)
            result += a[i];
        return result;
    }
}
```



#### 생성자(constructor)

인스턴스가 생성될 때마다 호출되는 **인스턴스 초기화 메서드**

```java
Time t = new Time();
t.hour = 12;
t.minute = 34;
t.second = 56;
```

인스턴스 생성시 수행할 작업(iv 초기화)에 사용

```java
Time t = new Time(12, 34, 56);	// 생성자 호출
```



✔ 생성자의 이름은 클래스의 이름과 같아야 한다.

✔ 리턴값이 없다. (void를 붙이지 않는다.)

✔ 모든 클래스는 반드시 생성자를 가져야한다.

```java
class Card{
    Card(){							// 매개변수 없는 생성자
        // 인스턴스 초기화 작업
    }
    
    Card(String kind, int number){	// 매개변수 있는 생성자
        // 인스턴스 초기화 작업
    }
}
```



##### 기본 생성자(default constructor)

매개변수가 없는 생성자

```java
클래스이름(){}	// 기본생성자
Point(){}		// Point클래스의 기본 생성자
```



생성자가 하나도 없을때만, 컴파일러가 기본 생성자를 자동으로 추가한다.

```java
class Data_1{
    int value;
}

class Data_2{
    int value;
    
    Data_2(int x){	// 매개변수가 있는 생성자
        value = x;
    }
}

class Ex6_11 {
    public static void main(String[] args){
        Data_1 d1 = new Data_1();
        Data_2 d2 = new Data_2();	// compile error발생
    }
}
```

**결과**

```
Ex6_11.java:15: cannot resolve symbol
symbol : constructor Data_2 ()
location: class Data_2
			Data_2 d2 = new Data_2();
```

✔ Data_1 클래스는 생성자가 존재하지 않기 때문에, 컴파일러가 기본 생성자를 자동으로 추가해주었다.

✔ Data_2 클래스에 기본 생성자 `Data_2(){}`을 추가해주어야한다.



#### 매개변수가 있는 생성자

```java
class Car{
    String color;			// 색상
    String gearType;		// 변속기 종류 - auto(자동), manual(수동)
    int door;				// 문의 개수
    
    Car(){}	// 기본 생성자
    Car(String c, String g, int d){	// 매개변수가 있는 생성자
        color = c;
        gearType = g;
        door = d;
    }
}
```

![image-20220925224247137](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220925224247137.png)

✔ `new`: 객체 생성

✔ `Car("white", "auto", 4)`: 객체 초기화, 생성자 호출

✔ `=`: 대입(연결)



#### 생성자 this()

생성자에서 다른 생성자 호출할 때 사용

다른 생성자 호출시 첫 줄에서만 사용가능

```java
class Car2 {
    String color;			// 색성
    String gearType;		// 변속기 종류 - auto(자동), manual(수동)
    int door;				// 문의 개수
    
    Car2(){	// Car2(String color, String gearType, int door)를 호출
        this("white", "auto", 4);
    }
    
    Car2(String color){	// Car2(String color, String gearType, int door)를 호출
        this(color, "auto", 4);
    }
    
    Car2(String color, String gearType, int door){
        this.color = color;
        this.gearType = gearType;
        this.door = door;
    }
}
```



❗ 다른 생성자 호출시 첫 줄에서만 사용가능

```java
Car(String color){
    door = 5;
    Car(color, "auto", 4);	// 에러 발생
}
```

1. 첫 줄에서 사용하지 않았다.
2. class이름 대신this를 사용하지 않았다.

코드의 중복을제거하기 위해 생성자를 통해 호출한다.

![image-20220925225121989](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220925225121989.png)



#### 참조변수 this

❗ this() 생성자와 다르다.

인스턴스 자신을 가리키는 참조변수

인스턴스 메서드(생성자 포함)에서 사용가능하다.

지역변수(lv)와 인스턴스 변수(iv)를 구별할 때 사용한다.

![image-20220925225430715](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220925225430715.png)

**iv**

* this.color
* this.gearType
* this.door

✔ 같은 클래스 내에서 생략이 가능하다.

✔ 오른쪽 예시처럼 구분을 위해서 this를 사용(this.참조변수(변수이름))

**lv**

* String color
* String gearType
* int door
* color
* gearType
* door



#### 참조변수 this와 생성자 this()

**this**

* 인스턴스 자신을 가리키는 참조변수, 인스턴스의 주소가 저장되어 있다.

* 모든 인스턴스 메서드에 지역변수로 숨겨진 채로 존재한다.(this을 선언하지 않아도 사용 가능하다)

**this(), this(매개변수)**

* 생성자

* 같은 클래스의 다른 생성자를 호출할 때 사용한다.

✔ this와 this()는 비슷하게 생겼을 뿐 완전히 다른 것이다.

✔ this는 '참조 변수'

✔ this()는 '생성자'



#### 변수의 초기화

지역변수(lv)는 수동 초기화 해야한다. **(사용전 꼭!!!)**

멤버변수(iv, cv)는 자동 초기화 된다.

```java
class InitTest{
    int x;			// 인스턴스 변수 
    int y = x;		// 인스턴스 변수
    
    void method1(){
        int i;		// 지역변수
        int j = i;	// 에러. 지역변수를 초기화하지 않고 사용
    }
}
```

✔ 인스턴스 변수 - 자동

✔ 지역변수 - 수동



자동 초기화는 Type에 따라 기본값이 다르다.

기본적으로 0으로 초기화된다.

![image-20220926230524856](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220926230524856.png)

#### 멤버변수의 초기화

멤버변수(iv, ic)

##### 1. 명시적 초기화(=)

대입연산자를 이용하여 초기화, 선언시

```java
class Car{
    int door = 4;				// 기본형(primitive type) 변수의 초기화
    Engine e = new Engine();	// 참조형(reference type) 변수의 초기화
}
```

✔ 참조형 변수의 기본값은 null

✔ 참조형 변수의 초기화는 객체를 생성해서 넣어주어야한다.



##### 2. 초기화 블럭

* 인스턴스 초기화 블럭: {} - **iv**

* 클래스 초기화 블럭: static{} - **cv**

```java
class StaticBlockTest {
    static int[] arr = new int[10];	// 명시적 초기화 = 간단 초기화
    
    static {	// 클래스 초기화 블럭 - 배열 arr을 난수로 채운다. = 복잡 초기화
        for (int i=0; i<arr.length; i++){
            arr[i] = (int)(Math.random()*10)+1;
        }
    }
}
```



##### 3. 생성자

iv 초기화, 복잡한 초기화에 사용

```java
Car(Stirng color, String gearType, int door){	// 매개변수 있는 생성자
    this.color = color;
    this.gearType = gearType;
    this.door = door;
}
```



##### 정리하면

1. 자동초기화 **0**으로 초기화

2. 간단 초기화 **=**(대입연산자 이용)

3. 복잡 초기화: 

   **{}** : 많이 사용하지 않는다.

   **static{}** : cv

   **생성자** : iv



클래스 변수 초기화 시점

* 클래스가 처음 로딩될 때 단 한번
* 클래스가 메모리에 올라갈 때

인스턴스 변수 초기화 시점

* 인스턴스가 생성될 때 마다

```java
class InitTest {
    static int cv = 1;	// 명시적 초기화
    int iv = 1;			// 명시적 초기화
    
    static { cv = 2; }	// 클래스 초기화 블럭
    {	iv = 2; }		// 인스턴스 초기화 블럭
    
    InitTest(){			// 생성자
        iv = 3;
    }
}
```



`initTest it = new InitTest();`

![image-20220926232158280](Chapter6%20%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20I.assets/image-20220926232158280.png)

**클래스 초기화**

1. 자동 초기화
2. 간단 초기화(=)
3. 복잡 초기화 (static{})

**인스턴스 초기화**

4. 자동 초기화
5. 간단 초기화(=)
6. 복잡 초기화
7. 복잡 초기화



#### ❗ 초기화 순서

**cv 초기화 된 후 iv가 초기화된다.**

**자동 ▶ 간단 ▶ 복잡 순서로 초기화된다.**
