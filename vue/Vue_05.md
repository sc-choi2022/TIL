# Vue 03

## Vue Todo App

### 1. Set project & components

Create Project

```bash
$ vue create todo-vuex-app
$ cd todo-vuex-app
$ code .
```

Add Vuex plugin in Vue CLI

```bash
$ vue add vuex
```

commit 여부 (Yes)

```bash
WARN There are uncommitted changes in the cuurent repository, it's recommended to commit or stash them first.
? Still proceed? Yes
```



#### Vuex로 인한 변화

1 store 디렉토리 생성

2 index.js 생성

**index.js**

* Vuex core concepts가 작성되는 곳



#### 컴포넌트 작성

##### components/TodoListItem.vue

* 개별 todo 컴포넌트
* TodoList 컴포넌트의 자식 컴포넌트

```vue
<template>
  <div>Todo</div>
</template>

<script>
export default {
  name: 'TodoListItem'
}
</script>
```



##### components/TodoList.vue

* todo 목록 컴포넌트
* TodoListItem 컴포넌트의 부모 컴포넌트

```vue
<template>
  <div>
    <todo-list-item></todo-list-item>
  </div>
</template>

<script>
import TodoListItem from '@/componets/TodoListItem.vue'
export default {
  name: 'TodoList',
  components: {
    TodoListItem,
  }
}
</script>
```



##### components/TodoForm.vue

* todo 데이터를 입력 받는 컴포넌트

```vue
<template>
  <div>Todo Form</div>
</template>

<script>
export default {
  name: 'TodoForm',
}
</script>
```



##### App.vue

* 최상위 컴포넌트
* TodoList, TodoForm 컴포넌트의 부모 컴포넌트

```vue
<template>
  <div id="app">
    <h1>MY TODOS</h1>
    <todo-list></todo-list>
    <todo-form></todo-form>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList.vue'
import TodoForm from '@/components/TodoForm.vue'
export default {
  name: 'App',
  components: {
    TodoList,
    TodoForm,
  }
}
</script>
```



### 2. Create Todo

#### State 작성

state에 2개의 todo 작성

[주의]

* Vuex를 사용한다고 해서 Vuex Store에 모든 상태를 넣어야하는 것은 아니다.

##### src/store/index.js

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {      // data
  },
  getters: {    // computed
  },
  mutations: {  // methods => change!
  },
  actions: {    // methods => !change
  },
  modules: {
  }
})
```

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {      // data
    todos: [
      { title: 'Lunch', isCompleted: false, data: new Date().getTime },
      { title: 'Vuex', isCompleted: false, data: new Date().getTime + 1 },
    ]
  },
})
```



#### TodoList 데이터 가져오기

컴포넌트에서 Vuex Store의 state에 접근한다.

* $store.state

##### TodoList.vue

```vue
<template>
  <div>
    <todo-list-item
     v-for="todo in $store.state.todos"
     :key="todo.date"
    ></todo-list-item>
  </div>
</template>
```



#### Computed로 변경

현재 state의 todo는 값이 변화하는 것이 아니다.

store에 저장된 todo 목록을 가져오는 것이기 때문에 매번 새로 호출하는 것은 비효율적이다.

대신 todo가 추가되는 등의 변경 사항이 있을 때만 새로 계산한 값을 반환하는 방향으로 변경한다.(computed)

this(Vue Instance)로 접근한다.

`<todo-list-item v-for="todo in todos" :key="todo.date"></todo-list-item>`

`computed:{ todos(){ return this.$store.state.todos }}`

```vue
<template>
  <div>
    <todo-list-item
     v-for="todo in todos"
     :key="todo.date"
    ></todo-list-item>
  </div>
</template>

<script>
import TodoListItem from '@/components/TodoListItem.vue'
export default {
  name: 'TodoList',
  components: {
    TodoListItem,
  },
  computed:{
    todos(){
      return this.$store.state.todos
    }
  }
}
</script>
```



#### Pass Props (TodoList -> Todo)

##### TodoList.vue

`:todo="todo"`

```vue
<template>
  <div>
    <todo-list-item
     v-for="todo in todos"
     :key="todo.date"
    ></todo-list-item>
  </div>
</template>
```



##### TodoListItem.vue

`{{ todo.title }}`

`props: { todo: { type: Object } }`

```vue
<template>
  <div>
    <h1>Todo</h1>
    {{ todo.title }}
  </div>
</template>

<script>
export default {
  name: 'TodoListItem',
  props: {
    todo: {
      type: Object
    }
  }
}
</script>
```



#### Actions & Mutations

createTodo 메서드를 통해 createTodo Action 함수 호출 (dispatch())

##### TodoForm.vue

`v-model.trim="todoTitle"`

`if (todoItem.title){ this.$store.dispatch('createTodo', todoItem) }`

`this.todoTitle = ''`

```vue
<template>
  <div>
    <h1>Todo Form</h1>
    <input type="text"
      v-model.trim="todoTitle"
      @keyup.enter="createTodo">
    <button @click="createTodo">Add</button>
  </div>

</template>

<script>
export default {
  name: 'TodoForm',
  data: function (){
    return {
      todoTitle: '',
    }
  },
  methods: {
    createTodo: function (){
      const todoItem = {
        title: this.todoTitle,
        isCompleted: false,
        date: new Date().getTime(),
      }
      if (todoItem.title){
        this.$store.dispatch('createTodo', todoItem)
      }
      this.todoTitle = ''
    }
  }
}
</script>
```



##### src/store/index.js

`  mutations: { CREATE_TODO: function(state, todoItem){ state.todos.push(todoItem) } },`

`actions: { createTodo: function(context, todoItem) { context.commit('CREATE_TODO', todoItem) } },`

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    todos: [
      { title: 'Lunch', isCompleted: false, data: new Date().getTime },
      { title: 'Vuex', isCompleted: false, data: new Date().getTime + 1 },
    ]
  },
  getters: {
  },
  mutations: {
    CREATE_TODO: function(state, todoItem){
      state.todos.push(todoItem)
    }
  },
  actions: {
    createTodo: function(context, todoItem){
      context.commit('CREATE_TODO', todoItem)
    }
  },
})
```



#### Actions의 "context" 객체

Vuex store의 전반적인 맥락 속성을 모두 포함하고 있다.

그래서 context.commit을 호출하여 mutation을 호출하거나, context.state와 context.getters를 통해 state와getters에 접근할 수 있다.

* dispatch()로 다른 actions도 호출 가능하다.

**할 수 있지만 actions에서 state를 조작하지 말것**

```js
actions: {
  createTodo: function(context, todoItem){
    console.log(context)
    console.log(context.state)
    console.log(context.getters)
    console.dispatch(...)
    context.commit('CREATE_TODO', todoItem)
  }
},
```



#### Mutations handler name

Mutations 함수(핸들러 함수)의 이름은 상수로 작성하는 것을 권장한다.

* linter와 같은 tool에서 디버깅하기에 유용하며, 전체 애플리케이션에서 어떤 것이 mutation인지 한눈에 파악할 수 있다.



#### Javascript Destructuring assignment

배열의 값이나 객체의 속성을 고유한 변수로 압축 해제(unpack)할 수 있는 JavaScript 표현식

```js
// 00_destructuring.js

const context = {
  commit: function(){
    console.log('commit!')
  },
  state: {
    todo: 'todo 1'
  },
  getters: {},
  mutations: {},
}

// 1. 하나 하나 할당
const commit = context.commit
const state = context.state
console.log(commit())
console.log(state)

// Destructuring assignment
// 2. 이름으로 가져온다.
// 2.1 순서가 필요헝ㅄ다.
const { state, commit } = context
console.log(commit())
console.log(state)

// 2.2 한 개만 가져와도 상관없다.
const { commit } = context
console.log(commit())
```

```js
 actions: {
  createTodo(context){
    context.commit('CREATE_TODO')
  }
},

 actions: {
  createTodo(context){
    const commit = context.commit
    commit('CREATE_TODO')
  }
},
    
 actions: {
  createTodo(context){
    const { commit } = context
    commit('CREATE_TODO')
  }
},
    
 actions: {
  createTodo({ commit }){
    commit('CREATE_TODO')
  }
},    
```



##### actions 변경

```js
// index.js

// before
actions: {
  createTodo: function(context, todoItem){
    context.commit('CREATE_TODO', todoItem)
  }
},
    
// after
actions: {
  createTodo : ({ commit }, todoItem ){
    commit('CREATE_TODO', todoItem)
  }
}
```



### 3. Delete Todo

#### TodoListItem 컴포넌트

deleteTodo action 함수 호출

##### TodoListItem.vue

`<button @click="deleteTodo">Delete</button>`

`methods: { deleteTodo (){ this.$store.dispatch('deleteTodo', this.todo) } }`

```vue
<template>
  <div>
    <h1>Todo</h1>
    <span>{{ todo.title }}</span>
    <button @click="deleteTodo">Delete</button>
  </div>
</template>

<script>
export default {
  name: 'TodoListItem',
  props: {
    todo: {
      type: Object
    }
  },
  methods: {
    deleteTodo (){
      this.$store.dispatch('deleteTodo', this.todo)
    }
  }
}
</script>
```



#### Actions & Mutations

##### src/store/index.js

`DELETE_TODO: function(state, todoItem){  const index = state.todos.indexOf(todoItem) state.todos.splice(index, 1) }`

`deleteTodo({ commit }, todoItem ){ commit('DELETE_TODO', todoItem ) }`

```js
  mutations: {
    DELETE_TODO: function(state, todoItem){
      // 1. todoItem이 첫 번째로 만나는 요소의 index를 가져온다.
      const index = state.todos.indexOf(todoItem)
      // 2. 해당 index 1개만 삭제하고 나머지 요소를 토대로 새로운 배열을 생성한다.
      state.todos.splice(index, 1)
    }
  },
  actions: {
    deleteTodo({ commit }, todoItem ){
      commit('DELETE_TODO', todoItem )
    }
  },
```



### 4. Update Todo

#### TodoListItem 컴포넌트

updateTodoStatus action 함수 호출

##### TodoListItem.vue

`<span @click="updateTodoStatus">{{ todo.title }}</span>`

`updateTodoStatus (){ this.$store.dispatch('updateTodoStatus', this.todo) }`

```vue
<template>
  <div>
    <span @click="updateTodoStatus">{{ todo.title }}</span>
    <button @click="deleteTodo">Delete</button>
  </div>
</template>

<script>
export default {
  name: 'TodoListItem',
  props: {
    todo: {
      type: Object
    }
  },
  methods: {
    deleteTodo (){
      this.$store.dispatch('deleteTodo', this.todo)
    },
    updateTodoStatus (){
      this.$store.dispatch('updateTodoStatus', this.todo)
    }
  }
}
</script>
```

**src/store/index.js**

```js
export default new Vuex.Store({
  mutations: {
	...,
    UPDATE_TODO_STATUS: function(state, todoItem){
      state.todos = state.todos.map(todo => {
        // 1. todoItem과 현재 todos의요소 todo가 서로 일치하면
        if (todo === todoItem){
          // 2. isCompleted의 값을 변경한 새로운 object를 return
          return {
            title: todoItem.title,
            date: new Date().getTime(),
            isCompleted: !todo.isCompleted
          }
        } else {
          // 3. 일치하지 않으면 기존 배열 return
          return todo
        }
      })
    }
  },
  actions: {
	...,
    updateTodoStatus({ commit }, todoItem ){
      commit('UPDATE_TODO_STATUS', todoItem)
    }
  },
})
```



#### Javascript Spread Syntax

"전개 구문"

배열이나 문자열과 같이 반복 가능한(iterable) 문자를 요소(배열 리터럴의 경우)로 확장하여, 0개 이상의 key-value의 쌍으로 된 객체로 확장시킬 수 있다.

'...'을 붙여서 요소 또는 키가 0개 이상의 iterable object를 하나의 object로 간단하게 표현하는 법

ECMAScript2015에서 추가되었다.

Spread Syntax의 대상은 반드시 iterable 객체여야한다.



**주 사용처**

1 함수 호출

* 배열의 목록을 함수의 인수로 활용 시

2 배열

* 배열 연결
* 배열 복사

3 객체

* 객체 복사

**객체에서의 전개 구문**

* 객체 복사 (shallow copy)

```js
const obj1 = { foo: 'bar', x: 42}
const obj2 = { foo: 'baz', y: 13}

const cloneObj = { ...obj1}
// {foo: 'bar', x: 42}
const mergedOjb = { ...obj1, ...obj2 }
// {foo: 'baz', x: 42, y: 13}
```

```js
const todoItem = {
  todo: 'First',
  dueDate: '1999-12-12',
  importance: 'high',
  isCompleted: false,
}

// isCompleted 값만 변경
// 1. 첫번째 방법
const UpdatedItem = {
  todo: 'First',
  dueDate: '1999-12-12',
  importance: 'high',
  isCompleted: true,
}

// 2. 두번째 방법
const UpdatedItem2 = {
  ...todoItem,
  isCompleted: true,
}
```



**Mutation 변경**

변경 전

* title: todoItem.title

변경 후

* ... todo,

```js
mutations: {
  UPDATE_TODO_STATUS: function (state,todoItem) {
    state.todos = state.todos.map(todo => {
      if ( todo === todoItem) {
        return {
          ...todo,
          isCompleted: !todo.isCompleted
        }
      } else {
        return todo
      }
    })
  }
}
```



#### 취소선 긋기

* v-bind를 사용한 class binding

**TodoListItem.vue**

```vue
<template>
  <div>
    <span @click="updateTodoStatus(todo)" :class="{'is-completed': todo.isCompleted}">{{ todo.title }}</span>
    <!-- <button @click="deleteTodo">Delete</button> -->
    <button @click="deleteTodo(todo)">Delete</button>
  </div>
</template>

<style>
.is-completed {
  text-decoration: line-through;
}
</style>
```

:heavy_check_mark: \<style scoped>

현재 scope에서의 tag만 선택하고 싶을 때 사용한다.



### 5. Getters

#### 5.1 완료된 todo 개수 계산

##### src/store/index.js

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  getters: {
    completedTodosCount: function(state){
      return state.todos.filter(todo =>{
        return todo.isCompleted === true
      }).length
    }
  },
})
```



#### 5.2 getters 사용 & computed 반환 값으로 사용

##### App.vue

`<h2>Completed Todo: {{ completedTodosCount }}</h2>`

`  computed: { completedTodosCount: function(){ return this.$store.getters.completedTodosCount }}`

```vue
<template>
  <div id="app">
    <h1>MY TODOS</h1>
    <h2>Completed Todo: {{ completedTodosCount }}</h2>
    <todo-list></todo-list>
    <todo-form></todo-form>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList.vue'
import TodoForm from '@/components/TodoForm.vue'
export default {
  name: 'App',
  components: {
    TodoList,
    TodoForm,
  },
  computed: {
    completedTodosCount: function(){
      return this.$store.getters.completedTodosCount
    }
  }
}
</script>
```



#### 5.3 완료되지 않은 todo 개수 계산

##### src/store/index.js

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  getters: {
    uncompletedTodosCount: function(state){
      return state.todos.filter(todo =>{
        return todo.isCompleted === false
      }).length
    }
  },
})
```



#### 5.4  getters 사용 & computed 반환 값으로 사용

##### App.vue

```vue
<template>
  <div id="app">
    <h1>MY TODOS</h1>
    <h2>Completed Todo: {{ completedTodosCount }}</h2>
    <h2>Unompleted Todo: {{ uncompletedTodosCount }}</h2>
    <todo-list></todo-list>
    <todo-form></todo-form>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList.vue'
import TodoForm from '@/components/TodoForm.vue'
export default {
  name: 'App',
  components: {
    TodoList,
    TodoForm,
  },
  computed: {
    completedTodosCount: function(){
      return this.$store.getters.completedTodosCount
    },
    uncompletedTodosCount: function(){
      return this.$store.getters.uncompletedTodosCount
    }
  }
}
</script>
```



#### 5.5 전체 todo 개수 계산

##### src/store/index.js

`allTodosCount: function(state){ return state.todos.length }`

```
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  getters: {
    completedTodosCount: function(state){
      return state.todos.filter(todo =>{
        return todo.isCompleted === true
      }).length
    },
    uncompletedTodosCount: function(state){
      return state.todos.filter(todo =>{
        return todo.isCompleted === false
      }).length
    },
    allTodosCount: function(state){
      return state.todos.length
    }
  },
})
```



#### 5.6 getters 사용 & computed 반환 값으로 사용

##### App.vue

```vue
<template>
  <div id="app">
    <h1>MY TODOS</h1>
    <h2>All Todos: {{ allTodosCount }}</h2>
    <todo-list></todo-list>
    <todo-form></todo-form>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList.vue'
import TodoForm from '@/components/TodoForm.vue'
export default {
  name: 'App',
  components: {
    TodoList,
    TodoForm,
  },
  computed: {
    allTodosCount: function(){
      return this.$store.getters.allTodosCount
    }
  }
}
</script>
```



### Vuex component binding helper

JS Array Helper Method를 통해 배열 조작을 편하게 하는 것과 유사하다.

* 논리적인 코드 자체가 변하는 것이 아니라 "쉽게" 사용할 수 있도록 되어있음에 초점을 맞춘 것이다.

종류

* mapState
* mapGetter
* mapActions
* mapMutations
* createNamespacedHelpers

#### "mapState"

computed와 Store의 state를 매핑

Vuex Store의 하위 구조를 반환하여 component옵션을 생성한다.

매핑된 computed 이름이 state 이름과 같을 때 문자열 배열을 전달할 수 있다.

**src/store/index.js**

```js
computed: {
  todos: function(){
    return this.$store.state.todos
  }
}
```

:arrow_down_small:

**TodoList.vue**

```vue
import {mapState} from 'vuex'
```

**src/store/index.js**

```js
computed: mapState([
  'todos',
])
```



하지만 다른 computed값을 함께 사용할 수 없기 때문에 최종 객체는 computed에 전달할 수 있도록 다음과 같이 객체 전개 연산자(Object Spread Operator)로 객체를 복사하여 작성한다.

* mapState()는 객체를 반환한다.

```js
computed: {
  ...mapState([
    'todos'
  ])
}
```



**TodoList.vue**

```vue
<script>
// 1. vuex 모듈에서 mapState 메서드만 가져온다.
import { mapState } from 'vuex'

export default{
  ...
  computed:{
	// todos: function(){
    // 	 return this.$store.state.todos
    // }
    // 2. todos는 state에 지정한 이름을 그대로 사용한다.
    ...mapState([
      'todos',
    ])
  }
}
}
</script>
```



#### "mapGetters"

Computed와 Getters를 매핑한다.

getters를 객체 전개 연산자(Object Spread Operator)로 계산하여 추가한다.

해당 컴포넌트 내에서 매핑하고자하는 이름이 index.js에 정의해 놓은 getters의 이름과 동일하면 배열의 형태로 해당 이름만 문자열로 추가한다.

**App.vue**

```vue
<script>

import { mapGetters } from 'vuex'

export default{
  ...
  computed:{
    // mapGetters 안에 정의한 메서드 중에서 아래 3개만 가져와서 Array에 추가한다.
    ...mapGetters([
      'completedTodosCount',
      'uncompletedTodosCount',
      'allTodosCount'
    ])
  }
}
}
</script>
```



#### "mapActions"

action을 전달하는 컴포넌트 method 옵션을 만든다.

actions를 객체 전개 연산자(Object Spread Operator)로 계산하여 추가한다.

[주의]

mapActions를 사용하면, 이전에 dispatch()를 사용했을 때 playload로 넘겨줬던 this.todo를 pass prop으로 변경해서 전달해야한다.

```vue
<template>
  <div>
    <span>{{ todo.title }}</span>
    <button @click="deleteTodo">Delete</button>
  </div>
</template>

<script>
export default {
  name: 'TodoListItem',
  props: {
    todo: {
      type: Object
    }
  },
  methods: {
    deleteTodo (){
      this.$store.dispatch('deleteTodo', this.todo)
    }
  }
}
</script>
```

:arrow_down_small:

```vue
<template>
  <div>
    <span>{{ todo.title }}</span>
    <button @click="deleteTodo">Delete</button>
  </div>
</template>

<script>
// import vuex from 'vuex'    
import { mapActions } from 'vuex' 
export default {
  name: 'TodoListItem',
  props: {
    todo: {
      type: Object
    }
  },
  methods: {
//    deleteTodo (){
//      this.$store.dispatch('deleteTodo', this.todo)
//    }

      // deleteTodo: vuex.mapActions(['deleteTodo', 'createTodo']), deleteTodo
      
    ...mapActions([
      'deleteTodo',
      ])
  }
}
</script>
```



### Local storage

#### vuex-persistendstate

Vuex state를 자동으로 브라우저의 LocalStorage에 저장해주는 라이브러리 중 하나이다.

페이지가 새로고침되어도 Vuex state를 유지시킨다.



설치

```bash
$ npm i vuex-persistedstate
```



라이브러리 사용

**index .js**

```js
import createPersistedState from 'vuex-persistedstate'

export default ne Vuex.Store({
  plugins: [
    createPersistedState(),
  ],
  ...
})
```



:heavy_check_mark: 개발자도구 - Application - Local Storage에 저장된 데이터를 확인



:heavy_exclamation_mark:

```js
const data = JSON.stringify(todos)
localStorage.setItem('todos', data)
```

```js
const prevData = localStorage.getItem('todos')
JSON.parse(prevData)
```



### 마무리

#### 그냥 mutation으로만 state를 변경하면 안될까?

가능하다

* 단, 저장소의 각 컨셉(state, getters, mutations, actions)은 각자의 역할이 존재하도록 설계되어있다.

물론 우리가 작성한 todo app처럼 actions의 로직이 특별한 작업 없이 단순히 mutations만을 호출하는 경우도 있으나 

* 이 경우는 Vuex 도입의 적절성을 판단해 볼 필요가 있다.



### Vuex, 그럼 언제 사용해야 할까?

Vuex를 공유된 상태 관리를 처리하는 데 유용하지만, 개념에 대한 이해와 시작하는 비용이 크다.

앱이 단순하다면 Vuex가 없는 것이 더 적절할 수 있다.

그러나 중대형 규모의 SPA를 구축하는 경우 Vuex는 자연스럽게 선택할 수 있는 단계가 오게 된다.

결과적으로 역할에 적절한 상황에서 활용했을 때 Vuex라이브러리 효용을 극대화할 수 있다.

즉, 필요한 순간이 왔을 때 사용하는 것을 권장한다.



"Flux 라이브러리는 안경과 같습니다. 필요할 때 알아볼 수 있습니다." 

\- Dan Abramov (author of Redux)