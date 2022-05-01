# JavaScript 02

## DOM

### History of JavaScript

#### 핵심 인물: 

팀 버너스리(Tim Berners-Lee) 

- www, URL, HTTP, HTML 최초 설계자, 웹의 아버지

브랜던 아이크(Brenden Eich) 

- JavaScript 최초 설계자, 모질라 재단 공동 설립자, 코드네임 피닉스 프로젝트 진행

#### JavaScript의 탄생:

넷스케이프 커뮤니케이션스사의 Netscape Navigator(NN) 브라우저의 전 세계 점유율 80%이상 독점하며 브라우저의 표준 역할을 했다.

다시 넷스케이프에 재직 중이던 브랜던 아이크가 HTML을 동적으로 동작하기 위한 회사 내부 프로젝트를 진행 중에 JS를 개발했다.

JavaScript 이름 변천차 : Mocha -> LiveScript -> JavaScript

1995년 경쟁사 마이크로소프트에서 이를 채택하여 커스터마이징한 JScript를 만든다.

#### 브라우저 전쟁:

<u>제 1차 브라우저 전쟁</u>

넷스케이프 vs 마이크로소프트(MS)

빌 게이츠 주도하에 MS는 1997년 IE 4를 발표하면서 시장을 장악하기 시작한다.

* 당시 윈도우 OS의 시장 점유율은 90%
* 글로벌 기업 MS의 공격적인 마케팅

MS의 승리로 끝나며 2001부터 IE의 점유율은 90%를 상회한다.

1998년 넷스케이프에서 나온 브랜던 아이크 외 후계자들은 모질라 재단을 설립한다.

* 파이어폭스를 통해 IE에 대항하며 꾸준히 점유율을 올렸다.

MS의 폭발적 성장, IE3에서 자체적인 JScript를 지원, 호환성 문제로 크로스 브라우징의 이슈가 발생했다.

이후 넷스케이프 후계자들은 모질라 재단 기반의 파이어폭스를 개발했다.



<u>제 2차 브라우저 전쟁</u>

MS vs Google

2008년 Google의 Chrome 브라우저 발표

2011년 3년 만에 파이어폭스의 점유율을 돌파 후 2012년 부터 전 세계 점유율 1위에 등극한다.

크롬의 승리 요인

* 압도적인 속도
* 강력한 개발자 도구 제공
* 웹 표준



#### 파편화와 표준화:

제 1차 브라우저 전쟁 이후 수많은 브라우저에서 자체 자바스크립트 언어를 사용하게 된다.

결국 서로 다른 자바스크립트가 만들어지면서 크로스 브라우징 이슈가 발생하여 웹 표준의 필요성이 제기되었다.

**<u>크로스 브라우징</u>**

* W3C에서 채택된 표준 웹 기술을 채용하여 각각의 브라우저마다 다르게 구현되는 기술을 비슷하게 만들되, 어느 한쪽에 치우치지 않도록 웹 페이지를 제작하는 방법론 (동일성이 아닌 동등성)
* 브라우저마다 렌더링에 사용하는 엔진이 다르기 때문이다.



1996년부터 넷스케이프는 표준 제정의 필요성을 주장했다.

* ECMA 인터내셔널(정보와 통신 시스템을 위한 국제적 표준화 기구)에 표준 제정 요청

1997년 ECMAScript 1(ES1) 탄생

제1차 브라우저 전쟁 이후 제기된 언어의 파편화를 해결하기 위해 각 브라우저 회사의 재단은 표준화에 더욱 적극적으로 힘을 모으기 시작했다.



#### JavaScript ES6+:

2015년 ES2015 (ES6) 탄생

* "Next-gen of JS"
* JavaScript의 고질적인 문제들을 해결했다.
* JavaScript의 다음 시대라고 불릴 정도로 많은 혁신과 변화를 맞이한 버전
* 이때부터 버전 순서가 아닌 출시 연도를 붙이는 것이 공식 명칭이나 통상적으로 ES6라고 부른다.
* 현재는 표준 대부분이 ES6+로 넘어왔다.



#### Vanilla JavaScript

크로스 브라우징, 간편한 활용 등을 위해 많은 라이브러리가 등장했다.

ES6 이후, 다양한 도구의 등장으로 순수 자바스크립트 활용의 증대했다.



#### 정리

History of JavaScript & Browser

* 브라우저 전쟁
* 파편화와 표준화의 투쟁

브라우저 전쟁의 여파

* Cross Browsing Issue
* 표준화(통합)를 위한 노력
* Vanilla JavaScript



## DOM 조작과 Event

### DOM

#### 브라우저에서 할 수 있는 일

DOM 조작

* 문서(HTML) 조작

BOM 조작

* navigator, screen, location, frames, history, XHR

JavaScript Core (ECMAScript)

* Data Structure(Object, Array), Conditional Expression, Iteration



#### DOM 이란?

HTML, XML과 같은 문서를 다루기 위한 문서 프로그래밍 인터페이스

문서를 구조화하고 구조화된 구성 요소를 하나의 객체로 취급하여 다루는 논리적 트리 모델

문서가 구조화되어 있으며 각 요소는 객체(object)로 취급한다.

단순한 속성 접근, 메서드 활용뿐만 아니라 프로그래밍 언어적 특성을 활용한 조작이 가능하다.

주요 객체

* window: DOM을 표현하는 창. 가장 최상위 객체(작성 시 생략 가능하다)
* document: 페이지 컨텐츠의 Entry Point 역할을 하며, `<body>`등과 같은 수많은 다른 요소들을 포함한다.
* navigator, location, history, screen



#### DOM - 해석

파싱(Parsing)

* 구문 분석, 해석
* 브라우저가 문자열을 해석하여 DOM Tree로 만드는 과정

```javascript
document.title = 'JavaScript'
```



#### BOM 이란?

Browser Object Model

자바스크립트가 브라우저와 소통하기 위한 모델

브라우저의 창이나 프레임을 추상화해서 프로그래밍적으로 제어할 수 있도록 제공하는 수단

* 버튼, URL 입력창, 타이틀 바 등 브라우저 윈도우 및 웹 페이지 일부분을 제어 가능하다.

window 객체는 모든 브라우저로부터 지원받으며 브라우저의 창(window)를 지칭한다.

```javascript
window.open()			// 탭 창
window.print()			// 인쇄 창
window.confirm()		// 메시지 및 확인, 취소 버튼이 있는 대화상자 창
window.document			// document도 브라우저 내에 종속되어 있기 때문에 window 전역 객체에 포함된다.
```



#### JavaScript Core

```javascript
const number = [1, 2, 3, 4, 5]
for (let i=0; i < numbers.length; i++){
    console.log(numbers[i])
}
// 1
// 2
// 3
// 4
// 5
```

### DOM 조작

#### 개념

Document는 문서 한 장(HTML)에 해당하고 이를 조작한다.

DOM 조작 순서

1. 선택 (Select)
2. 변경(Manipulation)



#### DOM 관련 객체의 상속 구조

**EventTarget**

* **Node**
  * **Element / Document**
    * **HTMLElement**



EventTarget

* Event Listener를 가질 수 있는 객체가 구현하는 DOM 인터페이스

Node

* 여러 가지 DOM 타입들이 상속하는 인터페이스

Element

* Document 안의 모든 객체가 상속하는 가장 범용적인 인터페이스
* 부모인 Node와 그 부모인 EventTarget의 속성을 상속

Document(<u>HTML을 상징하는 객체</u>)

* 브라우저가 불러운 웹 페이지를 나타낸다.
* DOM 트리의 진입점(entry point) 역할을 수행한다.

HTMLElement

* 모든 종류의 HTML 요소
* 부모 element의 속성 상속



#### DOM 선택

##### 선택 관련 메서드

document.**querySelector(seletor)**

* 제공한 선택자와 일치하는 element 하나 선택
* 제공한 CSS selector를 만족하는 첫 번째 element 객체를 반환한다. (없다면 null)

document.**querySelectorAll(selector)**

* 제공한 선택자와 일치하는 여러 element를 선택한다.
* 매칭 할 하나 이상의 셀렉터를 포함하는 유효한 CSS selector를 인자(문자열)로 받는다.
* 지정된 셀렉터에 일치하는 NodeList를 반환한다.

getElementById(id)

getElementByTagName(name)

getElementsByClassName(names)



**querySelector(), querySelectorAll()을 사용하는 이유**

id, class 그리고 tag 선택자 등을 모두 사용 가능하므로, 더 구체적이고 유연하게 선택 가능하다.

예) 

document.querySelector('#id')

document.querySelector('.class')



##### 선택 메서드별 반환 타입

단일 element

* getElementById()
* **querySelector()**

HTMLCollection

* getElementsByTagName()
* getElementsByClassName()

NodeList

* **querySelectorAll()**



##### HTMLCollection & NodeList

둘 다 배열과 같이 각 항목에 접근하기 위한 index를 제공한다. (유사 배열)

**HTMLCollection**

* name, id, index 속성으로 각 항목에 접근 가능하다.

**NodeList**

* indes로만 각 항목에 접근 가능하다.
* 단, HTMLCollection과 달리 배열에서 사용하는 forEach 메서드 및 다양한 메서드를 사용가능하다.

둘 다 Live Collection으로 DOM의 변경사항을 실시간으로 반영하지만, **querySelectorAll()에 의해 반환되는 NodeList는 Static Collection으로 실시간으로 반영되지 않는다.**



##### Collectin

**Live Collection**

* 문서가 바뀔 때 실시간으로 업데이트 된다.

* DOM의 변경사항을 실시간으로 collection에 반영한다.

  예) HTMLCollection, NodeList

**Static Collection (non-live)**

* DOM이 변경되어도 collection 내용에는 영향을 주지 않는다.
* querySelectorAll()의 반환 NodeList만 static collection



:heavy_check_mark: **DOM 선택 실습**



#### DOM 변경

##### 변경 관련 메서드 (Creation)

document**.createElement()**

* 작성한 태그 명의 HTML 요소를 생성하여 반환

```javascript
// primitive
const a = 1

// Ref
const obj = {}
```



##### 변경 관련 메서드 (append DOM)

Element**.append()**

* 특정 부모 Node의 자식 NodeList 중 마지막 자식 다음에 Node 객체나 DOMString을 삽입한다.
* 여러 개의 Node 객체, DOMString을 추가 할 수 있다.
* 반환 값이 없다.

```javascript
const ulTag = document.querySelector('ul')
const newLiTag = document.createElement('li')
newLiTag.innerText = 'New'
ulTag.append(newLiTag)
ulTag.append('string')

const new1 = document.createElement('li')
new1.innerText = 'list1'
const new2 = document.createElement('li')
new2.innerText = 'list2'
ulTag.append(new1, new2)
```



Node**.appendChild()**

* 한 Node를 특정 부모 Node의 자식 Nodelist 중 마지막 자식으로 삽입 (Node만 추가 가능하다.)
* 한번에 **오직 하나의 Node**만 추가할 수 있다.
* 만약 주어진 Node가 이미 문서에 존재하는 다른 Node를 참조한다면 새로운 위치로 이동한다.

```javascript
const ulTag = document.querySelector('ul')
const newLiTag = document.createElement('li')
newLiTag.innerText = 'New'
ulTag.appendChild(newLiTag)
ulTag.appendChild('string')
// Uncaught TypeError: Failed to execute 'appendChild' on 'Node': parameter 1 is not of type 'Node'.

const new1 = document.createElement('li')
new1.innerText = 'list1'
const new2 = document.createElement('li')
new2.innerText = 'list2'
ulTag.append(new1, new2)
```



##### ParentNode.append() vs Node.appendChild()

append()를 사용하면 DOMString 객체를 추가할 수도 있지만, .appendChild()는 Node 객체만 허용한다.

append()는 반환 값이 없지만, appendChild()는 추가된 Node의 객체를 반환한다.

append()는 여러 Node 객체와 문자열을 추가할 수 있지만, appendChild()는 하나의 Node 객체만 추가할 수 있다.



##### 변경 관련 속성(property)

Node.**innerText**

* Node 객체와 그 자손의 텍스트 컨텐츠(DOMString)를 표현(해당 요소 내부의 raw text)
  * 사람이 읽을 수 있는 요소만 남긴다.
* 즉, 줄 바꿈을 인식하고 숨겨진 내용을 무시하는 등 최종적으로 스타일링이 적용된 모습으로 표현된다.

Element.**innerHTML**

* 요소(element) 내에 포함된 HTML 마크업을 반환한다.
* 참고) XSS 공격에 취약하므로 사용 시 주의

```javascript
const ulTag = document.querySelector('ul')
const liTag1 = document.createElement('li')
liTag1.innerText = '<li>춘천</li>'			// String으로 인지

const liTag2 = document.createElement('li')
liTag2.innerHTML = '<li>춘천</li>'			// HTML로 인지
ulTag.append(liTag1, liTag2)
```



##### XSS(Cross-site Scripting)

공격자가 입력요소를 사용하여(\<input>) 웹사이트 클라이언트 측 코드에 악성 스크립트를 삽입해 공격하는 방법

피해자(사용자)의 브라우저가 악성 스크립트를 실행하여 공격자가 엑세스 제어를 우회하고 사용자를 가장할 수 있도록 한다.

예시) 게시판이나 메일 등 악성 자바스크립트 코드를 삽입해 민감한 정보를 탈취할 수 있다.



#### DOM 삭제

##### 삭제 관련 메서드

ChildNode.**remove()**

* Node가 속한 트리에서 해당 Node를 제거한다.



Node.**removeChild()**

* DOM에서 자식 Node를 제거하고 제거된 Node를 반환한다.
* Node는 인자로 들어가는 자식 Node의 부모 Node

```javascript
const header = document.querySelector('#location-header')
header.remove()

const parent = document.querySelector('ul')
const child = document.querySelector('ul >  li')
const removeChild = parent.removeChild(child)
console.log(removeChild)
```



#### DOM 속성

##### 속성 관련 메서드

Element.**setAttribute(name, value)**

* 지정된 요소의 값을 설정한다.
* 속성이 이미 존재하면 값을 갱신하고, 존재하지 않으면 지정된 이름과 값으로 새 속성을 추가한다.

```javascript
const header = document.querySelector('#location-header')
header.setAttribute('class','happy-location')
```



Element.**getAttribute(attributeName)**

* 해당 요소의 지정된 값(문자열)을 반환한다.
* 인자(attributeName)는 값을 얻고자 하는 속성의 이름

```javascript
const getAttr = document.querySelector('.happy-location')
getAttr.getAttribute('class')
// 'happy-location'
```



#### DOM 조작 정리

**1. 선택한다.**

querySelector()

querySelectorAll()

**2. 변경(조작)한다.**

innerText

innerHTML

element.style.color

setAttribute()

getAttribute()

createElement()

append()

appendChild()



### Event

네트워크 활동이나 사용자와의 상호작용 같은 사건의 발생을 알리기 위한 객체

이벤트 발생

* 마우스를 클릭하거나 키보드를 누르는 등 사용자 행동을 발생할 수도 있다.
* 특정 메소드를 호출(Element.click())하여 프로그래밍적으로도 만들어낼 수 있다.



#### Event 기반 인터페이스

AnimationEvent, ClipboardEvent, DragEvent 등

UIEvent

* 간단한 사용자 인터페이스 이벤트
* Event의 상속을 받는다.
* MouseEvent, KeyboardEvent, InputEvent, FocusEvent 등의 부모 객체 역할을 한다.



#### Event의 역할

**~하면 ~한다.**

클릭(Event)하면 경고창(결과)를 띄운다.

특정 이벤트가 발생하면 할일을 등록한다.



#### Event handler - addEventListener()

EventTarget.**addEventListener()**

* 지정한 이벤트가 대상에 전달될 때마다 호출할 함수를 설정한다.
* 이벤트를 지원하는 모든 객체(Element, Document, Window등)를 대상으로 지정 가능하다.



target.**addEventListener(type, listener[, options])**

target.addEventListener(종류, 일/동작 명세(함수))

type

* 반응할 이벤트 유형 (대소문자 구분 문자열)

listener

* 지정된 타입의 이벤트가 발생했을 때 알림을 받는 객체 EventListener인터페이스 혹은 JS function 객체(콜백 함수)여야 한다.

**EventTarger은 EventListener를 가질 수 있는 객체가 구현하는 DOM 인터페이스**

모든 요소는 event를 달아줄 수 있다. 화면에 보이는 요소부터 보이지 않는 요소까지



<u>대상에 특정 이벤트가 발생하면, 할일을 등록하자</u>

대상 : EventTarget

특정 이벤트: (type, )

할 일: ( , listener)



```javascript
const btn = document.querySelector('button')
btn.addEventListener('click', function(event){
    alert('clicked the button')
    console.log(evnet)
})
```

```html
<!--이 방법은 inline style이여서 쓰지 않는다.-->
<button onclick="alertMessage()">Click me!</button>
<script>
	const alertMessage = function(){
        alert('Clicked the button')
    }
</script>
```

```html
<button id="my-button">Click me!</button>

<script>
   	const alertMessage = function(){
        alert('Clicked the button')
    }
	const myButton = document.querySelector('#my-button')
    myButton.addEventListener('click', alertMessage)
</script>
```





```html
<p id="my-paragraph"></p>

<form action="#">
  <label for="my-text-input">내용을 입력하세요.</label>
  <input id="my-text-input" type="text">
</form>
```

```javascript
const myTextInput = document.querySelector('#my-text-input')
myTextInput.addEventListener('input', function(event){
    const myPtag = document.querySelector('#my-paragraph')
    myPtag.innerText = event.target.value
})
```





```html
<h2>Change My Color</h2>
<label for="change-color-input">원하는 색상을 영어로 입력하세요</label>
<input id="change-color-input">
<hr>

<script>
	const colorInput = document.querySelector('#change-color-input')
    
    const changeColor = function(event){
        const h2Tag = document.querySelector('h2')
        h2Tag.style.color = event.target.value
    }
    
    colorInput.addEventListener('input', changeColor)
</script>
```



#### Event 취소

event.**preventDefault()**

현재 이벤트의 기본 동작을 중단한다.

HTML 요소의 기본 동작을 작동하지 않게 막는다.

* a 태그의 기본 동작은 클릭 시 링크로 이동
* form 태그의 기본동작은 form 데이터 전송

이벤트를 취소할 수 있는 경우, 이벤트의 전파를 막지 않고 그 이벤트를 취소한다.

```html
<input type="checkbox" id="my-checkbox">

<script>
	const checkBox = document.querySelector('#my-checkbox')
    checkBox.addEventListener('click', function(event){
        event.preventDefault()
        console.log(event)
    })
</script>
```

**click을 막는 것이 아니라 click했을 때 기본 값으로 정해진 것이 있다면 그것을 막겠다.**



``` html
<form action="/acticle/" id="my-form">
	<input type="text">
    <input type="submit" value="제출">
</form>
<script>
	const formTag = document.querySelector('#my-form')
   	formTag.addEventListener('submit', function(event){
        console.log(event)
        event.preventDefault()		// submit을 일괄 차단
        event.target.reset()		// even.target === formTag 항상 addEventListener의 주어
    })
</script>
```



```html
<a href="https://google.com/" target="_blank" id="my-link">Google</a>

<script>
	const aTag = document.querySelector('#my-link')
    
    aTag.addEventListener('click', function(event){
        console.log(event)
        event.preventDefault()		// 이동, 화면전환 일어나지 않는다.
    })
</script>
```



```html
<style>
    body {
        height: 10000px;
    }
</style>

<script>
    // document 전체에 listener를 달아줄 수 있다.
	document.addEventListener('scroll', function(event){
        console.log(event)
        event.preventDefault()		// cancelable: false
        							// scroll은 기본값이 없다. preventDefault: false
    })
</script>
```

**취소 할 수 없는 이벤트도 존재한다.**

* 이벤트의 취소 가능 여부는 event.cancelable을 사용해 확인할 수 있다.



#### Event 추가 학습

다양한 이벤트 유형 참고

https://developer.mozilla.org/en-US/docs/Web/Events

cf) 둘은 동일하다.

```html
<button>Add</button>
<form><input type="submit"></form>
```



#### Event 종합 실습

CREATE, READ 기능을 충족하는 todo app 만들기

```html
<form>
    <input type="text">
    <button>Add</button>
</form>
<ul></ul>

<script>
	// 이벤트 타겟 설정
    const form = document.querySelector('form')
    
    const function addTodo(event){
        // event의 기본 동작을 막는다.
        event.preventDefault()
        
        // input 요소를 선택하고, value 값을 저장한다.
        const input = document.querySelector('input')
        const content = input.value
        
        if (content.trim()){
            // 새로운 li 요소 생성, input value를 innerText로 넣는다.
            const li = document.createElement('li')
            li.innerText = content
            
            // ul 요소를 선택, ul의 자식 요소로 li 요소를 추가한다.
            const ul = document.querySelector('ul')
            ul.appendChild(li)
        } else {
            alert('할 일을 입력해주세요.')
        }
        event.target.reset()
    }
    
    form.addEventListener('submit', addTodo)
</script>
```

