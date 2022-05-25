## Practical Procedure

```bash
$ vue create drf_vue_client
$ cd drf_vue_client
$ vue add axios
$ vue add router
$ npm run serve
```

:heavy_check_mark: 서버 완성



:balloon: 구조

articles-> 볼수 있고 만들 수 있다
accounts -> login, logout, signup



### Article

article부터 만들기 시작
**ArticleView.vue**를 만들고, **App.vue**에 router-link를 **index.js**에 routes에 추가해준다.
**ArticleView.vue**
article을 보여주고 싶다.
state에 정보가 들어가 있어 그 정보를 가져와서 보여줄 수 있어야 한다.
django server에서 가져와야한다.
무언가를 가져와야할 때,
함수(or event) 발생 > axios요청의 actions에서 보낼 것이다. > data가 오고 이 데이터를 mutations에서 state 저장
state에 저장된 것을 vue파일에서 사용할 것이다.

### 0 [Client] views/ArticleView.vue

```vue
<script>
export default {
  name: 'ArticleView',
  methods:{
    getArticle(){
      // django에서 article을 가져오기
      // actions 불러오기
      this.$store.dispatch('getArticle')
    }
  },
}
</script>
```



### 1 [Client] src/store/index.js

axios 요청을 보내는 getArticle을 actions에 추가

```js
import axios from 'axios'

  actions: {
    getArticle({commit, state}){
      // axios 요청을 보낼 것이다.
      axios({
        method: 'get',
        // django server
        url : 'http://127.0.0.1:8000/api/v1/articles/',
      })
        .then(res => {
          console.log(res)
        })
    },
  },
```



#### [Server]의 상태

##### [Server] articles/urls.py

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.article_list_or_create),
]
```

##### [Server] articles/views.py

```python
from django.shortcuts import get_list_or_404
from rest_framework import status
from rest_framework.decorators import api_view
from rest_framework.response import Response
from .models import Article
from .serializers.article import ArticleListSerializer, ArticleSerializer


@api_view(['GET', 'POST'])
def article_list_or_create(request):

    def article_list():
        # comment 개수 추가
        articles = get_list_or_404(Article)
        serializer = ArticleListSerializer(articles, many=True)
        return Response(serializer.data)
    
    def create_article(request):
        serializer = ArticleSerializer(data=request.data)
        if serializer.is_valid(raise_exception=True):
            serializer.save(user=request.user)
            return Response(serializer.data, status=status.HTTP_201_CREATED)

    if request.method == 'GET':
        return article_list()
    elif request.method == 'POST':
        return create_article(request)
```



### 2 [Client] views/ArticleView.vue

created를 활용하여 실행

```vue
<script>
export default {
  name: 'ArticleView',
  methods:{
    getArticle(){
      
      this.$store.dispatch('getArticle')
    }
  },
  created(){
    this.getArticle()
  },
}
</script>
```



### 3 [Server] settings.py

:x:서버를 켜면 CORS policy 오류가 뜰 것이다.

:heavy_check_mark: 당장은 모두 True로 받는다.

```python
INSTALLED_APPS = [
    'corsheaders',
]

MIDDLEWARE = [
    # CORS
    # CommonMiddleware보다 위에 위치
    'corsheaders.middleware.CorsMiddleware',
]

CORS_ALLOW_ALL_ORIGINS = True
```

추가해주면 CORS가 성공적이고 data가 들어온다.



### 4 [Client] src/store/index.js

res의 data에는 articles가 들어있다.

articles를 state에 저장하고 싶다.

```js
import axios from 'axios'

  actions: {
    getArticle({commit}){
      // axios 요청을 보낼 것이다.
      axios({
        method: 'get',
        // django server
        url : 'http://127.0.0.1:8000/api/v1/articles/',
      })
        .then(res => {
          const articles = res.data
          commit('GET_ARTICLE', articles)
        })
    },
  },
```



### 5 [Client] src/store/index.js

mutations에 GET_ARTICLE()추가

```js
import axios from 'axios'

export default new Vuex.Store({
  state: {
    articles: [],
  },
  mutations: {
    GET_ARTICLE(state, articles){
      state.articles = articles
    },
  },
  actions: {
    getArticle({commit}){
      // axios 요청을 보낼 것이다.
      axios({
        method: 'get',
        // django server
        url : 'http://127.0.0.1:8000/api/v1/articles/',
      })
        .then(res => {
          const articles = res.data
          commit('GET_ARTICLE', articles)
        })
    },
  },
})
```



### 6 [Client] views/ArticleView.vue

state의 값을 computed를 통해 받아와서 사용한다.

```vue
<template>
  <div>
    <h1>articles</h1>
    <li 
      v-for="article in articles"
      :key="article.pk"
      >
      {{ article.title }}
    </li> 
  </div>
</template>

<script>
export default {
  name: 'ArticleView',
  computed:{
    articles(){
      return this.$store.state.articles
    }
  }
}
</script>
```



### Accounts

settings.py에서 `'rest_framework.permissions.IsAuthenticated'`이 되어야한다.

```python
# drf 설정
REST_FRAMEWORK = {
    # 기본 인증을 기본 Token 으로 설정
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.TokenAuthentication',
    ],
    # 인증받은 사용자에게만 요청 허용
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.AllowAny',       # => 기본적으로 모두에게 허용
        # 'rest_framework.permissions.IsAuthenticated',  # => 기본적으로 인증받아야 사용
    ],
}
```

:x:현재 상태 대로 `'rest_framework.permissions.AllowAny'`를 `'rest_framework.permissions.IsAuthenticated'`로 바꾸고 실행 시 **Unauthorized**오류가 뜨게 된다. (401)



🎯 여기서부터는 `'rest_framework.permissions.IsAuthenticated'`로 바꾼 상태로 진행

### Signup

### 0 [Client] views/SignupView.vue

```vue
<template>
  <div>
    <h1>signup</h1>
  </div>
</template>

<script>
export default {
  name: 'SignupView',
</script>
```



### 1 [Client] router/index.js

router에 등록

```js
import Vue from 'vue'
import VueRouter from 'vue-router'
import SignupView from '../views/SignupView.vue'

const routes = [
  {
    path: '/signup',
    name: 'signup',
    component: SignupView,
  },
]
```



### 2 [Client] App.vue

```vue
<template>
  <div id="app">
    <nav>
      <router-link to="/signup">Signup</router-link> |
    </nav>
    <router-view/>
  </div>
</template>

```



### 3 [Client] views/SignupView.vue

회원가입을 위해 필요한 data는 django에서 받아야한다. (username, password1, password2)

django에서 rest_framework의 것을 사용했었다.

:heavy_check_mark: POSTMAN에서 확인한다.

api/v1/accounts/signup/ 을 POST로 보내면 username, password1, password2이 필요하다는 정보가 응답된다.

1 data에 username, password1, password2를 추가한다.

2 template안에 label와 input를 생성하고 이를 v-model로 연결해준다.

3 button을 생성

4 form에서 event를 받는다. `<form @submit.prevent="signup">`

* form의 default기능을 사용하지 않기 위해 prevent추가한다.

5 methods로 signup함수에서 data를 담아서 axios요청(signup)을 보낸다.

6 값을 `credentials`로 묶어서 보내주며 v-model도 `v-model="credentials.username"`로 작성한다.

7 password입력 시 보여주지 않기 위해서 `<input type="password" v-model="credentials.password2">`

8 `this.$store.dispatch('signup', this.credentials)`

```vue
<template>
  <div>
    <h1>signup</h1>
    <form @submit.prevent="signup">
      <div>
        <label for="username">username</label>
        <input type="text" v-model="credentials.username" id="username">
      </div>
      <div>
        <label for="password1">password1</label>
        <input type="password" v-model="credentials.password1" id="password1">
      </div>
      <div>
        <label for="password2">password2</label>
        <input type="password" v-model="credentials.password2" id="password2">
      </div>
      <button>회원가입</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'SignupView',
  data(){
    return {
      credentials:{
        username : '',
        password1 : '',
        password2 : '',
      }
    }
  },
  methods:{
    signup(){
      this.$store.dispatch('signup', this.credentials)
    }
  }
}
</script>
```



### 4 [Client] src/store/index.js

actions에 signup을 추가한다.

```js
import axios from 'axios'

  actions: {
    signup({commit}, credentials){
      axios({
        method: 'post',
        url : 'http://127.0.0.1:8000/api/v1/accounts/signup/',
      })
        .then(res => {
          console.log(res)
        })
    }
  },
```

:x: 400 Bad Request가 된다. data가 들어있지 않다.

```js
import axios from 'axios'

  actions: {
    signup({commit}, credentials){
      axios({
        method: 'post',
        url : 'http://127.0.0.1:8000/api/v1/accounts/signup/',
        data : credentials,
      })
        .then(res => {
          console.log(res)
        })
    }
  },
```

:heavy_check_mark: Created되었고, data의 key값이 생성된다. 이 key값을 header에 담아서 요청을 보내야한다.

token을 추가한다.

`token : null`

`const token = res.data.key`

```js
import axios from 'axios'
  state: {
    articles: [],
    token : null,
  },
  actions: {
    signup({commit}, credentials){
      axios({
        method: 'post',
        url : 'http://127.0.0.1:8000/api/v1/accounts/signup/',
        data : credentials,
      })
        .then(res => {
          console.log(res)
          const token = res.data.key
        })
    }
  },
```



### 5 [Client] src/store/index.js

Token의 state에 저장

actions에 `commit('SET_TOKEN',token)` 추가

mutations에 `SET_TOKEN(state, token){ state.token = token }` 추가

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

import axios from 'axios'
import router from '@/router'

export default new Vuex.Store({
  state: {
    articles: [],
    token : null,
  },
  getters: {
  },
  mutations: {
    GET_ARTICLE(state, articles){
      state.articles = articles
    },
    SET_TOKEN(state, token){
      state.token = token
    }
  },
  actions: {
    signup({commit}, credentials){
      axios({
        method: 'post',
        url : 'http://127.0.0.1:8000/api/v1/accounts/signup/',
        data : credentials,
      })
        .then(res => {
          console.log(res)
          const token = res.data.key
          commit('SET_TOKEN',token)
        })
    }
  },
  modules: {
  }
})

```

:x: 401 Unauthorized 오류 발생! header에 Token 넣어주어야한다.

actions에 `headers : { Authorization : ``Token ${state.token}``}`을 추가한다.

getArticle에는 state가 없다. 따라서 state추가 `getArticle({commit, state})`

:heavy_check_mark: axios를 보낼 때 header에 Token을 담아서 보낼 것이다.

:heavy_check_mark: signup하고 router로 이동하고 싶다. `router.push({name: 'articles'})`

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

import axios from 'axios'
import router from '@/router'

export default new Vuex.Store({
  state: {
    articles: [],
    token : null,
  },
  getters: {
  },
  mutations: {
    GET_ARTICLE(state, articles){
      state.articles = articles
    },
    SET_TOKEN(state, token){
      state.token = token
    }
  },
  actions: {
    getArticle({commit, state}){
      axios({
        method: 'get',
        url : 'http://127.0.0.1:8000/api/v1/articles/',
        headers : { Authorization : `Token ${state.token}`}
      })
        .then(res => {
          const articles = res.data
          commit('GET_ARTICLE', articles)
        })
    },
    signup({commit}, credentials){
      axios({
        method: 'post',
        url : 'http://127.0.0.1:8000/api/v1/accounts/signup/',
        data : credentials,
      })
        .then(res => {
          console.log(res)
          const token = res.data.key
          commit('SET_TOKEN',token)
          router.push({name: 'articles'})
        })
    }
  },
  modules: {
  }
})
```

:x:  새로고침하면 Vuex는 새로 실행히 되어 Token이 들어간다.

:heavy_check_mark: Token을 localstorage에 담아줄 것이다.
