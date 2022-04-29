# JavaScript 01

## JavaScript Intro

JavaScript의 필요성

* 브라우저 화면을 '동적'으로 만들기 위함
* 브라우저를 조작할 수 있는 **유일한 언어**



## Browser

브라우저에서 할 수 있는 일

* DOM(Document Object Model) 조작
  * 문서(HTML) 조작
* BOM(Browser Object Model) 조작
  * navigator, screen, location, frames, history, XHR
* JavaScript Core (ECMAScript)
  * Data Structure(Object, Array), Conditional Expression, Iteration

### DOM

HTML, XML과 같은 문서를 다루기 위한 프로그래밍 인터페이스

문서를 구조화하고, 구조화된 구성 요소를 하나의 객체로 취급하여 다루는 논리적 트리 모델

문서가 객체(object)로 구조화되어 있으며 key로 접근 가능하다.

단순한 속성 접근, 메서드 활용뿐만 아니라 프로그래밍 언어적 특성을 활용한 조작이 가능하다.

**document: 문서를 상징하는 단어**

주요 객체

* window : DOM을 표현하는 창(브라우저 탭). 최상위 객체 (작성 시 생략 가능)
* document : 페이지 컨텐츠의 Entry Point 역할을 하며, \<head>, \<body> 등과 같은 수많은 다른 요소들을 포함한다.
* navigator, location, history, screen

#### 해석

파싱 (Parsing)

* 구문 분석, 해석
* 브라우저가 문자열을 해석하여 DOM Tree로 만드는 과정

cf) input.txt  ----- input().split(), map(int, input()) [parsing] ---> [1,2,3,4]


### BOM

Browser Object Model

자바스크립트가 브라우저와 소통하기 위한 모델

브라우저의 창이나 프레임을 추상화해서 프로그래밍적으로 제어할 수 있도록 제공하는 수단

* 버튼, URL 입력창, 타이틀 바 등 브라우저 윈도우 및 웹 페이지 일부분을 제어 가능하다.

window 객체는 모든 브라우저로부터 지원받으며 브라우저의 창(window)를 지칭한다.

**window: 브라우저 탭을 상징하는 단어**

```javascript
// 탭 창
window.open()
// 인쇄 창
window.print()
// 메시지 및 확인, 취소 버튼이 있는 대화상자 창
window.confirm('진짜 삭제하시겠습니까?')
// document도 브라우저 내에 종속되어 있기 때문에 window 전역 객체에 포함
window.document
```



### JavaScript Core

브라우저(BOM & DOM)을 조작하기 위한 명령어 약속(언어)

```javascript
const numbers = [1,2,3,4,5]
for (let i=0; i < numbers.length; i++){
    console.log(numbers[i])
}
```

출력 결과

```
1
2
3
4
5
```



**<u>브라우저(BOM)와 그 내부의 문서(DOM)를 조작하기 위해 ECMAScript(JS)를 학습한다.</u>**



## ECMAScript

1. Javascript와 ECMAScript와 같은 이야기를 하고 있는 것
2. ECMAScript에는 몇가지 버전이 있는 데 학습하는 부분은 ECMAScript6 이상

### ECMA(ECMA International)

정보 통신에 대한 **표준을 제정하는 비영리 표준화 기구**



ECMAScript는 ECMA에서 <u>ECMA-262</u> 규격에 따라 정의한 언어

* ECMA-262: 범용적인 목적의 프로그래밍 언어에 대한 명세

**ECMAScript6는 ECMA에서 제안하는 <u>6번째 표준 명세</u>**

* 참고) ECMAScript6의 발표 연도에 따라 ECMAScript2015이라고도 불린다.



## 세미콜론

자바스크립트는 **세미콜론을 선택적으로 사용 가능**

세미콜론이 없으면 **ASI**에 의해 자동으로 세미콜론이 삽입된다.

* ASI: 자동 세미콜론 삽입 규칙 (Automatic Semicolon Insertion)

본 수업에서는 <u>자바스크립트의 문법 및 개념적 측면에 집중하기 위해 세미콜론을 사용하지 않고 진행한다.</u>

**세미콜론을 선택적으로 사용 가능**

```javascript
// 세미콜론이 있는 경우
const greeting = 'Hello';
console.log(greeting)

// 세미콜론이 없는 경우
const greeting = 'Hello'
console.log(greeting)
```



## 코딩 스타일 가이드

코딩 스타일의 핵심은 **합의된 원칙과 일관성**

* 절대적인 하나의 정답은 없으며, 사오항에 맞게 원칙을 정하고 일관성 있게 사용하는 것이 중요하다.

코딩 스타일은 **코드의 품질에 직결되는 중요한 요소**

* 코드의 가독성, 유지보수 또는 팀원과의 커뮤니케이션 등 **개발 과정 전체에 영향을 끼침**

참고) 다양한 자바스크립트 코딩 스타일 가이드

* Airbnb Javascript Style Guide 
  * **수업은 Airbnb Style Guide 중심으로 진행**
  * 단, 가이드의 일부 항목은 <u>문법 및 개념적 측면에 집중하기 위해 변형해서 사용한다.</u>
* Google Javascript Style Guide
* standardjs



## 변수와 식별자

### 식별자

식별자 정의와 특징

* 식별자(identifier)는 변수를 구분할 수 있는 변수명을 말한다.
* 식별자는 반드시 문자, **달러($)** 또는 밑줄(_)로 시작한다.
* 대소문자를 구분하여, 클래스명 외에는 모두 소문자로 시작한다.
* 예약어* 사용 불가능
  * 예약어 예시: for, if, function 등

식별자 작성 스타일

* 카멜케이스(**camelCase**, lower-camel-case)

  두 번째 단어의 첫 글자부터 대문자(시작이 소문자)

  * <u>변수, 객체, 함수</u>에 사용

```javascript
// 변수
let dog
let variableName

// 객체
const userInfo = { name: 'Tom', age: 20 }

// 함수
function add() {}
function getName() {}
```



* 파스칼 케이스(PascalCase, upper-camel-case)

  모든 단어의 첫 번째 글자를 대문자로 작성

  * <u>클래스, 생성자</u>에 사용

```javascript
// 클래스
class User {
    constructor(options){
        this.name = options.name
    }
}

// 생성자 함수
function User(options){
    this.name = options.name
}
```



* 대문자 스테이크 케이스(SNAKE_CASE)

  모든 단어 대문자 작성 & 단어 사이에 언더스코어 삽입

  * <u>상수(constants)</u>에 사용
    * 상수 : 개발자의 의도와 상관없이 **변경될 가능성이 없는 값을 의미**

```javascript
// 값이 바뀌지 않을 상수
const API_KEY = 'my-key'
const PI = Math.PI

// 재할당이 일어나지 않는 변수
const numbers = [1, 2, 3]
```



### 변수 선언 키워드

#### let, const

| let                                    | const                                       |
| -------------------------------------- | ------------------------------------------- |
| **재할당 할 예정인 변수** 선언 시 사용 | **재할당 할 예정이 없는 변수** 선언 시 사용 |
| 변수 **재선언 불가능**                 | 변수 **재선언 불가능**                      |
| 블록 스코프                            | 블록 스코프                                 |

(참고) 선언, 할당, 초기화

**javascript는 선언과 할당을 분리할 수 있다.**

선언 (Declaration)

* 변수를 생성하는 행위 또는 시점
* 이름만 선점 가능

할당 (Assignment)

* 선언된 변수에 값을 저장하는 행위 또는 시점

초기화 (Initialization)

* 선언된 변수에 처음으로 값을 저장하는 행위 또는 시점

```javascript
let foo				// 선언
console.log(foo)	// undefined

foo = 11			// 할당
console.log(foo)	// 11

let bar = 0			// 선언 + 할당
console.log(bar)	// 0
```



#### 재할당 예시

**let (재할당 가능)**

```javascript
let number = 10		// 1. 선언 및 초기값 할당
number = 10			// 2. 재할당
console.log(number) // 10
```

**const (재할당 불가능)**

```javascript
const number = 10	// 1. 선언 및 초기값 할당
number = 10			// 2. 재할당 불가능

=> Uncaught TypeError : Assignment to constant variable.
```

값을 바꾸는 것을 못하는 것이 아니라 **재할당이 안되는 것!**

배열 추가는 가능하다.

**=를 사용하지 못한다.**



#### 재선언 예시

**let (재선언 불가능)**

```javascript
let number = 10 		// 1. 선언 및 초기값 할당
let number = 50			// 2. 재선언 불가능

=> Uncaught SyntaxError : Indentifier 'number' has already been declared.
```

**const (재선언 불가능)**

```javascript
const number = 10 		// 1. 선언 및 초기값 할당
const number = 50		// 2. 재선언 불가능

=> Uncaught SyntaxError : Indentifier 'number' has already been declared.
```



#### 블록 스코프(block scope)

if, for, 함수의 **중괄호 내부**를 가리킨다.

블록 스코프를 가지는 변수는 **블록 바깥에서 접근 불가능**

cf) Python은 함수스코프

```javascript
let x = 1
if (x===1){
    let x = 2
    console.log(x)		// 2
}
console.log(x)			// 1
```



#### var

**var로 선언한 변수는 재선언 및 재할당 모두 가능하다.**

**ES6 이전**에 변수를 선언할 때 사용되던 키워드

**호이스팅되는 특성**으로 인해 예기치 못한 문제 발생 가능하다.

* **ES6** 이후부터는 var 대신 **const와 let**을 사용하는 것을 권장한다.

함수 스코프



```javascript
var number = 10			// 1. 선언 및 초기값 할당
var number = 50 		// 2. 재선언 및 재할당
console.log(number)		// 50
```



##### 함수 스코프(function scope)

**함수의 중괄호 내부**를 가리킨다.

함수 스크포를 가지는 변수는 **함수 바깥에서 접근이 불가능하다.**

```javascript
function foo(){
    var x = 5
    console.log(x)	// 5
}
console.log(x)
// ReferenceError: x is not defined
```



##### 호이스팅(hoistinig)

변수를 **선언 이전에 참조할 수 있는 현상**

**변수 선언 이전의 위치에서 접근 시 undefined를 반환한다**

```javascript
console.log(username)
// undefined
var username = '홍길동'

console.log(email)
// Uncaught ReferenceError
let email = 'abc@gmailc.om'

console.log(age)
// Uncaught ReferenceError
const age = 50
```



#### let, const, var 비교

| /      | let          | const        | var         |
| ------ | ------------ | ------------ | ----------- |
| 재선언 | x            | x            | O           |
| 재할당 | O            | x            | O           |
| 스코프 | 블록 스코프  | 블록 스코프  | 함수 스코프 |
| 비고   | ES6부터 도입 | ES6부터 도입 | 사용 X      |



## 데이터 타입

데이터 타입 종류

자바스크립트의 모든 값은 **특정한 데이터 타입을 가진다.**

**원시 타입(Primitive type)** **참조 타입(Reference type)**

Data Type

* Primitive type
  * Number
  * String
  * Boolean
  *  
    * undefined
    * null
    * Symbol
* Reference type
  * Objects
    * Array
    * Function
    * ... etc.

### 원시 타입과 참조 타입 비교

**원시 타입(Primitive type)**

* **객체 (object)가 아닌 **기본 타입
* 변수에 **해당 타입의 값이 담긴다.**
* 다른 변수에 복사할 때 **실제 값이 복사된다.**

```javascript
let message = '안녕하세요'		// 1. message 선언 및 할당
let greeting = message		// 2. greeting에 message 복사
console.log(greeting)		// 3. '안녕하세요' 출력

message = 'Hello!'			// 4. message 재할당
console.log(greeting)		// 5. '안녕하세요' 출력
//=> 즉, 원시 타입은 실제 해당 타입의 값을 변수에 저장한다.
```



**참조 타입(Reference type)**

* **객체(object) 타입**의 자료형
* 변수에 해당 **객체의 참조 값이 담긴다.**
* 다른 변수에 복사할 때 **참조 값이 복사된다.**

```javascript
const message = ['안녕하세요']	 // 1. message 선언 및 할당
const greeting = message		// 2. greeting에 message 복사
console.log(greeting)			// 3. ['안녕하세요'] 출력

message[0] = 'Hello!'			// 4. message 재할당
console.log(greeting)			// 5. 'Hello!' 출력
//=> 즉, 참조 타입은 해당 객체를 참조할 수 있는 참조 값을 저장한다.
```



### 원시타입 (Primitive type)

#### 숫자 (Number) 타입

**정수, 실수 구분 없는 하나의 숫자 타입**

**부동소수점 형식**을 따름

(참고) NaN (Not-A-Number)

* **계산 불가능한 경우**반환되는 값
  * 'Angel'/1004 => NaN

```javascript
const a = 13		// 양의 정수
const b = -5		// 음의 정수
const c = 3.14		// 실수
const d = 2.998e8	// 거듭 제곱
const e = Infinity	// 양의 무한대
const f = -Infinity	// 음의 무한대
const g = NaN		// 산술 연산 불가
```

```javascript
1/0					// Infinity
-1/0				// -Infinity
NaN					// NaN
'abc'/ 100			// NaN
```



#### 문자열 (String) 타입

**텍스트 데이터**를 나타내는 타입

16비트 유니코드 문자의 집합

**작은따옴표** 또는 큰 따옴표 모두 가능하다.

**템플릿 리터럴 (Template literal)**'

cf) f-string과 유사하다.

* **ES6부터 지원**
* **따옴표 대신 backtick(``)**으로 표현한다.
* **${ expression }**형태로 표현식 삽입 가능하다.

```javascript
const firstName = 'Brandan'
const lastName = 'Eich'
const fullName = `${firstName} ${lastName}`

console.log(fullName)	// Brandan Eich

const a = 'hello'
`${a} world`			// 'hello world'
```



#### undefined

변수의 **값이 없음**을 나타내는 데이터 타입

변수 선언 이후 **직접 값을 할당하지 않으면, 자동으로 undefined가 할당된다.**

cf) 직접 `=undefined`을 쓰는 경우는 없다. 개발자의 의도가 없다.

```javascript
let firstName
console.log(firstName)	// undefined
```



#### null

변수의 **값이 없음을 의도적으로 표현**할 때 사용하는 데이터 타입

cf) null은 자동생성 되지 않는다. 개발자가 의도적으로 사용한다.

(참고) null 타입과 **typeof 연산자**

* **typeof 연산자: 자료형 평가를 위한 연산자**
* **null 타입은 ECMA 명세의 원시 타입의 정의**에 따라 원시 타입에 속하지만, **typeof 연산자의 결과는 객체(object)로 표현된다.**

```javascript
let firstName = null
console.log(firstName)	// null

typeof null		 		// object
```

##### undefined 타입과 null 타입 비교

**undefined**

* **빈 값을 표현**하기 위한 데이터 타입
* **변수 선언 시 아무 값도 할당하지 않으면, 자바스크립트가 자동으로 할당**
* typeof 연산의 결과는 undefined

```javascript
typeof undefined	// undefined
```



**null**

* **빈 값을 표현**하기 위한 데이터 타입
* **개발자가 의도적으로 필요한 경우 할당**
* typeof 연산의 결과는 object

```javascript
typeof null			// object
```



#### Boolean 타입

* **논리적 참 또는 거짓**을 나타내는 타입
* **true** 또는 **false**로 표현한다.
* **조건문 또는 반복문**에서 유용하게 사용한다.
  * 참고) 조건문 또는 반복문에서 **boolean이 아닌 데이터 타입**은 자동 형변환 규칙에 따라 true 또는 false로 변환된다.

**ToBoolean Conversions (자동 형변환) 정리**

if에 들어갔을 때,

| 데이터 타입 | 거짓       | 참               |
| ----------- | ---------- | ---------------- |
| Undefined   | 항상 거짓  | X                |
| Null        | 항상 거짓  | X                |
| Number      | 0, -0, NaN | 나머지 모든 경우 |
| String      | 빈 문자열  | 나머지 모든 경우 |
| Object      | X          | 항상 참          |

**Object**

Python에서는 `if []:`는 False였지만 JavaScript에서는 `if([])`는 true이다.



### 참조 타입 (Reference type)

### 연산자

#### 할당 연산자

오른쪽에 있는 피연산자의 평가 결과를 왼쪽 피연산자에게 할당하는 연산자

다양한 연산에 대한 단축 연산자를 지원

(참고) Increment 및 Decrement 연산자

* Increment(++):  피연산자의 값을 1 증가시키는 연산자
* Decrement(--): 피연산자의 값을 1 감소시키는 연산자
* Airbnb Style Guide에서는 '+=' 또는 '-='와 같이 더 분명한 표현으로 적을 것을 권장

```javascript
let x = 0

x += 10
console.log(x)			// 10

x -= 3
console.log(x)			// 7

x *= 10
console.log(x)			// 70

x /= 10
console.log(x)			// 7

x++						// += 연산자과 동일
console.log(x)			// 8

x--						// -= 연산자와 동일
console.log(x)			// 7
```



#### 비교 연산자

피연산자들(숫자, 문자, Boolean 등)을 비교하고 결과값을 boolean으로 반환하는 연산자

문자열은 유니코드 값을 사용하며 표준 사전 순서를 기반으로 비교

* 예) 알파벳끼리 비교할 경우
  * 알파벳 순서상 후순위가 더 크다.
  * 소자가 대문자보다 더 크다.

```javascript
const numOne = 1
const numTwo = 100
console.log(numOne < numTwo)	// true

const charOne = 'a'
const charTwo = 'z'
console.log(charOne > charTwo)	// false
```



#### 동등 비교 연산자 (==)

두 피연산자가 **같은 값으로 평가**되는지 비교 후 boolean 값을 반환

비교할 때 <u>암묵적 타입 변환</u>을 통해 타입을 일치시킨 후 같은 값인지 비교한다.

**두 피연산자가 모두 객체일 경우 메모리의 같은 객체를 바라보는지 판별한다.**

**예상치 못한 결과가 발생할 수 있으므로 <u>특별한 경우</u>를 제외하고 사용하지 않는다.**

```javascript
const a = 1004
const b ='1004'
console.log(a == b)			// true

const c = 1
const d = true
console.loge(c == d)		// true

// 자동 타입 변화 예시
console.log(a + b)			// 10041004
console.log(c + d)			// 2
```

```javascript
0 == '0'		// true
0 == []			// true
'0' == []		// false
```



#### 일치 비교 연산자(===)

두 피연사자가 같은 값으로 평가되는지 비교 후 boolean 값을 반환

**엄격한 비교**가 이뤄지며 암묵적 타입 변환이 발생하지 않는다.

* **엄격한 비교**: 두 비교 대상의 **타입과 값 모두** 같은지 비교하는 방식

**두 피연산자가 모두 객체일 경우 메모리의 같은 객체를 바라보는지 판별한다.**

```javascript
const a = 1004
const b ='1004'
console.log(a === b)			// false

const c = 1
const d = true
console.loge(c === d)			// false
```



#### 논리 연산자

세 가지 논리 연산자로 구성

* and 연산은 **'&&'** 연산자를 이용
* or 연산은 **'||'** 연산자를 이용
* not 연산은 **'!'** 연산자를 이용

단축 평가 지원

예)

* false && true => false

* true || false => true

```javascript
console.log(true && false)		// false
console.log(true && true)		// true
console.log(1 && 0)				// 0
console.log(4 && 7)				// 7
console.log('' && 5)			// ''

console.log(true || false)		// true
console.log(false || false)		// false
console.log(1 || 0)				// 1
console.log(4 || 7)				// 4
console.log('' || 5)			// 5

console.log(!true)				// false
console.log(!'Bonjour!')		// false
```

```javascript
!true		// false
!!true		// true
```



#### 삼항 연산자 (Ternary Operator)

세 개의 피연산자를 사용하여 조건에 따라 **값**을 반환하는 연산자

가장 왼쪽의 조건식이 참이면 콜론(:) 앞의 값을 사용하고 그렇지 않으면 콜론(:) 뒤의 값을 사용한다.

삼항 연산자의 결과 값이기 때문에 변수에 할당 가능하다.

* 참고) 한 줄에 표기하는 것을 권장한다.

```javascript
console.log(true ? 1 : 2)		// 1
console.log(false ? 1 : 2)		// 2

const result = Math.PI > 4 ? 'Yes' : 'NO'
console.log(result)				// No
```

```javascript
let x = 1 > 2
x ? 1 : 2				// 2
```



cf) Python

```python
1 if True else 2		# 1
```



### 조건문

#### 'if' statement

조건 표현식의 결과값을 **Boolean 타입으로 변환 후 참/거짓을 판단**

**if, else if, else**

조건은 **소괄호(condition)** 안에 작성한다.

실행할 코드는 **중괄호{}** 안에 작성한다.

블록 스코프 생성

```javascript
if (condition){
    // do something
} else if (condition) {
    // do something
} else {
    // do something
}
```

```javascript
const nation = 'Korea'

if (nation === 'Korea') {
    console.log('안녕하세요!')
} else if (nation === 'France') {
    console.log('Bonjour!')
} else {
    console.log('Hello!')
}
// 안녕하세요!
```



#### 'switch' statement

조건 표현식의 결과값이 **어느 값(case)에 해당하는지 판별**

참고) 주로 특정 변수의 값에 따라 조건을 분기할 때 활용한다.

* 조건이 많아질 경우 if문보다 가독성이 나을 수 있다.

**switch**

**표현식(expression)의 결과값**을 이용한 조건문

**표현식의 결과값과 case문의 오른쪽 값**을 비교한다.

**break 및 default문은 [선택적]**으로 사용 가능하다.

**break문이 없는 경우 break문을 만나거나 default문을 실행할 때까지 다음 조건문 실행한다.**

블록 스코프 생성

```javascript
switch (expression) {
    case 'first value': {
        // do something
        [break]
    }
    case 'second value': {
        // do something
        [break]
    }
    [default: {
    	// do something     
    }]
}
```

```javascript
const nation = 'Korea'

switch(nation){
    case 'Korea':{
        console.log('안녕하세요!')
        break
    }
    case 'France':{
        console.log('Bonjour!')
        break
    }
    default: {
        console.log('Hello!')
    }
}
// 안녕하세요!
```

**Fall-through 이 경우 모두 출력**

```javascript
const nation = 'Korea'

switch(nation){
    case 'Korea':{
        console.log('안녕하세요!')
    }
    case 'France':{
        console.log('Bonjour!')
    }
    default: {
        console.log('Hello!')
    }
}
// 안녕하세요!
// Bonjour!
// Hello
```



**참고 if vs. switch**

```javascript
const numOne = 5
const numTwo = 10
let operator = '+'

if (operator === '+'){
    console.log(numOne + numTwo)
} else if (operator === '-'){
    console.log(numOne - numTwo)
} else if (operator === '*'){
    console.log(numOne * numTwo)
} else if (operator === '/'){
    console.log(numOne / numTwo)
} else {
    console.log('유효하지 않은 연산자입니다.')
}
// 15
```

```javascript
const numOne = 5
const numTwo = 10
let operator = '+'

switch (operator){
    case '+':{
        console.log(numOne + numTwo)
        break
    }
    case '-':{
        console.log(numOne - numTwo)
        break
    }
    case '*':{
        console.log(numOne * numTwo)
        break
    }
    case '/':{
        console.log(numOne / numTwo)
        break
    }
    default:{
        console.log('유효하지 않은 연산자입니다.')
    }
}
// 15
```



### 반복문

반복문의 종류와 특징

* while
* for
* for...**in**
  * 주로 **객체(object)의 속성들을 순회**할 때 사용한다.
  * 배열도 순회 가능하지만 인덱스 순으로 순회한다는 보장이 없으므로 **권장하지 않는다.**
* for...**of**
  * **반복 가능한(iterable) 객체를 순회**하며 **값을 꺼낼 때 사용**
  * 반복 가능한(iterable) 객체의 종류: Array, Map, Set, String 등

#### while

조건문이 참(true)인 동안 반복 시행한다.

조건은 **소괄호** 안에 작성한다.

실행할 코드는 **중괄호** 안에 작성한다.

블록 스코프 생성

```javascript
while (condition){
    // do something
}
```

```javascript
let i = 0
while (i<6){
    console.log(i)	// 0, 1, 2, 3, 4, 5
    i += 1
}
```



#### for

세미콜론(;)으로 구분되는 세부분으로 구성된다.

**initialization**

* **최초 반복문 진입 시 1회만 실행**되는 부분

**condition**

* **매 반복 시행 전 **평가되는 부분

**expression**

* **매 반복 시행 이후** 평가되는 부분

블록 스코프 생성

```javascript
for (initialization; condition; expression){
    // do something
}
```

```javascript
for (let i=0; i < 6; i++) {
    console.log(i)			// 0, 1, 2, 3, 4, 5
}
// 1. 반복문 진입 및 변수 i 선언
// 2. 조건문 평가 후 코드 블럭 실행
// 3. 코드 블록 실행 이후 i 값 증가
```



#### for...in

**객체(object)의 속성(key)들을 순회**할 때 사용한다.

배열도 순회 가능하지만 **권장하지 않는다.**

실행할 코드는 **중괄호** 안에 작성한다.

블록 스코프 생성

```javascript
for (variable in object) {
    // do something
}
```

```javascript
// object(객체) => key-value로 이루어진 자료구조
const capitals = {
    korea : 'soeul',
    france : 'paris',
    USA : 'washington D.C.'
}

for (let capital in capitals){
    console.log(capital)		// korea, france, USA
}
```

```javascript
const capitals = {
    korea : 'soeul',
    france : 'paris',
    USA : 'washington D.C.'
}

for (let capital in capitals){
    console.log(capital)		// korea, france, USA
}

for (let nation in capitals){
    console.log(`${nation}의 수도는 ${capitals[nation]}`)
}
// korea의 수도는 soeul
// france의 수도는 paris
// USA의 수도는 washington D.C.

for (let nation in capitals){
    console.log(`${nation}의 수도는 ${capitals.nation}`)
}
// korea의 수도는 undefined
// france의 수도는 undefined
// USA의 수도는 undefined
```



#### for...of

**반복 가능한(iterable) 객체를 순회하며 값을 꺼낼 때 사용한다.**

* Object은 iterable 객체가 아니다.

실행할 코드는 **중괄호** 안에 작성한다.

블록 스코프 생성

```javascript
for (variable of object) {
    // do something
}
```

**재할당 여부에 따라 let const 구분하여 사용**

```javascript
const fruits = ['apple', 'mango', 'strawberry']

for (let fruit of fruits) {
    fruit = fruit + '!'		// 내부의 재할당
    console.log(fruit)
}
// apple!
// mango!
// strawberry!

for (const fruit of fruits) {
    // fruit 재할당 불가
    console.log(fruit)
}
// apple
// mango
// strawberry
```



#### (참고) for...in vs. for..of

**for... in (객체 순회 적합)**

```javascript
const fruits = ['apple', 'mango', 'strawberry']

for (let fruit in fruits) {
    console.log(fruit)			// 0, 1, 2
}

// object
const capitals = {
    korea : 'soeul',
    france : 'paris',
    USA : 'washington D.C.'
}

for (let capital in caplitals){
    console.log(capital)		// korea, france, USA
}
```



**for...of (배열 순회 적합)**

```javascript
const fruits = ['apple', 'mango', 'strawberry']
for (let fruit of fruits) {
    console.log(fruit)			// apple, mango, strawberry
}

// object
const capitals = {
    korea : 'soeul',
    france : 'paris',
    USA : 'washington D.C.'
}

for (let capital of caplitals){
    console.log(capital)		
}
// Uncaught ReferenceError: caplitals is not defined
```



### 조건문과 반복문 정리

| 키워드   | 종류   | 연관 키워드           | 스코프      |
| -------- | ------ | --------------------- | ----------- |
| if       | 조건문 | -                     | 블록 스코프 |
| switch   | 조건문 | case, break, default  | 블록 스코프 |
| while    | 반복문 | break, continue       | 블록 스코프 |
| for      | 반복문 | break, continue       | 블록 스코프 |
| for...in | 반복문 | 객체 순회             | 블록 스코프 |
| for...of | 반복문 | 배열 등 Iterable 순회 | 블록 스코프 |
