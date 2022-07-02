### 조건문과 반복문

제어문(flow control statement)

조건문: 조건을 만족할 때만 {}을 수행(0~1번)

반복문: 조건을 만족하는 동안 {}을 수행(0~n번)



#### if문

조건식이 참(true)일 때, 괄호 {}안의 문장들을 수행한다.

```java
if (조건식){
    // 조건식이 참(true)일 때 수행될 문장들을 적는다.
}
```



다양한 예시

![image-20220702015559004](Chapter4%20%EC%A1%B0%EA%B1%B4%EB%AC%B8%EA%B3%BC%20%EB%B0%98%EB%B3%B5%EB%AC%B8.assets/image-20220702015559004.png)

:heavy_check_mark: String에 대한 예시 확인



#### 블럭 {}

여러 문장을 하나로 묶어주는 것

{: 블럭의 시작

}: 블럭의 끝



#### if-else 문

둘 중 하나 - 조건식이 참일 떄와 거짓일 때로 나눠서 처리

```java
if (조건식) {
    // 조건식이 참(true)일 때 수행될 문장들을 적는다.
} else {
    // 조건식이 거짓(falst)일 때 수행될 문장들을 적는다.
}
```



#### if-else if문

여러개 중의 하나 - 여러 개의 조건식을 포함한 조건식

```java
if (조건식 1){
    // 조건식1의 연산결과가 참일 때 수행될 문장들을 적는다.
} else if (조건식 2){
    // 조건식2의 연산결과가 참일 때 수행될 문장들을 적는다.
} else if (조건식 3){	// 여러 개의 else if를 사용할 수 있다.
    // 조건식3의 연산결과가 참일 때 수행될 문장들을 적는다.
} else {	// 마지막은 보통 else블럭으로 끝나며, else블럭은 생략가능
    // 위의 어느 조건식도 만족하지 않을 때 수행될 문장들을 적는다.
}
```



#### 중첩 if문 - if문 안의 if

괄호를 잘 생각하여 사용해야한다.

```java
if (조건식1){
    // 조건식1의 연산결과가 true일 때 수행될 문장들을 적는다.
    if (조건식2){
        // 조건식1과 조건식2가 모두 true일 때 수행되는 문장들
    } else {
        // 조건식1이 false일 때 수행되는 문장들
    }
} else {
    // 조건식1이 false일 때 수행되는 문장들
}
```



#### switch문

처리해야하는 경우의 수가 많을 때 유용한 조건문

**제약조건이 존재한다.**

switch문은 언제나 if문으로 바꿀 수 있지만 if문은 언제나 switch문으로 바꿀 수 있다고 말할 수 없다.

1. 조건식을 계산한다.
2. 조건식의 결과와 일치하는 case문으로 이동한다.
3. 이후의 문장들을 수행한다.
4. break문이나 switch문의 끝을 만나면 switch문 전체를 빠져나간다.

```java
switch (조건식){
    case 값1 :
        // 조건식의 결과가 값1와 같을 경우 수행될 문장들
        // ...
        break;	// switch문을 벗어난다.
    case 값2 :
        // 조건식의 결과가 값2와 같은 경우 수행될 문장들
        // ...
        break;
    default :
        // 조건식의 결과와 일치하는 case문이 없을 때 수행될 문장들
        // ...
}
```



#### switch문의 제약 조건

switch문의 조건식 결과는 정수 또는 문자열이어야한다.

case문의 값은 정수 상수(문자 포함), 문자열만 가능하며, 중복되지 않아야한다.

(변수 불가능하다.)



#### 임의의 정수 만들기

**Math.random()**: 0.0과 1.0사이의 임의의 double값을 반환

(0.0 <= Math.random() < 1.0)

원하는 수를 만들기 위해 예시 1~3

1. 각 변에 3을 곱한다.

   ```
   0.0 <= Math.random() * 3 < 3.0
   ```

2. 각 변을 int형으로 변환한다.

   ```
   (int)0.0 <= (int)(Math.random()) * 3 < (int)3.0
   0 <= (int)(Math.random() * 3) < 3
   ```

3. 각 변에 1을 더한다.

   ```
   0 + 1 <= (int)(Math.random()*3) + 1 < 3 + 1
   1 <= (int)(Math.random()*3) + 1 < 4
   ```



#### for문

조건을 만족하는 동안 블럭{}을 반복 - 반복횟수를 알 때 적합

:heavy_check_mark:for문의 경우 조건식의 확인이 필요하다. (무한반복)

for문 안에 선언된 변수(i)는 for문 안에서만 사용될 수 있다.

```java
for (int i=1; i<=5; i++){
    System.out.println("Yes")
}
for (int i=1; i<=10; i=i+1){
    System.out.println("Hello");
}
for (초기화;조건식;증감식){
    // 참일경우 수행될 문장
}
```

```java
int i;
for (i=1; i <= 10; i++){
    System.out.println("i="+i);
}
```



#### 중첩 for문

for문 내에 또 다른 for문을 포함시킬 수 있다.

```java
for (int i=2; i<=9; i++){
    for (int j=1; j<=9; j++){
        System.out.println(i+"*"+j+"="+(i*j));
    }
}
```

```java
for (int i=1; i<=10; i++){
    for (int j=1; j<=i; j++){
        System.out.print("*")
    }
    System.out.println()
}
```



#### while문

조건을 만족시키는 동안 블럭{}을 반복 - 반복횟수 모를 때

while문과 for문은 서로 변경이 가능하다.

while (true)의 true는 생략불가능

```java
while (조건식){
    // 조건식의 연산결과가 참(true)인 동안, 반복될 문장들을 적는다.
}
```

```java
int i = 5;
while(i!=0){
    i--;
    System.out.println(i + "Check")
}
```

```java
int num = 0, sum = 0;
System.out.println("숫자를 입력하세요");

Scanner scanner = new Scanner(System.in);
String tmp = scanner.nextLine();
num = Integer.parseInt(tmp);

while (num!=0){
    sum += num % 10;
    System.out.printf("sum-%3d num=%d%n", sum, num);
    
    num /= 10;
}
System.out.printf("각 자리수의 합:" + sum)
```



#### do-while문

블럭{}을 최소한 한 번 이상 반복 - 사용자 입력받을 때 유용

```java
do {
    // 조건식의 연산결과가 참일 때 수행될 문장들을 적는다.
    // (처음 한번은 무조건 실행)
} while (조건식);
```



#### break문

자신이 포함된 하나의 반복문을 벗어난다.



#### continue문

자신이 포함된 반복문의 끝으로 이동 - 다음 반복으로 넘어간다.



#### 이름붙은 반복문

반복문에 이름을 붙여서 하나 이상의 반복문을 벗어날 수 있다.

```java
class Ex4_19 {
    public static void main(String[] args){
        Loop1: for (int i=2; i <= 9; i++){
            if(j==5)
                break Loop1;
//            	break;
//            	continue Loop1;
//            	continue;
            System.out.println(i+"*"+j+"="+i*j);
        }
        System.out.print();
    }
}
```

