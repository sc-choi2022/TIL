# Vue 02

## Vue CLI

### SFC

#### Component(컴포넌트)

(부품)

기본 HTML 엘리먼트를 확장하여 재사용 가능한 코드를 캡슐화하는데 도움을 준다.

CS에서는 다시 사용할 수 있는 범용성을 위해 개발된 소프트웨어 구성 요소를 의미한다.

즉, 컴포넌트는 유지보수를 쉽게 만들어 줄 뿐만 아니라, 재 사용성의 측면에서도 매우 강력한 기능을 제공한다.

**Vue 컴포넌트 === Vue 인스턴스**



#### SFC (Single File Component)

Vue의 컴포넌트 기반 개발의 핵심 특징

하나의 컴포넌트는 .vue 확장자를 가진 하나의 파일 안에서 작성되는 코드의 결과물

화면의 특정 영역에 대한 HTML, CSS, JavaScript 코드를 하나의 파일(.vue)에서 관리

즉, .vue 확장자를 가진 싱글 파일 컴포넌트를 통해 개발하는 방식

**Vue 컴포넌트 === Vue 인스턴스 === .vue 파일**



#### Component 예시

**단일 파일 관리**

단일 파일에서의 개발

* 처음 개발을 시작할 때는 크게 신경 쓸 것이 없기 때문에 쉽게 개발 가능하다.
* 하지만 코드의 양이 많아지면 변수 관리가 힘들어지고 유지보수에 많은 비용 발생한다.



**한 화면을 구성하는 여러 컴포넌트**

각 기능 별로 파일을 나눠서 개발한다.

* 처음 개발을 준비하는 단계에서 시간 소요가 증가한다.
* 하지만 이후 변수 관리가 용이하며 기능 별로 유지 & 보수 비용이 감소한다.



#### Vue Component 구조 예시

한 화면 안에서도 기능 별로 각기 다른 컴포넌트가 존재한다.

* 하나의 컴포넌트는 여러 개의 하위 컴포넌트를 가질 수 있다.
* Vue는 컴포넌트 기반의 개발 환경을 제공한다.



Vue 컴포넌트는 **const app = new Vue({...})**의 app을 의미하여 이는 Vue 인스턴스

* 여기서 오해하면 안되는 것은 컴포넌트 기반의 개발이 **반드시 파일 단위로 구분되어야 하는 것이 아니라는 것**

* 단일 .html 파일 안에서도 여러 개의 컴포넌트를 만들어 개발 가능하다.



#### 정리

Vue 컴포넌트는 Vue 인스턴스(new Vue({}))이기도 하다.

Vue 인스턴스는 .vue 파일 안에 작성된 코드의 집합이다.

HTML, CSS, 그리고 JavaScript를 .vue라는 확장자를 가진 파일 안에서 관리하며 개발한다.



### Vue CLI

Vue.js 개발을 위한 표준 도구

프로젝트의 구성을 도와주는 역할을 하며 Vue 개발 생태계에서 표준 tool기준을 목표로 한다.

확장 플러그인, GUI, Babel등 다양한 tool을 제공한다.



#### Node.js

자바스크립트를 브라우저가 아닌 환경에서도 구동할 수 있도록 하는 자바스크립트 런타임 환경

* 브라우저 밖을 벗어 날 수 없던 자바스크립트 언어의 태생적 한계를 해결한다.

Chrome V8엔진을 제공하여 여러 OS 환경에서 실행할 수 있는 환경을 제공한다.

즉, 단순히 브라우저만 조작할 수 있던 자바스크립트를 SSR 아키텍처에서도 사용할 수 있도록 한다.



[참고] 2009년 Ryan Dahl에 의해 발표



#### NPM(Node Package Manage)

자바스크립트 언어를 위한 패키지 관리자

* Python에 pip가 있다면 Node.js에는 NPM
* pip와 마찬가지로 다양한 의존성 패키지를 관리

Node.js의 기본 패키지 관리자

Node.js 설치시 함께 설치된다.



#### Vue CLI Quick Start

설치

```bash
$ npm install -g @vue/cli
```

* -g는 공식문서에 작성된 경우에만 사용하는 것을 권장

버전 확인

```bash
$ vue --version
```



**git-bash아닌 vscode terminal로 진행**

프로젝트 생성

```bash
$ vue create my-first-app
```

npm 레지스트리 변경(환경에 따라 나오지 않을 수 있다.)

```bash
? Your connectionto the default npm registry seems to be slow.
  Use https://registry.npm.taobao.org for faster installations? Yes
```

* 나온다면 Yes하면 된다.

Vue 버전 선택(Vue 2)

```bash
Vue CLI v5.0.4
? Please pick a preset: (Use arrow keys)
  Default ([Vue 3] babel, eslint)
  Default ([Vue 3] babel, eslint)
> Manually select features
```

프로젝트 생성 성공

```bash
🎉	Successfully created project my-first-app.
👉	Get started with the following commands:

$ cd my-first-app
$ npm run serve
```

프로젝트 디렉토리 이동

```bash
$ cd my-first-app
```

서버 실행

```bash
$ npm run serve
```

서버를 끄는 방법

ctrl + c



### Babel & Webpack

#### Vue 프로젝트 구조

* babel.config.js
* webpack



#### Babel

"JavaScript compiler"

자바스크립트의 ECMAScript 2015+ 코드를 이전 버전으로 번역/변환해 주는 도구

과거 자바스크립트의 파편화와 표준화의 영향으로 코드의 스펙트럼이 매우 다양하다.

* 이 때문에 최신 문법을 사용해도 이전 브라우저 혹은 환경에서 동작하지 않는 상황이 발생한다.

원시 코드(최신 버전)를 목적 코드(구 버전)로 옮기는 번역기가 등장하면서 개발자는 더 이상 내 코드가 특정 브라우저에서 동작하지 않는 상황에 대해 크게 고민하지 않을 수 있게 되었다.



#### Webpack

"static module bundler"

모듈간의 의존성 문제를 해결하기 위한 도구

프로젝트에 필요한 모든 모듈을 매핑하고 내부적으로 종속성 그래프를 빌드한다.



#### Static <u>Module</u> Bundler

모듈은 단지 파일 하나를 의미 (ex. js파일 하나 === 모듈 하나)

배경

* 브라우저만 조작할 수 있었던 시기의 자바스크립트는 모듈 관련 문법없이 사용되었다.
* 하지만 JS와 애플리케이션이 복잡해지고 크기가 커지자 전역 scope를 공유하는 형태의 기존 개발 방식의 한계점이 드러났다.
* 그래서 라이브러리를 만들어 필요한 모듈을 언제든지 불러오거나 코드를 모듈 단위로 작성하는 등의 다양한 시도가 이루어졌다.

여러 모듈 시스템

* **ESM(ECMA Script Module)**

* AMD(Asynchronous Module Definition)
* CommonJS
* UMD(Universal Module Definition)



#### Module 의존성 문제

모듈의 수가 많아지고 라이브러리 혹은 모듈간의 의존성(연결성)이 깊어지면서 특정한 곳에서 발생한 문제가 어떤 모듈간의 문제인지 파악하기 어려워졌다.

Webpack은 이 모듈 간의 의존성 문제를 해결하기 위해 등장했다.



#### Static Module <u>Bundler</u>

모듈 의존성 문제를 해결해주는 작업을 Bundling이라고 한다.

이런한 일을 해주는 도구가 Bundler이고, Webpack은 다양한 Bundler 중 하나이다.

여러 모듈을 하나로 묶어주고 묶인 파일은 하나(혹은 여러 개)로 합쳐진다.

Bundling된 결과물은 더 이상 순서에 영향을 받지 않고 동작하게 된다.

snowpack, parcel, rollup.js 등의 webpack 이외에도 다양한 모듈 번들러가 존재한다.

**Vue CLI는 이러한 Babel, Webpack에 대한 초기 설정이 자동으로 되어 있다.**



####  node_module의 의존성 깊이

**HEAVISE OBJECTS IN THE UNIVERSE**



#### 정리

**Node.js**

* JavaScript Runtime Environment
* JavaScript를 브라우저 밖에서 실행할 수 있는 새로운 환경

**Babel**

* Compiler
* ES2015+ JavaScript 코드를 구 버전의 JavaScript로 바꿔주는 도구

**Webpack**

* Module Bundler
* 모듈 간의 의존성 문제를 해결하기 위한 도구



#### Vue 프로젝트 구조

node_modules <u>(git에 올리면 안됨, 용량도 크다, 자동으로 .ignore파일 만들어진다.)</u>

* node.js 환경의 여러 의존성 모듈

public/index.html(SPA, 실제 html은 한장)

* Vue앱의 뼈대가 되는 파일
* 실제 제공되는 단일 html 파일

<u>(우리가 작업하는 데 중요한 것은 src)</u>

src/assets (이미지 등)

* webpack에 의해 빌드된 정적 파일

src/components

* 하위 컴포넌트들이 위치

src/App.vue

* 최상위 컴포넌트

src/main.js

* webpack이 빌드를 시작할 때 가장 먼저 불러오는 entry point
* <u>실제 단일 파일에서 DOM과 data를 연결했던 것과 동일한 작업이 이루어지는 곳</u>
* Vue 전역에서 활용할 모듈을 등록할 수 있는 파일

babel.config.js

* babel관련 설정이 작성된 파일

<u>(package.json와 package-lock.json은 requirement.txt 같은 것)</u>

package.json

* 프로젝트의 종속성 목록과 지원되는 브라우저에 대한 구성 옵션이 포함

package-lock.json

* node_modules에 설치되는 모듈과 관련된 모든 의존성을 설정 및 관리
* 팀원 및 배포 환경에서 정확히 동일한 종속성을 설치하도록 보장하는 표현
* 사용할 패키지의 버전을 고정
* 개발 과정 간의 의존성 패키지 충돌 방지



### Pass Props & Emit Event

#### 컴포넌트 작성

Vue app은 자연스럽게 중첩된 컴포넌트 트리로 구성된다.

컴포넌트간 부모-자식 관계가 구성되며 이들 사이에 필연저긍로 의사 소통이 필요하다.

부모는 자식에게 데이터를 전달(Pass props)하며, 자식은 자신에게 일어난 일을 부모에게 알린다(Emit event).

* 부모와 자식이 명확하게 정의된 인터페이스를 통해 격리된 상태를 유지할 수 있다.

**props는 아래로, events는 위로**

부모는 props를 통해 자식에게 '데이터'를 전달하고, 자식은 events를 통해 부모에게 '메시지'를 보낸다.



#### 컴포넌트 구조

1. 템플릿 (HTML)
2. 스크립트 (JavaScript)
3. 스타일 (CSS)

##### 템플릿(HTML)

HTML의 body부분

각 컴포넌트를 작성한다.



##### 스크립트 (JavaScript)

JavaScript가 작성되는 곳

컴포넌트 정보, 데이터, 메서드 등 vue 이느턴스를 구성하는 대부분이 작성된다.



##### 스타일 (CSS)

CSS가 작성되며 컴포넌트의 스타일을 담당한다.



#### 컴포넌트 등록 3단계

1. 불러오기 (import)
2. 등록하기 (register)
3. 보여주기 (print)

```vue
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- 3. 보여주기 (print)-->
    <!-- CamelCase -->
    <TheAbout/>
    <!-- kebab-case -->
    <the-about></the-about>
  </div>
</template>

<script>
// 1. 불러오기 (import)
import TheAbout from './components/TheAbout.vue'
export default {
  name: 'App',
  components: {
    // 2. 등록하기 (register)
    TheAbout
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```



#### Pass Props & Emit Events

#### Props

props는 부모(상위) 컴포넌트의 정보를 전달하기 위한 사용자 지정 특성이다.

자식(하위) 컴포넌트는 props 옵션을 사용하여 수신하는 props를 명시적으로 선언해야 한다.

즉, 데이터는 props옵션을 사용하여 자식 컴포넌트로 전달된다.



주의

* 모든 컴포넌트 인스턴스에는 자체 격리된 범위가 있다.
* 즉, 자식 컴포넌트의 템플릿에서 상위 데이터를 직접 참조할 수 없다.



#### Static Props 작성

자식 컴포넌트(About.vue)에 보낼 prop 데이터 선언

작성법

* prop-data-name="value"

**App.vue**

```vue
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- CamelCase -->
    <TheAbout my-message="CamelCase"/>
    <!-- kebab-case -->
    <the-about my-message="kebab-case"></the-about>
  </div>
</template>
```



수신 할 prop 데이터를 명시적으로 선언 후 사용

**TheAbout.vue**

```vue
<template>
  <!-- template 안에는 반드시 하나의 Element만 있어야한다. -->
  <div>
    <h1>About</h1>
    <h2> {{ myMessage }} </h2>
  </div>
</template>

<script>
export default {
  name: 'TheAbout',
  props: {
    // 넘길때에는 kebab이지만 받을때에는 camel
    myMessage: String,
  }
}
</script>
```



#### Dynamic Props 작성

v-bind directive를 사용해 부모의 데이터의 props를 동적으로 바인딩

부모에서 데이터가 업데이트 될 때마다 자식 데이터로도 전달된다.

**App.vue**

```vue
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <TheAbout :my-message="parentData"/>
    <the-about :my-message="parentData"></the-about>
  </div>
</template>

<script>
import About from './components/About.vue'
    
export default {
  name: 'App',
  components: {
    TheAbout
  },
  data: function(){
    return {
      parentData: 'This is parent data to child component'
    }
  }
}
</script>
```



마찬가지로 수신 할 prop 데이터를 명시적으로 선언 후 사용한다.

**TheAbout.vue**

```vue
<template>
  <!-- template 안에는 반드시 하나의 Element만 있어야한다. -->
  <div>
    <h1>About</h1>
    <h2> {{ myMessage }} </h2>
    <h2> {{ parentData }} </h2>
  </div>
</template>

<script>
export default {
  name: 'TheAbout',
  props: {
    myMessage: String,
    parentData: String,
  }
}
</script>
```



#### Props 이름 컨벤션

during declaration (선언 시)

**camelCase**

in template(HTML)

**kebab-case**



#### 컴포넌트의 'data'는 반드시 함수여야 한다.

기본적을 각 인스턴스는 모두 같은 data 객체를 공유하므로 새로운 data 객체를 반환(return)하여야 한다.

```vue
<script>   
export default {
  data: function () {
    return {
      myData: null,
    }
  },
}
</script>
```



#### Props시 자주하는 실수

Static 구문을 사용하여 숫자를 전달하려고 시도하는 것

실제 JavaScript 숫자를 전달하려면 값이 JavaScript 표현식으로 평가되도록 v-bind를 사용해야한다.

```vue
    <!-- 이것은 일반 문자열 "1"을 전달합니다. -->
    <comp some-prop="1"></comp>

    <!-- 이것은 실제 숫자로 전달합니다. -->
    <comp :some-prop="1"></comp>
```



#### 단방향 데이터 흐름

모든 props는 하위 속성과 상위 속성 사이의 **단방향** 바인딩을 형성한다.

부모의 속성이 변경되면 자식 속성에게 전달되지만, 반대 방향으로는 안된다.

* 자식 요소가 의도치 않게 부모 요소의 상태를 변경하여 앱의 데이터 흐름을 이해하기 어렵게 만드는 일을 방지한다.

부모 컴포넌트가 업데이트될 때마다 자식 요소의 모든 prop들이 최신 값으로 업데이트된다.



#### Emit event

"Listening to Child Components Events"



$emit(eventName)

* 현재 인스턴스에서 이벤트를 트리거
* 추가 인자는 리스너의 콜백 함수로 전달한다.



부모 컴포넌트는 자식 컴포넌트가 사용되는 템플릿에서 v-on을 사용하여 자식 컴포넌트가 보낸 이벤트를 청취 (v-on을 이용한 사용자 지정 이벤트)



#### Emit event 작성

현재 인스턴스에서 $emit 인스턴스 메서드를 사용해 child-input-change 이벤트를 트리거

**TheAbout.vue**

```vue
<template>
  <!-- template 안에는 반드시 하나의 Element만 있어야한다. -->
  <div>
    <h1>About</h1>
    <h2> {{ myMessage }} </h2>
    <h2> {{ parentData }} </h2>
    <input 
      type="text"
      @keyup.enter="childINputChange"
      v-model="childInputData" 
    >
  </div>
</template>

<script>
export default {
  name: 'TheAbout',
  data: function (){
    return {
      childInputData:''
    }
  },
  props: {
    myMessage: String,
    parentData: String,
  },
  methods: {
    childINputChange : function(){
      // 부모 컴포넌트에게 1번인자라는 이름의 이벤트를 발생
      // 2번 인자 데이터를 보냄
      this.$emit('child-input-change', this.childInputData)
    }
  }
}
</script>
```



부모 컴포넌트(App.vue)는 자식 컴포넌트(TheAbout.vue)가 사용되는 템플릿에서 v-on directive를 사용하여 자식 컴포넌트가 보낸 이벤트(child-input-change)를 청취한다.

```vue
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <the-about 
      :my-message="parentData" 
      @child-input-change="parentGetChange"
    >
    </the-about>
  </div>
</template>
<script>
import TheAbout from './components/TheAbout.vue'
export default {
  name: 'App',
  components: {
    TheAbout
  },
  data: function(){
    return {
      parentData: 'This is parent data to child component'
    }
  },
  methods: {
    parentGetChange: function(inputData){
      console.log('Boss: 들리는 군', inputData)
    }
  }
}
</script>
```



#### event 이름 컨벤션

컴포넌트 및 props와는 다르게, 이벤트는 자동 대소문자 변환을 제공하지 않는다.

HTML의 대소문자 구분을 위해 DOM 템플릿의 v-on 이벤트 리스너는 항상 자동으로 소문자 변환되기 때문에

 `v-on:myEvent` 는 자동으로 `v-on:myevent`로 변환된다.

이러한 이유로 이벤트 이름에는 **항상 kebab-case를 사용하는 것을 권장한다.**



### Vue Router

"Vue.js 공식 라우터"

라우트(route)에 컴포넌트를 매핑한 후, 어떤 주소에서 렌더링할지 알려준다.

SPA상에서 라우팅을 쉽게 개발할 수 있는 기능을 제공한다.



[참고] router

위치에 대한 최적의 경로를 지정하며, 이 경로를 따라 데이터를 다음 장치로 전향시키는 장치



#### Vue Router 시작하기

프로젝트 생성 및 이동

```bash
$ vue create my-router-app
$ cd my-router-app
```

Vue Router plugin 설치 (Vue CLI 환경)

```bash
$ vue add router
```

**[주의]**

기존 프로젝트를 진행하고 있던 도중에 추가하게 되면 App.vue를 덮어쓰므로, 프로젝트 내에서 다음 명령을 실행하기 전에 필요한 경우 파일을 백업(커밋)해야 한다.



commit 여부 (Yes)

```bash
WARN Ther are uncommitted changes in the current repository, it's recommended to commit or stash them first.
? Still proceed? Yes
```



History mode 사용 여부 (Yes)

```bash
? Use history mode for router? (Requires proper server setup for index fallback in production) Yes
```



#### Vue Router로 인한 변화

1. App.vue 코드
2. router/index.js 생성
3. views 디렉토리 생성

**App.vue**

```vue
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </nav>
    <router-view/>
```

**main.js**

```js
import router from './router'

  router,
```

**index.js**

```js
Vue.use(VueRouter)

const routes = [
  {
    path: '/',
    name: 'home',
    component: HomeView
  },
  {
    path: '/about',
    name: 'about',
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    component: () => import(/* webpackChunkName: "about" */ '../views/AboutView.vue')
  }
]
```



#### Vue Router - "index.js"

라우트에 관련된 정보 및 설정이 작성되는 곳

**index.js**

```js
Vue.use(VueRouter)

const routes = [
  {
    path: '/',
    name: 'home',
    component: HomeView
  },
  {
    path: '/about',
    name: 'about',
    component: () => import(/* webpackChunkName: "about" */ '../views/AboutView.vue')
  }
]
```



#### Vue Router - "router-link"

\<router-link>

* 사용자 네비게이션을 가능하게 하는 컴포넌트
* 목표 경로는 'to' prop으로 지정된다.
* HTML5 히스토리 모드에서 router-link는 클릭 이벤트를 차단하여 브라우저가 페이지를 다시 로드하지 않도록 한다.
* a 태그지만 우리가 알고 있는 GET 요청을 보내는 a태그와 조금 다르게, 기본 GET 요청을 보내는 이벤트를 제거한 형태로 구성된다.

```vue
      <router-link :to="{ name: 'home' }">Home</router-link> |
      <router-link :to="{ name: 'about' }">About</router-link>
```



#### Vue Router - "router-view"

\<router-view>

* 주어진 라우트에 대해 일치하는 컴포넌트를 렌더링하는 컴포넌트
* 실제 component가 DOM에 부착되어 보이는 자리를 의미한다.
* router-link를 클릭하면 해당 경로와 연결되어 있는 index.js에 정의한 컴포넌트가 위치한다.



#### History mode

HTML History API를 사용해서 router를 구현한 것

브라우저의 히스토리는 남기지만 실제 페이지는 이동하지 않는 기능을 지원한다.

즉, 페이지를 다시 로드하지 않고 URL을 탐색할 수 있다.

* SPA의 단점 중 하나인 "URL이 변경되지 않는다."를 해결



#### [참고] History API

DOM의 Window 객체는 history 객체를 통해 브라우저의 세션 기록에 접근할 수 있는 방법을 제공한다.

history 객체는 사용자를 자신의 방문 기록 앞과 뒤로 보내거나, 기록의 특정 지점으로 이동하는 등 유용한 메서드와 속성을 가진다.



#### 1. Named Routes

이름을 가지는 라우트

명명된 경로로 이동하려면 객체를 vue-router 컴포넌트 요소의 prop에 전달한다.

**index.js**

```js
const routes = [
  {
    path: '/',
    name: 'home',
    component: HomeView
  },
  {
    path: '/about',
    name: 'about',
  }
]
```

```vue
<template>
  <div id="app">
    <nav>
      <router-link :to="{ name: 'home' }">Home</router-link> |
      <router-link :to="{ name: 'about' }">About</router-link>
    </nav>
    <router-view/>
  </div>
</template>
```



#### 2. 프로그래밍 방식 네비게이션

\<router-link>를 사용하여 선언적 탐색을 위한 a 태그를 만드는 것 외에도, router의 인스턴스 메서드를 사용하여 프로그래밍 방식으로 같은 작업을 수행할 수 있다.

| 선언적 방식             | 프로그래밍 방식   |
| ----------------------- | ----------------- |
| \<router-link to="..."> | $router.push(...) |



Vue 인스턴스 내부에서 라우터 인스턴스에  **$router**로 접근할 수 있다.

따라서 다른 URL로 이동하려면 **this.<u>$router</u>.push**를 호출할 수 있다.

* 이 메서드는 새로운 항목을 히스토리 스택에 넣기 때문에 사용자가 브라우저의 뒤로가기 버튼을 클릭하면 URL로 이동하게 된다.

\<router-link>를 클릭할 때 내부적으로 호출되는 메서드이므로 \<router-link :to="...">를 클릭하면, **routher.push(...)**를 호출하는 것과 같다.



작성할 수 있는 인자 예시

```js
// literal string path
router.push('home')

// object
router.push({ path: 'home' })

// named route
router.push({ path: 'user', params: { userId: '123' } })

// with query, resulting in /register?plan=private
router.push({ path: 'register', query: { plan: 'private'} })
```



About에서 Home으로 이동하는 로직 작성

```vue
<template>
  <div class="about">
    <h1>This is an about page</h1>
    <button @click="moveToHome">To Home</button>
  </div>
</template>

<script>
export default {
  name: 'AboutView',
  methods: {
    moveToHome(){
      // this.$router.push('/')
      this.$router.push({ name: 'home' })
    }
  }
}
</script>

<style>

</style>
```



#### 3. Dynamic Router Matching

동적 인자 전달

주어진 패턴을 가진 라우트를 동일한 컴포넌트에 매핑해야하는 경우

예를 들어 모든 User에 대해 동일한 레이아웃을 가지지만, 다른 User ID로 렌더링 되어야하는 User 컴포넌트 예시

```js
const routes = [
  {
    path: '/user/:userId',
    name: 'User',
    componenet: User
  }
]
```



동적 인자는 : (콜론)으로 시작

컴포넌트에서 **this.<u>$route</u>.params**로 사용가능하다.

| pattern                            | matched path          | $route.params                            |
| ---------------------------------- | --------------------- | ---------------------------------------- |
| /user/:userName                    | /user/john            | { username: 'john'}                      |
| /user/:userName/article/:articleId | /user/john/article/12 | { username: 'john',<br />articleId: 12 } |

