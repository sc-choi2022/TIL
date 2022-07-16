### 배열
같은 타입의 여러 변수를 하나의 묶음으로 다루는 것

```java
int score1, score2, score3, score4, score5;

int[] score = new int[5];
```
✔참조변수, 인덱스

✔연속적

#### 배열의 선언과 생성
배열의 선언: 배열을 다루기 위한 참조변수의 선언
![[Pasted image 20220716210721.png]]

✔[]: 배열 기호

```
타입[] 변수이름;          // 배열을 선언(배열을 다루기 위한 참조변수 선언)
변수이름 = new 타입[길이]; // 배열을 생성(실제 저장공간을 생성)
```

#### 배열의 인덱스
각 요소(저장공간)에 자동으로 붙은 (일련)번호
**인덱스(index)의 범위는 0부터 '배열길이-1'까지**
저장 공간 하나를 "배열의 요소(element)"라고 한다.

```java
class Ex5_1_tmp {
	public static void main(String[] args){
		int[] score;        // 1. 배열 score을 선언(참조 변수)
		score = new int[5]; // 2. 배열의 생성(int저장공간 x 5)

		int[] score = new int[5]; // 배열의 선언과 생성울 동시에
	}
}
```

#### 배열의 길이
배열이름.length - 배열의 길이(int형 **상수**)
**배열은 한번 생성하면 실행 동안 그 길이를 바꿀 수 없다.**
```java
int[] arr = new int[5]; // 길이가 5인 int 배열
int tmp = arr.length;   // arr.length의 값은 5이고 tmp에 5가 저장된다.
```

```java
int[] score = new int[6];
for (int i=0; i < 6; i++)
	System.out.println(score[i]);
```
```java
int[] score = new int[5];
for (int i=0; i < score.length; i++)
	System.out.println(score[i]);
```
✔배열에서 가장 많은 에러: index 범위를 벗어나는 에러

#### 배열의 초기화
배열의 각 요소에 처음으로 값을 저장하는 것
배열은 기본적으로 자동 초기화가 된다.
int: 0

초기화 방법 두가지
2번째 방법을 더 많이 사용
```java
int[] score = new int[]{ 50, 60, 70, 80, 90};
int[] score = { 50, 60, 70, 80, 90};
```

```java
int[] score;
score = { 50, 60, 70, 80, 90}; // error int[]을 생략할 수 없다.
```

#### 배열의 출력
```java
int[] iArr = { 100, 95, 80, 70, 60 };
System.out.println(iArr); // [I@14318bb와 같은 형식의 문자열이 출력된다.
System.out.println(Arrays.toString(iArr)); // [ 100, 95, 80, 70, 60] 출력
```

예외적으로
```java
int[] chArr = { 'a', 'b', 'c', 'd' };
System.out.println(chArr); // abcd 출력
```

✔ctrl+shift+o: 필요한 import문 자동으로 추가

#### 배열의 활용
for문 
* 총합과 평균
* 최대값과 최소값
* Math.random()을 활용하여 배열을 섞는다.

#### String배열의 선언과 생성
```java
String[] name = new String[3]; // 3개의 문자열을 담을 수 있는 배열을 생성
```
![[Pasted image 20220716220723.png]]

```java
String[] name = { "Kim", "Park", "Lee"};
```

#### String 클래스
1. String클래스는 char[]와 메서드(기능)을 결합한 것

**String클래스 = char[] + 메서드(기능)**
✔문자배열을 쓰는 것보다 String클래스를 쓰는 것이 편리하다.

2. String클래스는 내요을 변경할 수 없다. (read only)

#### String클래스의 주요 메서드
![[Pasted image 20220716221324.png]]

```java
String str = "012345";
String tmp = str.substring(1,4);
System.out.println(tmp);         // "123" 출력
System.out.println(1);           // "1234" 출력
```

#### 커맨드 라인을 통해 입력받기
커맨드 라인에 입력한 값이 문자열 배열에 담겨서 전달된다.
✔elicpes에서는 Run Configurations > Arguments
✔cmd > alt+Enter을 통해 bin의 class파일 경로로 이동 > java Ex5_7 abc 123 "Hello world" 입력
args에 입력한 값이 들어가서 실행된다.

#### 2차원 배열
테이블 형태의 데이터를 저장하기 위한 배열
```java
int[][] score = new int[4][3]; // 4행 3열의 2차원 배열을 생성
```

#### 2차원 배열의 인덱스

![[Pasted image 20220716222950.png]]

```java
int[][] arr = { {1, 2, 3}, {4, 5, 6} }; // new int[][]가 생략된다.
int[][] arr = { 
				{1, 2, 3}, 
				{4, 5, 6} 
				};
```

#### 2차원 배열 예제
* 2중 for문
* 여러 과목의 합계, 평균
* 문제, 답을 담은 2차원 배열

#### Arrays로 배열 다루기
**문자열의 비교와 출력 - equals(), toString()**
```java
int[] arr = {0, 1, 2, 3, 4};
int[][] arr2D = {{11,12}, {21,22}};

System,out.println(Arrays.toString(arr)); // [0, 1, 2, 3, 4]
// deepToString()은 2차원이상 다차원 배열일 때 사용
System,out.println(Arrays.deepToString(arr2D)); // [[11, 12],[21,22]]
```

```java
String[][] str2D = new String[][]{{"aaa","bbb"},{"AAA","BBB"}};
String[][] str2D2 = new String[][]{{"aaa","bbb"},{"AAA","BBB"}};

System.out.println(Arrays.equals(str2D, str2D2); // false
// 다차원 배열은 deep을 붙여준다
System.out.println(Arrays.deepEquals(str2D, str2D2); // true
```

**배열의 복사 - copyOf(), copyOfRange()**
```java
int[] arr = {0, 1, 2, 3, 4};
int[] arr2 = Arrays.copyOf(arr, arr.length); // arr2 = [0, 1, 2, 3, 4]
int[] arr3 = Arrays.copyOf(arr, 3); // arr3 = [0, 1, 2]
int[] arr4 = Arrays.copyOf(arr, 7); // arr4 = [0, 1, 2, 3, 4, 0, 0]
int[] arr5 = Arrays.copyOfRange(arr, 2, 4); // arr5 = [2,3] <- 4는 불포함
```

**배열의 정렬 - sort()**
```java
int[] arr = { 3, 2, 0, 1, 4};
Arrays.sort(arr);
System.out.println(Arrays.toString(arr)); // [0, 1, 2, 3, 4]
```