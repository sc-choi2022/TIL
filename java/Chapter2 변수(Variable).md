## 변수

하나의 값을 저장할 수 있는 메모리 공간(메모리 = RAM)

### 변수의 선언

변수의 선언 이유

* 값(data)을 저장할 공간을 마련하기 위해서

변수의 선언 방법

`변수타입 변수이름;`

```java
int age;	// 정수(int)타입의 변수 age를 선언
```

### 변수에 값 저장하기

변수에 값 저장하기

```java
int age;	// 정수(int) 타입의 변수 age를 선언
age = 25;	// 변수 age에 25를 저장
int age = 25; 	// 위의 두 줄을 한 줄로
```

변수의 초기화: 변수에 처음으로 값을 저장하는 것

```java
int x = 0;
int y = 5;
int x = 0, y = 5;
```



**변수의 종류**

클래스 변수, 인스턴스 변수, 지역 변수

:heavy_check_mark: 지역 변수: 지역 변수는 읽기 전에 꼭! 초기화 해야한다. (컴파일 시 에러 발생)



### 변수의 값 읽어오기

변수의 값이 필요한 곳에 변수의 이름을 적는다.

```java
int year = 0, age = 14;
year = age + 2000;
year = 2014;
System.out.println(year);
```



### 변수의 타입

1 변수의 타입은 저장할 값의 타입에 의해 결정된다.

2 저장할 값의 타입과 일치하는 타입으로 변수를 선언한다.

```java
char ch = '가';	// char 문자타입
double pi = 3.14;	// double 실수타입
```



### 값의 타입

값

* 문자: char
* 숫자
  * 정수: byte, short, int, long
  * 실수: float, double
* 논리: boolean - true, false



### 변수, 상수, 리터럴

변수(variable): 하나의 값을 저장하기 위한 공간

상수(constant): **한 번만** 값을 저장 가능한 변수

리터럴(literal): 그 자체로 값을 의미하는 것

```java
int score = 100;
score = 200;
final int MAX = 100;	// MAX는 상수
MAX = 200;	// error
char ch = "A";
String str = "abc";
```

리터럴 - 100, 200, A, abc

변수  - score, ch, str

상수 - MAX

:heavy_check_mark:Problem 창에서 error를 확인할 수 있다.

* 에러메시지
* 소스파일이름
* 소스파일의 경로
* 에러가 발생한 라인



### 리터럴의 접두사와 접미사

접미사는 대소문자 구별안하지만 L은 대문자로 쓰는 경우가 많다.

| 종류   | 리터럴                       | 접미사                        |
| ------ | ---------------------------- | ----------------------------- |
| 논리형 | false, true                  | 없음                          |
| 정수형 | 123, 0b0101, 077, 0xFF, 100L | L<br />long을 의미            |
| 실수형 | 3.14, 3.0e8, 1.4f, 0x1.0p-1  | f(float), d(double, 생략가능) |
| 문자형 | 'A, '1', '\n'                | 없음                          |
| 문자열 | "ABC", "123", "A", "true"    | 없음                          |

문자형은 '', 문자열은 ""

:heavy_check_mark:

```java
byte b = 127;	// (byte: -128~127)
byte b = 128;	// error   
int i = 100;
int oct = 0100;		// 8진수 숫자 0으로 시작
int hex = 0x100;	// 16진수
long l = 10_000_000_000L;	// _는 큰 숫자를 나타낼 때 사용
long l = 100;
float f = 3.14f;
double d =3.14d;
```

1e3 = 1000.0



### 변수와 리터럴의 타입 불일치

1 범위가 '변수 > 리터럴' 인 경우, OK

```java
int i = 'A';	// int > char
long l = 123;	// long > int
double d = 3.14f;	// double > float
```

2 범위가 '변수 < 리터럴' 인 경우, **에러**

```java
int i = 30_0000_0000;
long l =3.14f;
float f = 3.14;
```

3 byte, short 변수에 int리터럴 저장가능

:heavy_check_mark: 접미사는 출력되지 않는다.



### 문자와 문자열

```java
char ch = 'A';
char ch = 'AB';		// 에러
String s = "ABC";
String s1 = "AB";
String s2 = new String("AB");	// 위에 문장을 더 잘 사용한다.

String s = "";	// 빈 문자열
char ch = '';	// 에러

String s1 = "A" + "B";	// "AB"
```

문자열 + any type = 문자열

any type + 문자열 = 문자열



### 두 변수의 값 교환하기

```java
int x = 10, y = 20;
int tmp;
tmp = x;	// x의 값을 tmp에 저장
x = y;		// x의 값을 y에 저장
y = tmp;	// tmp의 값을 y에 저장
```



### 값의 타입

값(data)

* 문자: char
* 숫자
  * 정수: byte, short, int, long
  * 실수: float, double

### 기본형과 참조형

**기본형(Primitive type)**

오직 8개(boolean, char, byte, short, int, long, float, double)

실제 값을 저장

**참조형(Reference type)**

기본형을 제외한 나머지(String, System 등)

메모리 주소를 저장(4 byte 또는 8 byte)

:heavy_check_mark:4byte = 40억 = 4GB

```java
Data todya;			// 참조형 변수 today를 선언
today = new Date();	// today 객체의 주소를 저장
```



### 기본형(Primitive type) - 종류와 크기

**논리형** - true와 false 중 하나를 값으로 갖으며, 조건식과 논리적 계산에 사용한다.

**문자형** - 문자를 저장하는데 사용되며, 변수 당 하나의 문자만을 저장할 수 있다.

**정수형** - 정수 값을 저장하는데 사용된다. 주로 사용하는 것은 int와 long이며 byte는 이진 데이터를 다루는 데 사용되며, short은 c언어와의 호환을 위해 추가 되었다.

**실수형** - 실수 값을 저장하는데 사용된다. float와 double이 있다.

| 종류\크기 | 1       | 2     | 4     | 8      |
| --------- | ------- | ----- | ----- | ------ |
| 논리형    | boolean |       |       |        |
| 문자형    |         | char  |       |        |
| 정수형    | byte    | short | int   | long   |
| 실수형    |         |       | float | double |



#### 기본형(Primitive type) - 표현범위

![image-20220629082858904](Chapter2%20%EB%B3%80%EC%88%98(Variable).assets/image-20220629082858904.png)

1 bit - 0, 1

2 bit - 00, 01, 10, 11

n비트로 표현할 수 있는 값의 개수: 2^n개

n비트로 표현할 수 있는 부호없는 정수의 범위: 0 ~ n^2 -1

n비트를 표현할 수 있는 부호있는 정수의 범위: -2^(n-1) ~ 2^(n-1)-1



**byte**

![image-20220629090910125](Chapter2%20%EB%B3%80%EC%88%98(Variable).assets/image-20220629090910125.png)

**short & char**

![image-20220629091204597](Chapter2%20%EB%B3%80%EC%88%98(Variable).assets/image-20220629091204597.png)

**int**

![image-20220629092528962](Chapter2%20%EB%B3%80%EC%88%98(Variable).assets/image-20220629092528962.png)

**long**

![image-20220629093209118](Chapter2%20%EB%B3%80%EC%88%98(Variable).assets/image-20220629093209118.png)



:red_circle:정수형과 실수형에는 부호가 있다.



**float & double**

![image-20220629094329570](Chapter2%20%EB%B3%80%EC%88%98(Variable).assets/image-20220629094329570.png)

:heavy_check_mark: 대부분의 경우 저장 가능한 값의 범위에 float가 있지만 float와 double의 경우 오차가 존재하므로 정밀도가 중요한 경우 float가 아닌 double을 사용해야 하는 경우가 있다.

**double is default**



#### 형식화된 출력 - printf()

**println()의 단점 - 출력형식 지정 불가**

1. 실수의 자리수 조절불가 - 소수점 n자리만 출력하려면?

   ```java
   System.out.println(10/3);	// 3
   System.out.println(10.0/3);	// 3.33333333333.......
   ```

2. 10진수로만 출력된다. - 8진수, 16진수로 출력하려면?

   ```java
   System.out.println(0x1A); // 26
   ```

**printf()로 출력형식 지정가능**

System.out.printf(지시자,)

```java
System.out.printf("%.2f", 10.0/3);`// 3.33
System.out.printf("%d", 0x1A);	// 26
System.out.printf("%x", 0x1);	// 1A
```



#### printf()의 지시자

JavaAPI - Formatter

![image-20220701203917664](Chapter2%20%EB%B3%80%EC%88%98(Variable).assets/image-20220701203917664.png)

* %b, %d, %o, %x, %X : 정수
* %f, %e, %E: 실수
* %c, %s: 문자

여러개의 지시자를 사용하는 것도 가능하다.

```java
System.out.printf("age:%d year:%d\n", 14, 2017);
```

* \n, %n: 개행문자(줄바꿈)

OS에 따라 개행문자가 다를 수 있다. %는 OS에 관계없이 사용가능하다.



1. 정수를 10진수, 8진수, 16진수로 출력

   ```java
   System.out.printf("%d", 15);	// 15 10진수 decimal
   System.out.printf("%o", 15);	// 17 8진수 octal
   System.out.printf("%x", 15);	// f 16진수 hexa
   System.out.printf("%s", Integer.toBinaryString(15));	
   // 정수를 이진문자열로 변경
   // 문자열 1111을 출력
   ```

2. 8진수와 16진수에 접두사 붙이기

   ```java
   System.out.printf("%#o", 15);	// 017
   System.out.printf("%#x", 15);	// 0xf
   System.out.printf("%#X", 15);	// 0XF
   ```

3. 실수 출력을 위한 지시자 %f - 지수형식(%e), 간략한 형식(%g)

   정밀도가 높기를 바란다면 double

   ```java
   float f = 123.4567890f;
   System.out.printf("%f", f);	// 123.456787 정밀도로 9가 아닌 7
   System.out.printf("%e", f);	// 1.234568e+02 반올림되어 보여짐
   							// 값이 변하는 것은 아니다.
   ```

[]안의 숫자는 자리수

```java
System.out.printf("[%5d]%n", 10);	// [   10] 오른쪽정렬
System.out.printf("[%-5d]%n", 10);	// [10   ] 왼쪽정렬
System.out.printf("[%05d]%n", 10);	// [00010] 빈값을 0으로 채운다

System.out.printf("d=%14.19f%n", d)	// 전체 14자리 중 소수점 아래 10자리
System.out.printf("[%ed]%n", 1234567)	// 1234567
```

```java
System.out.printf("[%s]%n", 	url);	// [www.naver.com]
System.out.printf("[%20d]%n", 	url);	// [   www.naver.com]
System.out.printf("[%-20d]%n", 	url);	// [www.naver.com   ]
System.out.printf("[%.8s]%n",	url);	// [www.nave]
```



#### 화면에서 입력 받기 - Scanner

**Scanner란?**

화면으로부터 데이터를 입력받는 기능을 제공하는 클래스

**Scanner를 사용하려면**

1. import 추가

   ```java
   import java.util.*;
   ```

2. Scanner객체의 생성

   ```java
   Scanner scanner = new Scanner Scanner(System.in);
   // System.in 화면으로부터 입력
   ```

3. Scanner 객체를 사용

   ```java
   int num = scanner.nextInt();	// 화면에서 입력받은 정수를 num에 저장
   String input = scanner.nextLine();	// 화면에서 입력받은 내용을 input에 저장
   int num = Integer.parseInt(input);	// 문자열(input)을 숫자(num)으로 변환
   ```

   숫자 -> 문자열: 숫자 + ""

   문자열 -> 숫자: Integer.parseInf()

```java
import java.util.*;
public class Hello {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner scanner = new Scanner(System.in);
		
		int num = scanner.nextInt();
		int num2 = scanner.nextInt();
		System.out.println(num);
		System.out.println(num2);
	}
}
```

**입력**

100 200

**출력**

100

200



#### 정수형의 오버플로우

오버플로우: 표현가능한 범위를 넘는 것

최대값 + 1 -> 최소값

최소값 - 1 -> 최대값

**10진수**

9999(최대값) + 1 -> 0000(최소값)

0000(최소값) - 1 -> 9999(최대값)

**2진수**

1111 + 1 -> 0000

0000 - 1 -> 1111

**부호없는 정수(4bit)**:heavy_check_mark: short

15(최대값) + 1 -> 0(최소값)

0(최소값) - 1 -> 15(최대값)

**부호있는 정수(4bit)**:heavy_check_mark:char

7(최대값) + 1 -> -8(최소값)

-8(최소값) - 1 -> 7(최대값)



**16bit로 표현할 수 있는 정수의 개수**: 2^16개 (65536개)

**short타입의 표현범위**: -2^15 ~ 2^15-1 (-32768~32767)

**char타입의 표현범위**: 0~2^16-1 (0~65535)



#### 타입간의 변환방법:star:

**문자와 숫자간의 변환**

숫자 -> 문자: 3 + '0' -> '3'

문자 -> 숫자: '3' - '0' -> 3

**문자열로의 변환**

숫자 -> 문자열: 3 + "" -> "3"

문자 -> 문자열: '3' + "" -> "3"

**문자열을 숫자로 변환**

문자열 -> 숫자: 

"3" -> Integer.parseInt("3") -> 3

"3.4" -> Double.parseDouble("3.4") -> 3.4

**문자열을 문자로 변환**

문자열 -> 문자

"3" -> "3".charAt(0)  -> '3'
