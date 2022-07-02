### 연산자(Operator)

연산자: 연산을 수행하는 기호

피연산자: 연산자의 연산 수행 대상

**모든 연산자는 연산결과를 반환한다.**

![image-20220701224911503](Chapter3%20%EC%97%B0%EC%82%B0%EC%9E%90(Operator).assets/image-20220701224911503.png)

:heavy_check_mark: 기타: 3항연산자



#### 연산자의 우선순위

하나의 식(expression)에 연산자가 둘 이상 있을 때, 어떤 연산을 먼저 수행할 지를 자동 결정하는 것

![image-20220701225821568](Chapter3%20%EC%97%B0%EC%82%B0%EC%9E%90(Operator).assets/image-20220701225821568.png)



#### 연산자의 결합규칙

우선순위가 같은 연산자가 있을 때, 어떤 것을 먼저 연산하는지

:heavy_check_mark: 대입과 단항 연산자를 제외하면, 모두 **왼쪽 -> 오른쪽**

대입연산자의 예시

```java
x = y = 3
```



#### 연산자의 우선순위와 결합법칙 정리

**산술 > 비교 > 논리 > 대입. 대입은 제일 마지막에 수행된다.**

**단항(1) > 이항(2) > 삼항(3). 단항 연산자의 우선순위가 이항 연산자보다 높다.**

**단항 연산자와 대입 연산자를 제외한 모든 연산의 진행방향은 왼쪽에서 오른쪽이다.**



#### 증감 연산자

증가 연산자(++): 피연산자의 값을 1 증가시킨다.

감소 연산자(--): 피연산자의 값을 1 감소시킨다.

![image-20220701230620512](Chapter3%20%EC%97%B0%EC%82%B0%EC%9E%90(Operator).assets/image-20220701230620512.png)

:heavy_check_mark: 증감 연산자가 독립적으로 사용된 경우, 전위형과 후위형의 차이가 없다.



이해를 하기 위해서는 식을 분리하는 것도 도움이 된다.

![image-20220701230839154](Chapter3%20%EC%97%B0%EC%82%B0%EC%9E%90(Operator).assets/image-20220701230839154.png)

![image-20220701230848016](Chapter3%20%EC%97%B0%EC%82%B0%EC%9E%90(Operator).assets/image-20220701230848016.png)

```java
public class Ex3 {

	public static void main(String[] args) {
		int i=5, j=0;
		
		j = i++;	// 후위형
		System.out.println("j=i++; 실행, i=" + i + ", j=" + j);
		
		i = 5;
		j = 0;
		
		j = ++i;	// 전위형
		System.out.println("j=++i; 실행, i=" + i + ", j=" + j);
	}
}
```

**출력결과**

j=i++; 실행 후, i=6, j=5
j=++i; 실행 후 , i=6, j=6



**부호 연산자**

'-'는 피연산자의 부호를 반대로 변경

'+'는 아무런 일도 하지 않는다.(실제로 사용X)



#### 형변환 연산자

형변환: 변수 또는 상수의 타입을 다른 타입으로 변환하는 것

**(타입)피연산자**

예)

```java
double d = 85.4;
int score = int(d); 
```

![image-20220701232010715](Chapter3%20%EC%97%B0%EC%82%B0%EC%9E%90(Operator).assets/image-20220701232010715.png)

**유니코드 문자표**

![image-20220701232051200](Chapter3%20%EC%97%B0%EC%82%B0%EC%9E%90(Operator).assets/image-20220701232051200.png)



#### 자동 형변환

컴파일러가 자동으로 형변환해주는 것

**기존의 값을 최대한 보존할 수 있는 타입으로 자동 형변환된다.**

![image-20220701234329907](Chapter3%20%EC%97%B0%EC%82%B0%EC%9E%90(Operator).assets/image-20220701234329907.png)

```java
float f = 1234;	// int타입의 값을 float타입의 변수에 저장(불일치)
float f = (float)1234;	// 자동 형변환
```

```java
int i = 3.14f;	// 에러, 값 손실 발생
// 수동 형변환 필요
int i = (int)3.14f;
```

![image-20220701234151641](Chapter3%20%EC%97%B0%EC%82%B0%EC%9E%90(Operator).assets/image-20220701234151641.png)

```java
byte b = 100;	// OK. byte타입의 범위(-128~127)의 값 대입
byte b = (byte)100;	// OK. byte타입으로 자동 형변환하여 대입
```

```java
int i = 100;
byte b = i;			// 에러, int타입을 byte타입에 대입
byte b = (byte)i;	// OK. byte타입으로 형변환하여 대입
```

```java
byte b = 1000;		// 에러. byte타입의 범위(-128~127)를 벗어남
byte b = (byte)1000;// OK. 그러나 값 손실이 발생, 변수 b에 -24 저장
```



#### 사칙 연산자

나눗셈을 원하는 결과를 얻기 위해서는 두 숫자 중 하나는 float이어야한다. 

```java
10 / 4;		// 2
10 / 4.0f;	// 2.5f
```



#### 산술 변환

연산 전에 피연산자의 타입을 일치시키는 것

1. 두 피연산자의 타입을 같게 일치시킨다. (보다 큰 타입으로 일치)

   long + int :arrow_right: long + long :arrow_right: long

   float + int :arrow_right: float + float :arrow_right: float

   double + float :arrow_right: double + double :arrow_right: double

2. 피연산자의 타입이 int보다 작은 타입이면 int로 변환한다.

   byte + short :arrow_right: int + int :arrow_right: int

   char + short :arrow_right: int + int :arrow_right: int



####  반올림 Math.round()

실수를 소수점 첫째자리에서 반올림한 정수를 반환

```java
long result = Math.round(4.52);	// result에 5가 저장된다.
```

```java
double pi = 3.141592;
System.out.println((int)(pi*1000));	// 3141
System.out.println((int)(pi*1000)/1000.0)	// 3.141
```



#### 나머지 연산자 %

오른쪽 피연산자로 나누고 남은 나머지를 반환

나누는 피연산자는 0이 아닌 정수만 허용(부호는 무시된다.)

```java
System.out.println(10 % 8);		// 2
System.out.println(10 % -8);	// 2
```



#### 비교연산자 > < >= <= == !=

두 피연산자를 비교해서 true(참) 또는 false(거짓)을 반환

![image-20220702012409216](Chapter3%20%EC%97%B0%EC%82%B0%EC%9E%90(Operator).assets/image-20220702012409216.png)

![image-20220702012435394](Chapter3%20%EC%97%B0%EC%82%B0%EC%9E%90(Operator).assets/image-20220702012435394.png)



#### 문자열의 비교

문자열 비교에는 == 대신 equals()를 사용해야한다.

```java
String str1 = "abc";
String str2 = "abc";
System.out.println(str1==str1);			// true
System.out.println(str1.equals(str2))	// true
```

```java
String str1 = new String ("abc");
String str2 = new String ("abc");
System.out.println(str1==str1);			// false
System.out.println(str1.equals(str2))	// true
```



#### 논리 연산자 && ||

조건을 연결할 때 사용하는 연산자



**|| (OR결합)**: 피연산자 중 어느 한 쪽이 true이면 true을 결과로 얻는다.

**&& (AND결합)**: 피연산자 양쪽 모두 true이어야 true을 결과로 얻는다.

![image-20220702013335974](Chapter3%20%EC%97%B0%EC%82%B0%EC%9E%90(Operator).assets/image-20220702013335974.png)



#### 논리 부정 연산자 !

true를 false로, false를 true로 바꾼다.

![image-20220702013715503](Chapter3%20%EC%97%B0%EC%82%B0%EC%9E%90(Operator).assets/image-20220702013715503.png)



#### 조건 연산자 ? :

조건식의 결과에 따라 연산 결과를 달리한다.

**조건식 ? 식1 : 식2**

```java
result = (x > y) ? x: y;	// 괄호 생략 가능

```



#### 대입 연산자

오른쪽 피연산자를 왼쪽 피연산자에 저장 후 저장된 값을 반환



lvalue:  대입 연산자의 왼쪽 피연산자

rvalue: 대입 연산자의 오른쪽 피연산자



#### 복합 대입 연산자

대입 연산자와 다른 연산자를 하나로 축약

![image-20220702014658592](Chapter3%20%EC%97%B0%EC%82%B0%EC%9E%90(Operator).assets/image-20220702014658592.png)