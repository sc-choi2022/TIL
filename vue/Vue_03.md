# Vue 02

### Youtube Project

### 1. 프로젝트 준비

```bash
$ vue create youtube-project
$ cd youtube-project
$ code .
$ npm i lodash
```



### 2. 유투브 검색 데이터(TheSearchBar.vue)

#### 2.1 컴포넌트 등록

**App.vue**

```vue
<template>
  <div id="app">
    <h1>Youtube</h1>
    <the-search-bar></the-search-bar>
  </div>
</template>

<script>
import TheSearchBar from './components/TheSearchBar.vue'

export default {
  name: 'App',
  components: {
    TheSearchBar,
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



#### 2.2 Emit Event (TheSearchBar.vue -> App.vue)

**TheSearchBar.vue**

```vue
<template>
  <div>
    <input @keyup.enter="onInputKeyword" type="text">
    <button @click="onInputKeyword">검색</button>
  </div>
</template>

<script>
export default {
  name: 'TheSearchBar',
  methods:{
    onInputKeyword: function (event){
      this.$emit('input-change', event.target.value)
    }
  }
}
</script>

<style>

</style>
```

**+ button 동작위해 코드 수정**

```vue
<template>
  <div>
    <input @keyup.enter="onInputKeyword" type="text" id="input">
    <button @click="onInputKeyword">검색</button>
  </div>
</template>

<script>
export default {
  name: 'TheSearchBar',
  methods:{
    onInputKeyword: function (){
      const input = document.querySelector('#input')
      this.$emit('input-change', input.value)
    }
  }
}
</script>
```



#### 2.3 이벤트 청취 후 함께 전달 된 데이터 할당

**App.vue**

```vue
<template>
  <div id="app">
    <h1>Youtube</h1>
    <the-search-bar @input-change="onInputChange"></the-search-bar>
  </div>
</template>

<script>
import TheSearchBar from './components/TheSearchBar.vue'

export default {
  name: 'App',
  components: {
    TheSearchBar,
  },
  data: function(){
    return {
      inputText: null,
    }
  },
  methods: {
    onInputChange: function(inputText){
      // console.log(this) -> Vue Instance
      this.inputValue = inputText
      // console.log(this.inputValue) 아이유
    }
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



### 3. 유투브 요청 & 응답 데이터 처리

#### 3.1 API_KEY, API_URL 할당 & Youtube API 요청 & 응답 데이터를 변수에 할당

:heavy_check_mark: POSTMAN

:heavy_check_mark: **part** parameter

API 할당량 사용을 관리할 수 있도록 해준다.

여러개를 받을 수 있다.

data의 종류 (snippet,..)

snippet와 q, type을 많이 사용하게 될 것

**KEY : VALUE**

key: API_key

part: snippet

type: video

q: something(input값)



**App.vue**

```vue
<template>
  <div id="app">
    <h1>Youtube</h1>
    <the-search-bar @input-change="onInputChange"></the-search-bar>
  </div>
</template>

<script>
import TheSearchBar from './components/TheSearchBar.vue'

const API_KEY = something
const API_URL = 'https://www.googleapis.com/youtube/v3/search'

export default {
  name: 'App',
  components: {
    TheSearchBar,
  },
  data: function(){
    return {
      inputText: null,
      videos: []
    }
  },
  methods: {
    onInputChange: function(inputText){
      // console.log(this) -> Vue Instance
      this.inputValue = inputText
      // console.log(this.inputValue) 아이유
    }
  }
}
</script>
```



**+ axios 추가**

```vue
<template>
  <div id="app">
    <h1>Youtube</h1>
    <the-search-bar @input-change="onInputChange"></the-search-bar>
  </div>
</template>

<script>
import axios from 'axios'
import TheSearchBar from './components/TheSearchBar.vue'
const API_KEY = ''
const API_URL = 'https://www.googleapis.com/youtube/v3/search'

export default {
  name: 'App',
  components: {
    TheSearchBar,
  },
  data: function(){
    return {
      inputText: null,
      videos: []
    }
  },
  methods: {
    onInputChange: function(inputText){
      this.inputValue = inputText

      const params = {
        key: API_KEY,
        part: 'snippet',
        type: 'video',
        q: this.inputValue
      }
      axios({
        method: 'get',
        url: API_URL,
        params,
      })
      .then(res => {
        console.log(res)
        this.videos = res.data.items
      })
      .catch(err => {
        console.log(err)
      })
    }
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



#### 3.2 Pass props (App.vue -> VideoList.vue) & 할당한 응답 데이터를 하위 컴포넌트로 전달

**App.vue**

```vue
<template>
  <div id="app">
    <h1>Youtube</h1>
    <video-list :videos="videos"></video-list>
  </div>
</template>

<script>
import VideoList from './components/VideoList.vue'

export default {
  name: 'App',
  components: {
    TheSearchBar,
    VideoList
  },
  data: function(){
    return {
      inputText: null,
      videos: []
    }
  },
}
</script>
```



#### 3.3 내려받은 prop 데이터 선언 후 사용

**VideoList.vue**

```vue
<template>
  <ul>
    <li v-for="video in videos" :key="video.id.videoId">
      {{ video.snippet.title }}
    </li>
  </ul>
</template>

<script>
export default {
  name: 'VideoList',
  props:{
    videos: {
      type: Array,
      required: true,
    }
  }
}
</script>
```



#### 3.4 Pass props (VideoList.vue -> VideoListItem.vue)

**VideoList.vue**

```vue
<template>
  <ul>
    <video-list-item 
      v-for="video in videos" 
      :key="video.id.videoId"
      :video-item="video" 
    ></video-list-item>
  </ul>
</template>

<script>
import VideoListItem from '@/components/VideoListItem.vue'
export default {
  name: 'VideoList',
  components:{
    VideoListItem
  },
  props:{
    videos: {
      type: Array,
      required: true,
    }
  }
}
</script>
```



#### 3.5 내려받은 prop 데이터(개별 비이도 객체) 선언 후 사용

**VideoListItem.vue**

```vue
<template>
  <li>
    <img :src="videoItem.snippet.thumbnails.default.url" alt="youtube-thumbnail-image">
    {{ videoItem.snippet.title }}
  </li>
</template>

<script>
export default {
  name: 'VideoListItem',
  props: {
    videoItem: {
      type: Object,
      required: true,
    }
  }
}
</script>
```

:arrow_down_small:변경

```vue
<template>
  <li>
    <img :src="videoUrl" alt="youtube-thumbnail-image">
    {{ videoTitle }}
  </li>
</template>

<script>
export default {
  name: 'VideoListItem',
  props: {
    videoItem: {
      type: Object,
      required: true,
    }
  },
  computed:{
    videoTitle(){
      return this.videoItem.snippet.title
    },
    videoUrl(){
      return this.videoItem.snippet.thumbnails.default.url
    }
  }
}
</script>
```

**+ 제목의 불필요한 문자를 제거하는 코드 추가**

```vue
<script>
import _ from 'lodash'
export default {
  computed:{
    videoTitle(){
      const title = _.unescape(this.videoItem.snippet.title)
      return title
    },
    videoUrl(){
      return this.videoItem.snippet.thumbnails.default.url
    }
  }
}
</script>
```



### 4. 유투브 영상 상세 정보 - VideoDetail.vue

#### 4.1 유튜브 상세 영상 정보 알리기

**VideoListItem.vue -> VideoList.vue**

**VideoListItem.vue**

`<li @click="selectVideo">`

`method: {selectVideo: function(){this.$emit('select-video', this.videoItem)}}`

```vue
<template>
  <li @click="selectVideo">
    <img :src="videoUrl" alt="youtube-thumbnail-image">
    {{ videoTitle }}
  </li>
</template>

<script>
import _ from 'lodash'
export default {
  name: 'VideoListItem',
  props: {
    videoItem: {
      type: Object,
      required: true,
    }
  },
  computed:{
    videoTitle(){
      const title = _.unescape(this.videoItem.snippet.title)
      return title
    },
    videoUrl(){
      return this.videoItem.snippet.thumbnails.default.url
    }
  }
  ,method: {
    selectVideo: function(){
      this.$emit('select-video', this.videoItem)
    }
  },
}
</script>
```



**VideoList.vue**

`@select-video="onSelectVideo"`

`methods:{onSelectVideo:function(video){this.$emit('select-video', video)}}`

```vue
<template>
  <ul>
    <video-list-item 
      v-for="video in videos" 
      :key="video.id.videoId"
      :video-item="video" 
      @select-video="onSelectVideo"
    ></video-list-item>
  </ul>
</template>

<script>
import VideoListItem from '@/components/VideoListItem.vue'
export default {
  name: 'VideoList',
  components:{
    VideoListItem
  },
  props:{
    videos: {
      type: Array,
      required: true,
    }
  },
  methods:{
    onSelectVideo:function(video){
      this.$emit('select-video', video)
    }
  }
}
</script>
```



#### 4.2 유튜브 상세 영상 정보 알리기

**VideoList.vue -> App.vue**

**App.vue**

`<header></header>`

`<video-list :videos="videos" @select-video="onVideoSelect"></video-list>`

`selectedVideo: null`

`methods: { onVideoSelect: function(video){ this.selectedVideo = video}}`

```vue
<template>
  <div id="app">
    <h1>Youtube</h1>
    <header>
      <the-search-bar @input-change="onInputChange"></the-search-bar>
    </header>
    <section>
      <video-list :videos="videos" @select-video="onVideoSelect"></video-list>
    </section>
  </div>
</template>

<script>
import axios from 'axios'
import TheSearchBar from './components/TheSearchBar.vue'
import VideoList from './components/VideoList.vue'
const API_KEY = 'AIzaSyC3u0Im-2vcGFbZzNbEQbXXlceDW1gxefc'
const API_URL = 'https://www.googleapis.com/youtube/v3/search'

export default {
  name: 'App',
  components: {
    TheSearchBar,
    VideoList
  },
  data: function(){
    return {
      inputText: null,
      videos: [],
      selectedVideo: null,
    }
  },
  methods: {
	...
    onVideoSelect: function(video){
      this.selectedVideo = video
    }
  }
}
</script>
```



#### 4.3 App 컴포넌트에서 내린 데이터가 VideoDetail에 전달되었는지 확인

**App.vue**

`import VideoDetail from './components/VideoDetail.vue'`

`<video-detail :video="selectedVideo"></video-detail>`

`components: { VideoDetail, }`

```vue
<template>
  <div id="app">
    <h1>Youtube</h1>
    <header>
      <the-search-bar @input-change="onInputChange"></the-search-bar>
    </header>
    <section>
      <video-detail :selected-video="selectedVideo"></video-detail>
      <video-list :videos="videos" @select-video="onVideoSelect"></video-list>
    </section>
  </div>
</template>

<script>
import axios from 'axios'
import TheSearchBar from './components/TheSearchBar.vue'
import VideoList from './components/VideoList.vue'
import VideoDetail from './components/VideoDetail.vue'
const API_KEY = 'AIzaSyC3u0Im-2vcGFbZzNbEQbXXlceDW1gxefc'
const API_URL = 'https://www.googleapis.com/youtube/v3/search'

export default {
  name: 'App',
  components: {
    TheSearchBar,
    VideoList,
    VideoDetail,
  },
  data: function(){
    return {
      inputText: null,
      videos: [],
      selectedVideo: null,
    }
  },
  methods: {
    onInputChange: function(inputText){
      this.inputValue = inputText

      const params = {
        key: API_KEY,
        part: 'snippet',
        type: 'video',
        q: this.inputValue
      }
      axios({
        method: 'get',
        url: API_URL,
        params,
      })
      .then(res => {
        console.log(res)
        this.videos = res.data.items
      })
      .catch(err => {
        console.log(err)
      })
    },
    onVideoSelect: function(video){
      this.selectedVideo = video
    }
  }
}
</script>
```



 #### 4.4 유투브 영상 상세 정보 알리기

**App.vue -> VideoDetail.vue**

**VideoDetail.vue**

`{{ video }}`

`name: 'VideoDetail',`

`  props: { video: { type: Object } }`

```vue
<template>
  <div>
    {{ selectedVideo }}
  </div>  
</template>

<script>
export default {
  name: 'VideoDetail',
  props: {
    selectedVideo: {
      type: Object
    }
  }
}
</script>
```



#### 4.5 VideoDetail 컴포넌트 마무리 & Youtube iframe 문서를 참고하여 videoId 값 찾기

**VideoDetail.vue**

`<div v-if="selectedVideo" class="video-detail"><iframe :src="videoURI" frameborder="0"></iframe></template>`

`computed: { videoURI: function () {
      const videoId = this.video.id.videoId
      return https://www.youtube.com/embed/${videoId} } }`

```vue
<template>
  <div v-if="selectedVideo" class="video-detail">
    <iframe :src="videoURI" frameborder="0"></iframe>
  </div>  
</template>

<script>
export default {
  name: 'VideoDetail',
  props: {
    selectedVideo: {
      type: Object
    }
  },
  computed: {
    videoURI: function () {
      const videoId = this.selectedVideo.id.videoId
      return `https://www.youtube.com/embed/${videoId}`
    }
  }
}
</script>
```

**+ autoplay**

`<iframe v-if="selectedVideo" :src="videoURI" frameborder="0" allow='autoplay'>`

`+'?autoplay=1'`

```vue
<template>
  <div class="video-detail">
    <iframe v-if="selectedVideo" :src="videoURI" frameborder="0" allow='autoplay'></iframe>
  </div>  
</template>

<script>
export default {
  name: 'VideoDetail',
  props: {
    selectedVideo: {
      type: Object
    }
  },
  computed: {
    videoURI: function () {
      const videoId = this.selectedVideo.id.videoId
      return `https://www.youtube.com/embed/${videoId}`+'?autoplay=1'
    }
  }
}
</script>
```



### 5. Environment Variable

#### 5.1 API 키 환경변수 설정

**.env.local 생성**(위치는 src안)

```
VUE_APP_YOUTUBE_API_KEY=API_KEY
```

**App.vue**

```vue
const API_KEY = process.env.VUE_APP_YOUTUBE_API_KEY
```



#### 5.2

프로젝트 최상단에 배치하여 환경 변수를 지정할 수 있다.

'NODE_ENV', 'BASE_URL' 및 'VUE_APP_'으로 시작하는 변수만 클라이언트 번들에 정적으로 표함된다.

.env.local에 작성하는 환경 변수는 개발 단계에서 원격 저장소에 노출시키지 않기 위해 git에 의해 무시되며, 모든 경우에 로드하기 위해 사용한다.

단, 환경 변수는 빌드에 포함되므로 누구나 앱 파일을 검사하여 볼 수 있으며, 실제 배포 단계에서는 배포 서비스에서 이러한 환경 변수를 설정할 수 있도록 환경을 제공한다.



[참고] 환경 변수

* 컴퓨터에서 동작하는 방식에 영향을 미치는, 동적인 값들의 모임
* 시스템의 실행 파일이 놓여 있는 디렉터리의 경로등 운영체제 상에서 동작하는 응용 프로그램이 참조하기 위한 설정이 기록된다.



### 6. Extra

#### css transition

