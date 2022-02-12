# Web

## Bootstrap

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="bootstrap.css">
  <title>Document</title>
</head>
<body>
  <h1>title</h1>
  <a href="#"></a>

  <script src="bootstrap.budle.js"></script>
</body>
</html>
```



Bootstrap에서 사용가능

* utilities (flexbox)
* component
* grid system



### CDN

Content Delivery(Distribution) Network

컨텐츠(CSS, JS, Image, Text 등)을 효율적으로 절달하기 위해 여러 노드에 가진 네트워크에 데이터를 제공하는 시스템

개별 end-user의 가까운 서버를 통해 빠르게 전달 가능(지리적 이점)

외부 서버를 활용함으로써 본인 서버의 부하가 적어짐



**CDN via jsDelivr활용**



### Spacing

브라우저 html의 root 글꼴 크기는 16px

| class name | rem  | px   |
| ---------- | ---- | ---- |
| m-1        | 0.25 | 4    |
| m-2        | 0.5  | 8    |
| m-3        | 1    | 16   |
| m-4        | 1.5  | 25   |
| m-5        | 3    | 48   |

|      |         | t    | top         |
| ---- | ------- | ---- | ----------- |
|      |         | b    | bottom      |
| m    | margin  | s    | left        |
| p    | padding | e    | right       |
|      |         | x    | left, right |
|      |         | y    | top, bottom |

**.mx-auto: 수평중앙 정렬**

**.ms-auto: 오른쪽 정렬**



### Color, Display, Position

color: primary, secondary, success, info, warning, danger, light, dark

배경색 class = bg-color

글자색 class = text-color

Display, Position을 공식문서 확인



#### Text에서의 사용

text-start, text-center, text-end

text-decoration-non

fw-bold, fw-normal, fw-light, fst-italic



#### Display

d-inline, d-box

box fixed-top, box fixed-bottom



### Components, Flexbox in Bootstrap

d-flex justify-contents-start

d-flex align-items-start

d-flex / align-self-start



### Responsive Web

반응형 웹

웹 디자인에 대한 접근 방식

반응형 레이아웃 작성에 도움이 되는 사례들의 모음 등을 기술하는데 사용되는 용어

Bootsrap의 이미지는 .img-fluid로 반응한다. 

* max-width: 100%;
* height: auto;

로 지정되어 부모 너비에 맞게 크기가 조정되도록 이미지에 추가된다.



예)

Media Queries, Flexbox, Bootstrap Grid System, The viewport meta tag



## Bootstrap Grid System

### Grid system (web design)

요소들의 디자인과 배치에 도움을 주는 시스템

기본 요소

* Column: 실제 컨텐츠를 포함하는 부분
* Gutter: 칼럼과 칼럼 사이의 공간 (사이 간격)
* Container: Column들을 담고 있는 공간



### Bootstrap Grid System

Bootstrap Grid system은 flexbox로 제작됨

container, row, column으로 컨텐츠를 배치하고 정렬

**반드시 기억해야 할 2가지**

**1. 12개의 column**

**2. 6개의 grid breakpoints**



#### Grid system

```html
<div class="container">
    <div class="row">
        <div class="col"></div>
        <div class="col"></div>
        <div class="col"></div>
    </div>
</div>
```



#### Grid system breakpoints

viewport에 따라 달라진다.

container와 breakpoint를 구별해서 사용



| Breakpoint                    | Class infix | Max container width |
| ----------------------------- | ----------- | ------------------- |
| **Extra-Small** <576px        | .col-       | None(auto)          |
| **Small** ≥576px              | .col-sm     | 540px               |
| **Medium** ≥768px             | .col-md     | 720px               |
| **Large **≥992px              | .col-lg     | 960px               |
| **Extra-Large** ≥1200px       | .col-xl     | 1140px              |
| **Extra-Extra-Large** ≥1400px | .col-xxl    | 1320px              |

**Gutter width 1.5rem(12px)**



**Grid System 사용을 위해 class container과 class row를 지정**

* container
  * row
    * col-(breakpoint: sm, md, lg, xl, xxl)-(1~12)

```html
<div class="container">
    <div class="row">
        <div class="box col">1</div>
        <div class="box col">2</div>
        <div class="box col">3</div>
    </div>
</div>
```



Grid system breakpoint는 연습이 필요

##### Grid system breakpoints

```html
<div class="row">
    <div class="box col-2 col-sm-8 col-md-4 col-lg-5">1</div>
    <div class="box col-8 col-sm-2 col-md-4 col-lg-2">1</div>
    <div class="box col-2 col-sm-2 col-md-4 col-lg-5">1</div>
</div>
```



##### nesting

```html
<div class="row">
    <div class="box col-6">
        <div class="row">
            <div class="box col-3">1</div>
            <div class="box col-3">2</div>
            <div class="box col-3">3</div>
            <div class="box col-3">4</div>
        </div>
    </div>
    <div class="box col-6">1</div>
    <div class="box col-6">2</div>
    <div class="box col-6">3</div>
</div>
```



##### offset

offset은 공간을 차지하며 contents보다 먼저 존재

```html
<div class="row">
    <div class="box col-md-4 offset-4">
        .col-md-4 .offset-4
    </div>
    <div class="box col-md-4 offset-4 offset-lg-2">
        .col-md-4 .offset-4 .offset-lg-2
    </div>
    </div>
</div>
```



이전 breakpoint에서 offset을 사용했을 경우

다음 breakpoint에서 offset-breakpoint-0 필요

```html
<body>
    <div class="container">
        <div class="row">
            <div class="item col-4 offset-md-4 col-md-4 col-lg-5 offset-lg-7">
                <p>item1</p>
      		</div>
      		<div class="item col-4 offset-4 col-md-4 offset-md-0 col-lg-8 offset-lg-2">
        		<p>item2</p>
      		</div>
    	</div>
    </div>
</body>
```



#### 추가

##### Border color

```html
<span class="border border-primary"></span>
<span class="border border-secondary"></span>
<span class="border border-success"></span>
<span class="border border-danger"></span>
<span class="border border-warning"></span>
<span class="border border-info"></span>
<span class="border border-light"></span>
<span class="border border-dark"></span>
<span class="border border-white"></span>
```



##### Border-width

rem이 아닌 px단위

```html
<span class="border border-1"></span>
<span class="border border-2"></span>
<span class="border border-3"></span>
<span class="border border-4"></span>
<span class="border border-5"></span>
```



##### Border-radius

```html
<img src="..." class="radius" alt="...">
<img src="..." class="radius-top" alt="...">
<img src="..." class="radius-end" alt="...">
<img src="..." class="radius-bottom" alt="...">
<img src="..." class="radius-start" alt="...">
<img src="..." class="radius-circle" alt="...">
<img src="..." class="radius-pill" alt="...">
```



##### utilities 문서확인

##### components 문서확인



bootsrap의 css폴더에서 사용하고자하는(bootstrap-grid.css)만 가져와서 사용가능



동작을 하는 기능에 javascript 필요
