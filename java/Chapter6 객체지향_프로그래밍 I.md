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