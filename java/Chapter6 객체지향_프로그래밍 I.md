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

✔ 반환타입이 void가 아닌 경우, 반드시 return문 필요하다.

