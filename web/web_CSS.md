[toc]

# Web

## CSS

Cascading Style Sheets

: 스타일을 지정하기 위한 언어



① 선택한다.

② 스타일을 지정한다.

```css
h1{
    color: blue;
    font-size: 15px;
}
```

선택자(Selector): h1

선언(Declaration): color: blue 

속성(Property): font-size

값(Value): 15px



CSS 구문은 선택자를 통해 스타일을 지정할 <u>HTML요소</u>를 선택한다.

중괄호 안에서는 <u>속성과 값</u>, 하나의 쌍으로 이루어진 선언을 진행한다.

각 쌍은 선택한 요소의 속성, 속성에 부여할 값을 의미한다.

* <u>속성(Property)</u>: 어떤 스타일 <u>기능을 변경</u>할지 결정한다.(what)
* <u>값(Value)</u>: 어떻게 스타일 기능을 변경할지 결정한다.(how)



#### CSS 정의 방법

* 인라인(inline)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <h1 style="color: blue; font-size: 100px;">Hello</h1>
</body>
</html>
```

**해당 태그에 직접 style 속성을 활용한다.**



* 내부 참조(embedding) - \<style>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
	h1 {
        color: blue;
        font-size: 100px;
	}
  </style>
</head>
<body> 
</body>
</html>
```

**\<head> 태그 내에 \<style>에 지정한다.**



* 외부 참조(link file) - 분리된 CSS 파일

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>mySite</title>
  <link rel="stylesheet" href="mystyle.css">
</head>
<body>
  <h1>This is my site</h1>
</body>
</html>
```

```css
h1 {
    color: blue;
    font-size: 20px
}
```

**외부 CSS 파일을 \<head>내  \<link>를 통해 불러오기**



#### CSS with 개발자 도구

* style:  해당 요소에 선언된 모든 CSS **\<과정>**
* computed: 해당 요소에 최종 계산된 CSS **\<결과>**



### CSS Selectors

```css
h1{
  color: blue;
  font-size: 15px;
}
```

선택자(Selector): h1

선언(Declaration): color: blue

속성(Property): font-size

값(Value): 15px



#### 선택자(Select) 유형

기본 선택자

* 전체 선택자(*), 요소 선택자(h1,div)
* 클래스 선택자(.), 아이디 선택자(#), 속성 선택자

결합자(combinators)

* 자손 결합자, 자식 결합자(>)
* 일반 형제 결합자, 인접 형제 결합자

의사 클래스/요소 (Pseudo Class)

* 링크, 동적 의사 클래스
* 구조적 의사 클래스, 기타 의사 클래스, 의사 엘리먼트, 속성 선택자
* 태그 뒤에 붙여 추가적인 기능들을 부여할 수 있다.

cf) 의사클래스: 기능적으로 무엇인가를 만들때 (예: hover)

cf) 의사요소 :: (h1:: after)



#### 선택자 with 개발자 도구

* #sect1 > ul> li:nth-child(1)

```html
<body>
  <h1 class="green">HAPPY</h1>
  <h2>선택자 연습</h2>
  <div class="green box">
    box contents
    <div>
      <p>지역 목록</p>
      <ul>
        <li>서울</li>
        <li id="purple">인천</li>
        <li>강원</li>
        <li>경기</li>
      </ul>
    </div>
    <p>lorem + tab: 랜덥한 문자열 자동 생성!</p>
  </div>
  <h3>HELLO</h3>
  <h4>CSS</h4>
</body>
```

```html
<style>
  /* 정체 선택자 */
  * {
    color: red;
  }
    
  /* 요소 선택자 */
  * {
    color: orange;
  }
  
  h3,
  h4
  * {
    font-size : 10px;
  }
</style>
```

```html
<style>
  /* 클래스 선택자 */
  .green {
    color: green;    
  }
    
  /* id 선택자 */
  #purple {
    color: purple;    
  }

  /* 자식 선택자 */
  .box > p {
    font-size: 30px;    
  }
    
  /* 클래스 선택자 */
  .box p {
    color: blue;    
  }
</style>
```



#### CSS 선택자 정리

요소 선택자

* HTML 태그를 직접 선택

클래스(class) 선택자

* 마침표(.)문자로 시작하며, 해당 클래스가 적용된 항목을 선택
* 클래스 이름은 직관적으로 만든다.

아이디(id) 선택자

* \# 문자로 시작하며, 해당 아이디가 적용된 항목을 선택
* 일반적으로 하나의 문서에 1번만 사용. 여러 번 사용해도 동작하지만, 단일 id를 사용하는 것을 권장



#### CSS 적용 우선순위(cascading order)

CSS 우선순위를 아래와 같이 그룹을 지어볼 수 있다.

1 중요도(Importance) - 사용시 주의

* !important

2 우선 순위(Specificity)

* 인라인 > id > class, 속성, pseudo-class > 요소, pseudo-element

3 CSS 파일 로딩 순서

* 위 내용이 적용된다. 덮어씌워진다.



#### CSS 상속

CSS는 상속을 통해 부모 요소의 속성을 자식에게 상속하다.

* 속성(프로퍼티) 중에는 상속이 되는 것과 되지 않는 것들이 있따.
* 상속 되는 것 예시
  * Text 관련 요소(font, color, text-align), opacity, visibility 등
* 상속 되지 않는 것 예시
  * Box model 관련 요소(width, height, margin, padding, border, box-sizing, display), position 관련 요소(position, top/right/bottom/left, z-index) 등

**MDN에서 확인하기**



```html
<body>
  <p>안녕하세요<span>김싸피</span>입니다.</p>
</body>
```

```html
<style>
  p {
    /* 상속됨 */
    color: red;
    /* 상속 안됨*/
    border: 1px solid black;
}
  span{
    border: 1px solid blue;
}
</style>
```



### CSS 기본 스타일

#### 크기 단위

px (픽셀)

* 모니터 해상도의 한 화소인 '픽셀' 기준
* 픽셀의 크기는 변하지 않기 때문에 고정적인 단위

%

* 백분율 단위
* 가변적인 레이아웃에서 자주 사용

em

* (바로 위, 부모 요소에 대한) 상속의 영향을 받는다.
* 배수 단위, 요소에 지정된 사이즈에 상대적인 사이즈를 가진다.

rem(root em)

* (바로 위, 부모 요소에 대한) 상속의 영향을 받지 않음
* 최상위 요소(html)의 사이즈를 기준으로 배수 단위를 가진다.

viewport

* 웹 페이지를 방문한 유저에게 바로 보이게 되는 웹 컨텐츠의 영역 (디바이스 화면)
* 디바이스의 viewport를 기준으로 상대적인 사이즈가 결정된다.
* vw, vh, vmin(가로 세로 중 작은 것 기준), vmax(가로 세로 중 큰 것 기준)
  * 100hw: 세로 전체높이 
  * 100vw: 가로 전체높이



#### 색상 단위

색상 키워드

* 대소문자를 구분하지 않는다.
* red, blue, black과 같은 특정 색을 직접 글자로 나타냄

RGB 색상

* 16진수 표기법 혹은 함수형 표기법을 사용해서 특정 색을 표현하는 방식
* '#' + 16진수 표기법
* rgb() 함수형 표기법

HSL 색상

* 색상, 채도, 명도를 통해 특정 색을 표현하는 방식
* 색상, 채도, 명도

a는 alpha(투명도)

* 0(투명)~1(검정)

```css
# 모두 black
p { color: black; }
p { color: #000;}
p { color: #000000;}
p { color: rgb(0, 0, 0);}
p { color: hsl(120, 100%, 0);}

p { color: rgba(0, 0, 0, 0.5);}
p { color: hsla(120, 100%, 0.5);}
```



#### CSS 문서 표현

텍스트

* 서체, 서체 스타일
* 자간, 단어 간격, 행간, 들여쓰기 등

컬러(color), 배경(background-image, background-color)

기타 HTML 태그별 스타일링

* 목록(li), 표(table)



### Selectors 심화

#### 결합자 (Combinators)

자손 결합자

* selectorA 하위의 모든 selectorB 요소

```css
div span {
  color: red;
}
```

```html
<div>
  <span>이거 빨강입니다.</span>
  <p>이건 빨강이 아닙니다.</p>
  <p>
    <span>이건 빨강입니다.</span>    
  </p>
</div>
```



자식 결합자

* selectorA 바로 아래의 selectorB 요소

```css
div > span {
  color: red;
}
```

```html
<div>
  <span>이거 빨강입니다.</span>
  <p>이건 빨강이 아닙니다.</p>
  <p>
    <span>이건 빨강이 아닙니다.</span>    
  </p>
</div>
```



일반 형제 결합자

* selectorA의 형제 요소 중 뒤에 위치하는 selectorB 요소를 모두 선택

```css
p ~ span {
  color: red;
}
```

```html
<span>태그 앞에 있기 때문에 이건 빨강이 아닙니다.</span>
<p>여기 문단이 있습니다.</p>
<b>그리고 코드도 있습니다.</b>
<span>p태그와 형제이기 때문에 이건 빨강입니다.</span>
<b>더 많은 코드가 있습니다.</b>
<span>이것도 p태그와 형제이기 때문에 빨강입니다.</span>
```



인접 형제 결합자

* selectorA의 형제 요소 중 바로 뒤에 위치하는 selectorB 요소를 선택

```css
p + span {
  color: red;
}
```

```html
<span>태그 앞에 있기 때문에 이건 빨강이 아닙니다.</span>
<p>여기 문단이 있습니다.</p>
<span>p태그와 인접한 형제이기 때문에 이건 빨강입니다.</span>
<b>그리고 코드가 있습니다.</b>
<span>p태그와 인접한 형제가 아니기 때문에 이건 빨강이 아닙니다.</span>
```



### Box model

#### CSS 원칙

모든 요소는 네모(박스모델)이고, 위에서부터 아래로, 왼쪽에서 오른쪽으로 쌓인다.

(좌측 상단에 배치)

**Normal Flow**



#### Box model

모든 HTML요소는 box 형태로 되어 있다.

하나의 박스는 네 부분(영역)으로 이루어진다.

* content: 글이나 이미지 등 요소의 실제 내용
* padding: 테두리 안쪽의 내부 여백 요소에 적용된 배경색, 이미지는 padding까지 적용
* border: 테두리 영역
* margin: 테두리 바깥의 외부 여백 배경색을 지정할 수 없다.

​					  박스 사이의 관계에 필요한 것이다.



##### Box model 구성(margin/padding/border)

```css
.margin{
  margin-top: 10px;
  margin-right: 20px;
  margin-bottom: 30px;
  margin-left: 40px;
}

.margin-padding{
  margin: 10px;
  padding:30px;
}

.border{
  border-width: 2px;
  border-style: dashed;
  border-color: black;
}
```



shorthand를 통해서 표현 가능하다. **시계방향**

```css
# 모든 방향에 10px margin
.margin-1{
  margin: 10px;
}

# 상하 방향에 10px 좌우 방향에 20px margin
.margin-1{
  margin: 10px 20px;
}

# 비어있는 경우는 반대편 margin값에 맞춰 조정된다.
# 상 10px 오 20px 하 30px 좌 20px
.margin-1{
  margin: 10px 20px 30px;
}

# 상 10px 오 20px 하 30px 좌 40px
.margin-1{
  margin: 10px 20px 30px 40px;
}
```



border도 shorthand가 있다.

```css
.border {
  border-width: 2px;
  border-style: dashed;
  border-color: black;
}

# 위 코드를 줄일 수 있다.
# style은 필수
.bordr {
  border: 2px dashed black;
}
```



#### Box size

##### box-sizing

기본적으로 모든 요소의 box-sizing은 content-box

* padding을 제외한 순수 contents 영역만을 box로 지정

다만, 우리가 일반적으로 영역을 볼 때는 border까지의 너비를 100px 보는 것을 원한다.

* 그 경우 box-sizing을 border-box으로 설정

```html
<style>
  .box {
    width: 100px;
    margin: 10px auto;
    padding: 20px;
    border: 1px solid black;
    color: white;
    text-align: center;
    background-color: blueviolet;
    box-sizing: border-box;
  }
</style>
```



### CSS Display

모든 요소는 네모(박스모델)이고, 좌측상단에 배치한다.

**display에 다라 크기와 배치가 달라진다.**



display: block

* 줄 바꿈이 일어나는 요소
* <u>화면 크기 전체의 가로 폭을 차지한다.</u>
* <u>블록 레벨 요소 안에 인라인 레벨 요소가 들어갈 수 있다.</u>

display: inline

* <u>줄 바꿈이 일어나지 않는 행의 일부 요소</u>
* content 너비만큼 가로 폭을 차지한다.
* <u>width, height, margin-top, margin-bottom을 지정할 수 없다.</u>
* (가로 세로의 개념없이 자신의 size만을 가지고 있다.)
* 상하 여백은 line-height로 지정한다.



#### 블록 레벨 요소와 인라인 레벨 요소

블록 레벨 요소와 인라인 레벨 요소 구분(HTML 4.1까지)

대표적인 블록 레벨 요소

* div /ul, ol, li /p /hr /form 등

대표적인 인라인 레벨 요소

* span /a /img /input, label /b, em, i, strong 등



**block의 기본 너비는 가질 수 있는 너비의 100%**

너비를 가질 수 없다면 자동으로 부여되는 margin

inline의 기본 너비는 컨텐츠 영역만큼



#### 속성에 따른 수평 정렬

```html
# 왼쪽으로 박스를 붙인다.
margin-right: auto;

# 오른쪽으로 박스를 붙인다.
margin-left: auto;

# 중앙으로 박스를 붙인다.
margin-right: auto;
margin-left: auto;
```

```html
# inline는 margin이 없다.
# text-align을 사용한다.

# 왼쪽으로 text를 붙인다.
text-align: left;

# 오른쪽으로 text를 붙인다.
text-align: right;

# 중앙으로 text를 붙인다.
text-align: center;
```



#### display

display: inline-block

* block과 inline 레벨 요소의 특징을 모두 가진다.
* inline처럼 한 줄에 표시 가능하고, block처럼 width, height, margin 속성을 모두 지정할 수 있다.

display: none (hidden과 다르다.)

* 해당 요소를 화면에 표시하지 않고, <u>공간조차 부여되지 않는다.</u>
* 이와 비슷한 <u>visibility: hidden은 해당 요소가 공간은 차지하나 화면에 표시만 하지 않는다.</u>

이외 다양한 display 속성 

https://developer.mozilla.org/ko/docs/Web/CSS/display



### CSS Position

문서 상에서 요소를 위치를 지정한다.

static: 모든 태그의 기본 값(기준 위치)

* 일반적인 요소의 배치 순서에 따른다.(좌측 상단. Normal Flow를 따른다.)
* 부모 요소 내에서 배치될 때는 부모 요소의 위치를 기준으로 배치된다.

아래는 좌표 프로퍼티(top, bottom, left, right)를 사용하여 이동 가능하다.

* relative
* absolute
* fixed
* sticky



**relative: 상대 위치**

* 자기 자신의 static 위치를 기준으로 이동한다. (normal flow 유지)
* 레이아웃에서 요소가 차지하는 공간은 static 일 때와 같다. (normal position 대비 offset)



**absolute: 절대 위치**

* 요소를 일반적인 문서 흐름에서 제거 후 레이아웃에 공간을 차지하지 않는다. (normal flow에서 벗어난다.)
* static이 아닌 가장 가까이 있는 부모/조상 요소를 기준으로 이동한다. (없는 경우 body가 기준)
* (공간을 차지하지 않아 기준점이 필요하다.)



**fixed: 고정 위치**

* 요소를 일반적인 문서 흐름에서 제거 후 레이아웃에 공간을 차지하지 않는다. (normal flow에서 벗어난다.)
* 부모 요소와 관계없이 viewport를 기준으로 이동한다.
  * 스크롤 시에도 항상 같은 곳에 위치한다.



**sticky**

예) 사전까지 Alphabet에 붙어 있는 것



#### CSS 원칙

CSS 원칙 I, II: Normal flow

* 모든 요소는 네모(박스모델), 좌측상단에 배치
* display에 따라 크기와 배치가 달라진다.

CSS 원칙 III

* **position으로 위치의 기준을 변경**
  * static: 기본 값
  * relative: 본인의 원래 위치
  * absolute: 특정 부모의 위치
  * fixed: 화면의 위치



## 개발자 도구

### HTML & CSS

웹 브라우저 크롬에서 제공하는 개발과 관련된 다양한 기능을 제공한다.

주요 기능

* Elements: DOM 탐색 및 CSS 확인 및 변경, 해당 요소의 HTML 태그
  * Styles: 요소에 적용된 CSS 확인
  * Computed: 스타일이 계산된 최종 결과
  * Event Listeners: 해당 요소에 적용된 이벤트 (JS)
* ​	Sources, Network, Performance, Application, Security, Audits 등



#### HTML DOM 조작하기

Element에서 HTML 태그 구조를 탐색하며 추가, 삭제, 이동, 편집 등이 가능하다.



#### CSS - styles, computed

styles: 해당 요소에 선언된 모든 CSS

computed: 해당 요소에 최종 계산된 CSS



#### CSS 조작하기

우선순위, 파일 로딩 등에 의해 적용되고 있는 모든 CSS를 확인할 수 있다.

원하는 속성을 제거해보거나, 값을 변경하여 결과를 바로 확인할 수 있다.

현재 요소에 지정된 박스모델, 스타일에 대한 정보를 쉽게 확인할 수 있다.

박스모델에 해당하는 영역 값을 쉽게 변경할 수 있다.

해당 요소에 대한 스타일을 다양하게 추가해 볼 수 있다.

해당 요소에 기존에 정의된 클래스를 추가해 볼 수 있다.



## 추가 컨텐츠

### 학습 가이드라인

MDN web docs

https://developer.mozilla.org/ko/

개발자 도구 활용법

https://developer.chrome.com/docs/devtools/css/



### Emmet

HTML & CSS를 작성할 때보다 빠른 마크업을 위해서 사용되는 오픈소스

단축키, 약어 등을 사용

대부분의 텍스트 에디터에서 지원

https://emmet.io/

https://docs.emmet.io/cheat-sheet/

```html
! + tab
p.class + tab
dir#haha{!} + tab
ol>li*3.haha#hahaha + tab
```

