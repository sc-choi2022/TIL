## Skeleton (FE)

:heavy_check_mark: 프로젝트 구동

```bash
npm run serve
```



정상적으로 Webpack dev 서버가 실행되면 localhost:8083에서 Front-end 프로젝트의 동작을 확인할 수 있다.

[.../api/v1] 으로 시작되는 URL은 localhost:8080으로 Proxy 처리되므로, Back-end API로의 호출을 확인하려면 Back-end 프로젝트가 실행되어 있어야한다.



:heavy_check_mark:프론트엔드 빌드

```bash
npm run build
```

프로젝트 빌드 수행이 정상적으로 완료되었다면, 번들링 된 산출물 생성

생성 경로 /backend/main/resources/dist



:heavy_check_mark:통합 빌드 및 실행

Front-end 프로젝트와 Back-end 프로젝트 전체를 통합 빌드

/backend 경로에서 `gradlew clean build`실행

:x:



## 기존 Vue2 코드와의 차이점

:heavy_check_mark: 폴더 구조

**Vue 2**

src > components, views, router, store..



**Vue 3**

src > views > conferences, history, home, main

main > componenets, store, css...



:heavy_check_mark: Fragments

**Vue 3**

다중 루트 노드(multi-root nodes) 컴포넌트인 fragments 제공

:arrow_forward:template 정의에 단일 루트 요소 강제 X

* 최상단 <div>사용이 강제되지 않는다.



:heavy_check_mark: Composition API

코드의 재사용성과 가독성 높아졌다.

**Vue 2**

Props, data, method을 같은 Depth에서 선언

data을 Object로 선언



**Vue 3**

data, methods 선언에는 Composition API의 setup()을 사용한다.

data은 함수로 선언



### setup()

**ref 를 사용**

* 반응형 변수로 data을 대체
* 보통의 자바스크립트 함수로 methods을 대체

**Lifecycle Method**

* onMounted, onUpdated 같은 라이프사이클 훅 함수가 대신한다. 

반응형 변수의 변경 탐지: watch 함수로 구현 가능 

계산된 값을 위한 computed 함수도 제공 

Component 객체에서 속성으로 분리되었던 기능 대부분이 setup 함수 내에서 사용 가능

**:heavy_check_mark: 중요한 차이점**

setup 함수는 Component 인스턴스가 생성되기 전에 실행된다.

따라서 Component 인스턴스에 접근이 필요한 기능은 사용할 수 없다.

* setup 안에서 this을 통해 Component 객체의 data, computed, methods에서 선언한 것들에 접근이 불가능
* created 메소드에 matching되는 Life cycle Hook 존재하지 않는다.



:heavy_check_mark:Lifecycle Hooks

Vue 3 Composition API에서는 접두어 "on"을 추가하여 Component의 Life cycle Hooks에 접근 할 수 있다.

| Option API      | setup 내부의 Hook |
| --------------- | ----------------- |
| beforeCreate    | 필요하지 않다.    |
| created         | 필요하지 않다.    |
| beforeMount     | onBeforeMount     |
| mounted         | onMounted         |
| beforeUpdate    | onBeforeUpdate    |
| updated         | onUpdated         |
| beforeUnmount   | onBeforeUnmount   |
| unmounted       | onUnmounted       |
| errorCaptured   | onErrorCaptured   |
| renderTracked   | onRenderTracked   |
| renderTriggered | onRenderTriggered |



:heavy_check_mark:Props & Emits

props 인자와 emit 인자의 선언 및 사용 방법에 차이가 있다.

**Vue 2**

this를 통해 props와 emit에 접근

```vue
props: ['initialCounter'],
data: function (){
	return {
		counter: this.initialCounter
	}
}
```

```vue
_show(){
	this.$emit('update:title', newTitle)
}
```



**Vue 3**

props와 emit을 Composition API의 setup()에서 전달인자로 명시

```vue
export default {
	props: {
		title: String
	},
	setup(props){
		console.log(props.title)
	}
}

export default {
	setup(props, {emit}){
	}
}
```



:ballot_box_with_check:Vue3는 Vue 2와 비교하여 Component Life Cycle에도 변화가 있다.

:x: 상세한 비교

Vue 3을 기준으로 학습과 프로젝트 진행하고, 필요에 따라 차이점이나 변경점 참고



:cactus:

store/state.js

```js
// ROOT STATE 변수 정의 및 기본값 대입
const menuData = require('@/views/main/menu.json')

/**
 * 플랫폼 관련 정보로 데스크탑인지, 모바일인지 판별 - 하이브리드 앱 대비
 */
function getIsDesktop() {
  var userAgent = window.navigator.userAgent,
      platform = window.navigator.platform,
      macosPlatforms = ['Macintosh', 'MacIntel', 'MacPPC', 'Mac68K'],
      windowsPlatforms = ['Win32', 'Win64', 'Windows', 'WinCE'],
      iosPlatforms = ['iPhone', 'iPad', 'iPod'],
      os = null;

  if (macosPlatforms.indexOf(platform) !== -1) { //Desktop - Mac
    return true
  } else if (iosPlatforms.indexOf(platform) !== -1) { // IOS
    return false
  } else if (windowsPlatforms.indexOf(platform) !== -1) { //Desktop - window
    return true
  } else if (/Android/.test(userAgent)) { //Android
    return false
  } else if (!os && /Linux/.test(platform)) { //Linux
    return true
  }

  return os;
}

const IsDesktop = getIsDesktop()

export default {
  isDesktopPlatform: IsDesktop,
  activeMenu: 'home',
  menus: menuData
}
```

