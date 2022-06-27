## 자바를 시작하기 전에

### 자바(Java Programming Language)

프로그래밍 언어(programing language)

컴퓨터 프로그램(애플리케이션)을 만드는 데 사용

실행환경(JRE) + 개발도구(JDK) + 라이브러리(API)



* PC 애플리케이션
* 웹 애플리케이션
* 모바일 애플리케이션(안드로이드)
* 빅 데이터(Big Data) - hadoop



다양한 분야에서 활발히 사용

20년 동안 프로그래밍 언어 1,2위

C++보다 배우기 쉽고 풍부한 학습자료

모던 프로그래밍 언어(객체지향+함수형)

실무에서 가장 많이 사용

**JDK: 자바 개발도구**

**Java2: J2SE, J2ME, J2EE**

**J2SE 5.0**

**Java SE 8** - 이 버전으로 공부한다.

이후 6개월 마다 버전 발표



### 자바의 특징

배우기 쉬운 객체지향 언어 = 프로그래밍언어에 객체지향을 도입

자동 메모리 관리(가비지 컬렉터 GC)

멀티 쓰레드를 지원(하나의 프로그램에서 동시에 여러 개의 작업이 가능)

풍부한 라이브러리로 쉽게 개발 가능

운영체제에 독립적



### 자바 가상 머신(JVM: Java Virtual Machine)

자바 프로그램이 실행되는 가상 컴퓨터(VM)

한 번 작성하면, 어디서든 실행(Write once, run anywhere)



Java 애플리케이션 ↔JVM↔OS(Windows)↔컴퓨터(하드웨어)

일반 애플리케이션↔OS(Windows)↔컴퓨터(하드웨어)

OS위에서 실행되는 일반 애플리케이션 따라서 windows용 애플리케이션은 macintosh와 같은 다른 OS에서는 사용할 수 없다.

Java는 운영체제별로 JVM이 만들어져있기 때문에 Java 애플리케이션을 개발하면 JVM이 설치되어있으면 운영체제에 관계없이 수정하지 않고 사용할 수 있다.



**설치 시 확인할 링크**

github.com/castello/javajungsuk_basic

:heavy_check_mark: 현재는 이전에 설치한 eclipse를 사용



### Java API 문서의 설치

**Java API란?**

Java로 프로그램을 만드는데 필요한 주요기능을 미리 만들어서 제공

**Java API문서란?**

Java API가 제공하는 기능에 대한 상세한 정보 제공(html 파링)

**Java API 문서의 설치**

www.oracle.com에서 압축파일을 다운받아서 압축해제



### 자바프로그램 작성

:heavy_check_mark: Java에서는 대소문자를 구분

```java
class Hello {
        public static void main(String[] args) {
                System.out.println("Hello, world."); // 화면에 글자를 출력한다.
        }
}
```

**cmd**

```
javac Hello.java
```

javac은(는) 내부 또는 외부 명령, 실행할 수 잇ㄴ느 프로그램. 또는 배치 파일이 아닙니다.

:heavy_check_mark:javac의 위치를 알지 못하기 때문이다.

bin폴더 안에 java.exe가존재한다.

환경변수에 javac를 등록한다.

다시 cmd에서 `javac Hello.java`를 하면 컴파일되어 Hello.class가 생성된다.

:heavy_check_mark:컴파일 오류가 생기는 단계

:x:한글을 인식하지 못하는 오류가 있다 확인필요



1. javac.exe: 

   자바 컴파일러. 사람이 작성한 문장을 기계어로 번역

   소스 파일(\*.java)을 클래스 파일(\*.class)로 변환

이 class파일을 실행하기 위해 java.exe파일이 필요하다.

2. java.exe:

   자바 인터프리터

   자바 프로그램 (클래스파일)을 실행
   
3. 클래스 

   자바 프로그램의 단위

   자바 프로그램은 클래스들로 구성

   ```java
   class Name {// 클래스의 시작
   	/* 모든 문장은 클래스 {} 안에 있어야 한다. */
   }// 클래스의 끝
   ```

4. main메서드 

   자바 프로그램의 시작점. 이 메서드 없이 실행 불가

   ```java
   class Name {
       public static void main(String[] args){// main 메서드의 시작
           /* 실행할 문장을 넣는다(첫 문장부터 순서대로 실행된다.)*/
       }// main 메서드의 끝
   }
   ```



### 이클립스 설치 & 개발

![image-20220627003827783](Chapter1%20%EC%9E%90%EB%B0%94%EB%A5%BC_%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0_%EC%A0%84%EC%97%90.assets/image-20220627003827783.png)

![image-20220627003858781](Chapter1%20%EC%9E%90%EB%B0%94%EB%A5%BC_%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0_%EC%A0%84%EC%97%90.assets/image-20220627003858781.png)

:heavy_check_mark: 여러 perspective가 존재한다.



eclipse는 프로그램을 프로젝트 단위로 작성한다.

![image-20220627004323102](Chapter1%20%EC%9E%90%EB%B0%94%EB%A5%BC_%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0_%EC%A0%84%EC%97%90.assets/image-20220627004323102.png)



**New > Class**

![image-20220627004455747](Chapter1%20%EC%9E%90%EB%B0%94%EB%A5%BC_%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0_%EC%A0%84%EC%97%90.assets/image-20220627004455747.png)

![image-20220627004641925](Chapter1%20%EC%9E%90%EB%B0%94%EB%A5%BC_%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0_%EC%A0%84%EC%97%90.assets/image-20220627004641925.png)

:triangular_flag_on_post: eclipse는 저장과 함께 컴파일을 해준다. 따라서 따로 컴파일이 필요하지 않다.

실행하면 Console 창에 Hello, world가 출력된다.

**Project > Build Automatical이 체크되어 있기 때문**



Package Explorer view는 소스파일 중심으로 보여준다.

Navigator를 통해 모든 파일을 보여준다.

bin 폴더에는 class파일이 있다.

eclipse는 소스파일과 class파일을 별도에 폴더에서 관리한다.

.파일은 eclipse에서 만든 것이므로 수정하지 않는다.



### 이클립스에서 자바 프로그램을 작성하는 순서

1 프로젝트를 생성한다.

* 메뉴 File > New > Java Project

2 클래스를 생성한다.

* 프로젝트 이름 위에서 우클릭 > New > Class

3 소스파일의 작성 후 저장(자동 컴파일 된다.)

4 실행

* 메뉴 Run > Run



### Build 관련 메뉴 설명

Bulid란?

* 소스 파일 (*.java)로부터 프로그램을 만들어내는 전 과정

Project > Build All

* workspace의 모든 프로젝트를 빌드

Project > Build Project

* 현재 프로젝트를 빌드(변경된 소스 파일만 새로 컴파일)

Project > Clean

* 이전 빌드의 정보를 모두 삭제 (모든 소스 파일을 새로 컴파일)

Project > Build Automatically

* 소스 파일을 변경 후, 저장할 때마다 자동 컴파일



### 이클립스 단축키

**ctrl + shift + l**: 단축키 전체 목록

**ctrl + +, -**: 폰트 크기 조절

**ctrl + D**: 한 줄 삭제

**ctrl+alt+down**: 행단위 복사(충돌 가능성 있다.)

:heavy_check_mark: windows 단축키와 충돌 시 window > Preferences > General > Keys > copy line

**ctrl+shift+A**: 멀티컬럼 편집

**alt+up, down**: 행단위 이동

**ctrl+i**: 자동 들여쓰기

**ctrl+/**: 주석(토글)

**/\**/**: 여러 줄 주석

**ctrl+space**: 자동완성



### 책의 소스와 강의자료 다운로드

https://github.com/castello/javajungsuk_basic



#### Import 방법

Package Explorer > 빈 화면에서 우클릭 > Import > General > Existing Projects into Workspace(기존의 프로젝트를 workspace로 가져오기) > javajungsuk_basic_src 폴더 선택 > Copy projects into workspace



#### Export 방법

Package Explorer > 빈 화면에서 우클릭 > Export > General > Archive File > 폴더 선택 > Save in zip format 체크 > 저장위치 선택 > Finish
