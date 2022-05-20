# Vue 05

## Vue Router

**사전 준비사항: 서버가 있다는 가정하에 서버와 통신하는 것이기 때문에 0516-django_back 폴더를 runserver 시켜주어야한다. **

0518-vue-front 폴더를 활용

 

0516-django_back 서버와 Client가 통신하는 구조를 만드는 것이기 때문이다.

**서버가 없으면 클라이언트는 동작하지 않는다.**



0518-vue-front 에서 code로 열기로 VS code로 열고 `npm run serve`하면 실행되지 않는다.

package.json, package-lock.json에 사용할 라이브러리는 다 있다.

``` bash
$ npm install
```

:heavy_check_mark: api폴더는 생성한 폴더이다. api폴더 안에 drf.js파일이 있다.



### POSTMAN

이 때 사용하는 url은 django에 urls.py에 작성되어있는 것이다.

`http://127.0.0.1:8000/api/v1/articles/`

**Body, raw, JSON**

```json
{
    "title": "HEllo",
    "content": "World"
}
```

**Headers**

KEY: Authorization

VALUE: Token Token_value



이렇게 작성하던 부분을 ArticleNewView.vue에서 버튼을 눌러서 url로 POST방식으로 보내게 할 것이다.

Headers와 Body의 내용을 포함해서보낸다.



### Skelecton

#### api/drf.js

미리 url을 만들어 주는 부분

```js
const HOST = 'http://localhost:8000/api/v1/'

const ACCOUNTS = 'accounts/'
const ARTICLES = 'articles/'
const COMMENTS = 'comments/'

export default {
  accounts: {
    login: () => HOST + ACCOUNTS + 'login/',
    logout: () => HOST + ACCOUNTS + 'logout/',
    signup: () => HOST + ACCOUNTS + 'signup/',
    // Token 으로 현재 user 판단
    currentUserInfo: () => HOST + ACCOUNTS + 'user/',
    // username으로 프로필 제공
    profile: username => HOST + ACCOUNTS + 'profile/' + username,
  },
  articles: {
    articles: () => HOST + ARTICLES,
    article: articlePk => HOST + ARTICLES + `${articlePk}/`,
    likeArticle: articlePk => HOST + ARTICLES + `${articlePk}/` + 'like/',
    comments: articlePk => HOST + ARTICLES + `${articlePk}/` + COMMENTS,
    comment: (articlePk, commentPk) =>
      HOST + ARTICLES + `${articlePk}/` + COMMENTS + `${commentPk}/`,
  },
}
```

사용 방법

```
drf.accounts.login()
// 'http://localhost:8000/api/v1/accounts/login/'
```



#### LoginViewe.vue

```vue
<template>
  <div>
    <h1>Login</h1>

    <form>
      <div>
        <label for="username">username: </label>
        <input type="text" id="username" required />
      </div>

      <div>
        <label for="password">password: </label>
        <input type="password" id="password" required />
      </div>

      <button>Login</button>
    </form>
  </div>
</template>

<script>
  // import { mapActions, mapGetters } from 'vuex'

  export default {
    name: 'LoginView',
    computed: {},
    methods: {},
  }
</script>
```



#### router/index.js

```js
import Vue from 'vue'
import VueRouter from 'vue-router'
import store from '../store'

import ArticleListView from '@/views/ArticleListView.vue'
import ArticleDetailView from '@/views/ArticleDetailView.vue'
import ArticleNewView from '@/views/ArticleNewView'
import ArticleEditView from '@/views/ArticleEditView'

import LoginView from '@/views/LoginView.vue'
import LogoutView from '@/views/LogoutView.vue'
import SignupView from '@/views/SignupView.vue'
import ProfileView from '@/views/ProfileView.vue'
import NotFound404 from '../views/NotFound404.vue'

Vue.use(VueRouter)

const routes = [
  /*
  accounts
    /login => LoginView
    /logout => LogoutView
    /signup => SignupView
    /profile/:username => ProfileView
  
  articles
    / => ArticleListView
    /articles/new => ArticleNewView
    /articles/:articlePk => ArticleDetailView
    /articles/:articlePk/edit => ArticleEditView
    /404 => NotFound404
    * => /404
  */
]

export default router
```

**Componets**

부품으로 사용되는 vue파일들

**Views**

url과 매핑되는 vue파일들

```js
import Vue from 'vue'
import VueRouter from 'vue-router'
import store from '../store'

import ArticleListView from '@/views/ArticleListView.vue'
import ArticleDetailView from '@/views/ArticleDetailView.vue'
import ArticleNewView from '@/views/ArticleNewView'
import ArticleEditView from '@/views/ArticleEditView'

import LoginView from '@/views/LoginView.vue'
import LogoutView from '@/views/LogoutView.vue'
import SignupView from '@/views/SignupView.vue'
import ProfileView from '@/views/ProfileView.vue'
import NotFound404 from '../views/NotFound404.vue'

const routes = [
  {
    path: '/login',
    name: 'login',
    component: LoginView
  },
  {
    path: '/logout',
    name: 'logout',
    component: LogoutView
  },
  {
    path: '/signup',
    name: 'signup',
    component: SignupView
  },
  {
    path: '/profile/:username',  // /profile/neo
    name: 'profile',
    component: ProfileView,
  },
  {
    path: '/',  // Home
    name: 'articles',
    component: ArticleListView
  },
  {
    path: '/articles/new',
    name: 'articleNew',
    component: ArticleNewView
  },
  {
    path: '/articles/:articlePk',
    name: 'article',
    component: ArticleDetailView
  },
  {
    path: '/articles/:articlePk/edit',
    name: 'articleEdit',
    component: ArticleEditView
  },
  {
    path: '/404',
    name: 'NotFound404',
    component: NotFound404
  },
  {
    path: '*',
    redirect: '/404'
  },
  
]
```



## 404 page

#### views/NotFound404.vue

```vue
<template>
  <div>
    <!-- <img class="not-found" src="@/assets/404.jpg" alt="not-found"> -->
    <h1>404 Not Found</h1>
  </div>
</template>

<script>
  export default {
    name: 'NotFound404',
  }
</script>

<style>
  img.not-found {
    width: 100%;
  }
</style>
```



#### router/index.js

```js
const routes = [
  {
    path: '/404',
    name: 'NotFound404',
    component: NotFound404
  }, 
]
```



### 404 Not Found 시나리오

1 Vue Router에 등록되지 않는 routes일 경우

예) /no-such-routes

2 Vue Router에는 등록되어 있지만, 서버에서 해당 리소스를 찾을 수 없는 경우

예) /articles/987654321



### Vue Router에 등록되지 않는 routes

vue router는 routes 배열에서 순차적으로 URL을 검색한다.

등록되지 않은 모든(*) URL은 /404로 redirection한다.

브라우저에서 NotFound404 컴포넌트를 확인한다.

#### router/index.js

```js
const routes = [
  {
    path: '/404',
    name: 'NotFound404',
    component: NotFound404
  },
  {
    path: '*',
    redirect: '/404'
  },
]
```



### 서버에서 해당 리소스를 찾을 수 없는 경우

#### Vuex

```js
import router from '@/router'
axios({
    url: drf.articles.article(articlePk),
    method: 'get',
    headers: getters.authHeader,
    })
    .then(res => {})
    .catch(err => {
        console.error(err.response)
        if (err.response.status === 404) {
        router.push({ name: 'NotFound404' })
        }
    })
```



## Navigation Guards

### 전역 가드(Global Before Guards)

1 URL을 이동할 때마다, 이동하기 전 모든 경우에 발생

2 rounter 객체의 메서드로, 콜백 함수를 인자로 받고 해당 콜백 함수는 3개의 인자를 받는다.

1. to: 이동하려는 route의 정보를 담은 객체
2. from: 직전 route의 정보를 담은 객체
3. next: 실제 route의 이동을 조작하는 함수

3 반드시 마지막에 next()로 route 이동을 실행해야 한다.

```js
const routes = [ ... ]

const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes,
})

router.beforeEach((to, from, next) => {
	...
})

export default router
```



예시

```js
/*
Navigation Guard 설정
  (이전 페이지에서 있던 에러 메시지 삭제)

  로그인(Authentication)이 필요 없는 route 이름들 저장(/login, /signup)

  0. router 에서 이동 감지

  1. 현재 이동하고자 하는 페이지가 로그인이 필요한지 확인
  
  2. 로그인이 필요한 페이지인데 로그인이 되어있지 않다면
    로그인 페이지(/login)로 이동

  3. 로그인이 되어 있다면
    원래 이동할 곳으로 이동
  
  4. 로그인이 되어있는데 /login, /signup 페이지로 이동한다면
    메인 페이지(/)로 이동
*/
```

#### @/router/index.js

```js
const routes = [
  // 인증 필요 없음
  {
    path: '/login',
    name: 'login',
    component: LoginView
  },
  {
    path: '/signup',
    name: 'signup',
    component: SignupView
  },
  // 인증 필요
  {
    path: '/articles/new',
    name: 'articleNew',
    component: ArticleNewView
  },
  {
    path: '/articles/:articlePk/edit',
    name: 'articleEdit',
    component: ArticleEditView
  },
]
```

```js
router.beforeEach((to, from, next) => {
  // 로그인 여부 확인 (Vuex 사용 시)
  const { isLoggedIn } = store.getters
  
  // Auth가 필요한 route의 name
  const noAuthPages = ['articleNew', 'articleEdit']
  
  // 현재 이동하고자 하는 페이지가 Auth가 필요한가?
  const isAuthRequired = authoPages.includes(to.name)

  // Auth가 필요한데, 로그인되어 있지 않다면?
  if (isAuthRequired && !isLoggedIn) {
    alert('Require Login. Redirecting..')
    // 로그인 페이지로 이동
    next({ name: 'login' })
  } else {
    // 원래 이동하려던 곳으로 이동
    next()
  }
})
```

**콜백 함수의 to 객체 구성**

![image-20220520134206498](Vue_07.assets/image-20220520134206498.png)



## Vuex Module

### Module 분리

![image-20220520134612366](Vue_07.assets/image-20220520134612366.png)

1 단일 파일(@/store/index.js)에 모든 state, getters, mutations, actions를 작성할 경우, App이 커질수록 파일의 크기가 너무 커진다.

2 기능에 따라 state, getters, mutations, actions를 모듈(파일)로 분리하여 사용한다.

![image (1)](Vue_07.assets/image%20(1).png)

![image (2)](Vue_07.assets/image%20(2).png)



### Module의 이름공간(module space)

![image (3)](Vue_07.assets/image%20(3).png)

![image (4)](Vue_07.assets/image%20(4).png)

1 다른 module에 작성되어 있어도, 실제로는 global namespace에 등록된다.

2 만약 확실하게 모듈별로 구분하고 싶다면, namespaced: true 옵션을 사용한다.



## Vuex - Component 구성

### accounts Login

#### views/LoginView.vue

```vue
```



#### store/modules/accounts.js

```js
import router from '@/router'
import axios from 'axios'
import drf from '@/api/drf'

export default {
  // 생각해서 작성해야하는 부분
  state: {
    token: '',
    currentUser: {},
    profile: {},
    authError: null,
  },

  getters: {},

  mutations: {
    여기 작성
  },

  actions: {
    saveToken({ commit }, token) {
      /* 
      state.token 추가 
      localStorage에 token 추가
      */
    },

    removeToken({ commit }) {
      /* 
      state.token 삭제
      localStorage에 token 추가
      */
    },

    login({ commit, dispatch }, credentials) {
      /* 
      POST: 사용자 입력정보를 login URL로 보내기
        성공하면
          응답 토큰 저장
          현재 사용자 정보 받기
          메인 페이지(ArticleListView)로 이동
        실패하면
          에러 메시지 표시
      */
    },

    signup({ commit, dispatch }, credentials) {
      /* 
      POST: 사용자 입력정보를 signup URL로 보내기
        성공하면
          응답 토큰 저장
          현재 사용자 정보 받기
          메인 페이지(ArticleListView)로 이동
        실패하면
          에러 메시지 표시
      */
    },

    logout({ getters, dispatch }) {
      /* 
      POST: token을 logout URL로 보내기
        성공하면
          토큰 삭제
          사용자 알람
          LoginView로 이동
        실패하면
          에러 메시지 표시
      */
    },

    fetchCurrentUser({ commit, getters, dispatch }) {
      /*
      GET: 사용자가 로그인 했다면(토큰이 있다면)
        currentUserInfo URL로 요청보내기
          성공하면
            state.cuurentUser에 저장
          실패하면(토큰이 잘못되었다면)
            기존 토큰 삭제
            LoginView로 이동
      */
    },

    fetchProfile({ commit, getters }, { username }) {
      /*
      GET: profile URL로 요청보내기
        성공하면
          state.profile에 저장
      */
    },
  },
}
```

