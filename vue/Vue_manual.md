# Vue

```bash
$ vue create pjt-router
```

```bash
> Default ([Vue 2] babel, eslint)
```

```bash
$ cd pjt-router
```

cf)

```bash
$ npm i
```

를 사용해서 package.json에 있는 module을 다운받고, `npm run serve`

```bash
$ npm install axios
```

필요할 경우 필요한 모듈(axios)을 설치

**src/components**

새로운 vue파일 추가 (About.vue)

**App.vue**

```vue
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- 3. 보여주기 (print)-->
    <!-- CamelCase -->
    <TheAbout my-message="CamelCase"/>
    <!-- kebab-case -->
    <the-about my-message="kebab-case"></the-about>
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
  },
}
</script>
```

**TheAbout.vue**

```vue
<template>
  <!-- template 안에는 반드시 하나의 Element만 있어야한다. -->
  <div>
    <h1>About</h1>
  </div>
</template>
```

```bahs
$ npm run serve
```



### Props & Emits

#### Props

**App.vue**

```vue
<template>
  <div id="app">
    <the-about 
      send-data="Send!"
    ></the-about>
  </div>
</template>
```

**TheAbout.vue**

```vue
<template>
  <!-- template 안에는 반드시 하나의 Element만 있어야한다. -->
  <div>
    <h1>About</h1>
    <h2> {{ sendData }} </h2>
  </div>
</template>

<script>
export default {
  name: 'TheAbout',
  props: {
    sendData: String,
  },
}
</script>
```



#### Emits

**TheAbout.vue**

```vue
<template>
  <!-- template 안에는 반드시 하나의 Element만 있어야한다. -->
  <div>
    <button @click="emitData">클릭</button>
  </div>
</template>

<script>
export default {
  name: 'TheAbout',
  data(){
    childData: 'data'
  },
  methods: {
    emitData(){
      this.$emit("name-of-event", this.childData )
    }
  },
}
</script>
```

**App.vue**

```vue
<template>
  <div id="app">
    <the-about 
      send-data="Send!"
      @name-of-event="receiveData"
    ></the-about>
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
  },
  methods:{
    receiveData(data){
      console.log(data)
    }
  }
}
</script>
```



### router

```bash
$ vue add router
```

#### Changes

**before**

components, App.vue, main.js

**after**

router(/index.js), views, App.vue

**App.vue**

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

**router/index.js**(urls.py와 유사한 역할을 한다.)

```js
const routes = [
  {
    path: '/',
    name: 'home',
    component: HomeView
  },
]
```

* App.vue의 router-link의 to가 index.js의 path로 이동하고
* component에 해당하는 vue를 router에 렌더링하겠다.



뒤로가기 버튼도 사용할 수 있다.

* History mode를 사용하기 때문에 가능하다.
* : HTML History API를 사용한다.



:heavy_check_mark:새로운 router에 대한 페이지를 생성하고 싶다면 views에서 만들면 된다.



#### 파일 생성 흐름

**views에 새로운 vue파일 생성**

**TheLotto.vue**

```vue
<template>
  <div>
    <h1>Lotto</h1>
  </div>
</template>

<script>
import _ from 'lodash'
export default {
  name: 'TheLotto',
}
</script>
```

**index.js**

```js
import LottoView from '../views/LottoView.vue'

Vue.use(VueRouter)

const routes = [
  {
    path: '/lotto/:lottoNum',
    name: 'lotto',
    component: LottoView,
  }
]
```

**App.vue**

```vue
<template>
  <div id="app">
    <nav>
      <router-link to="/lotto">Lunch</router-link> |
      <router-link :to="{ name: 'lunch' }">Lunch</router-link> |
      <router-link :to="{ name: 'lotto', params: { lottoNum: 6} }">Lotto</router-link>
    </nav>
    <router-view/>
  </div>
</template>
```

:heavy_check_mark: Named Routes



#### 프로그래밍 방식 네비게이션

**$router.push()**

Vue 인스턴스 내부에서 라우터 인스턴스에  **$router**로 접근할 수 있다.

따라서 다른 URL로 이동하려면 **this.<u>$router</u>.push**를 호출할 수 있다.

* 이 메서드는 새로운 항목을 히스토리 스택에 넣기 때문에 사용자가 브라우저의 뒤로가기 버튼을 클릭하면 URL로 이동하게 된다.

\<router-link>를 클릭할 때 내부적으로 호출되는 메서드이므로 \<router-link :to="...">를 클릭하면, **routher.push(...)**를 호출하는 것과 같다.



**LottoView.vue**

```vue
<template>
  <div>
    <h1>로또</h1>
    <button @click="somFunc">Get Lucky Numbers</button>
  </div>
</template>

<script>
import _ from 'lodash'
export default {
  name: 'LottoView',
  methods: {
    somFunc(){
      this.$router.push('/')
    }
  }
}
</script>
```

작성 인자 예시

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

* params - Dynamic Route Matching
* qurey - ?뒤의 key=value형태



#### Dynamic Route Matching

cf) variable routing

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



**index.js**

```js
import LottoView from '../views/LottoView.vue'
const routes = [
  {
    path: '/lotto/:lottoNum',
    name: 'lotto',
    component: LottoView,
  }
]
```

**LottoView.vue**

```vue
<template>
  <div>
    <h1>로또</h1>
    <button @click="getLottoNumber">Get Lucky Numbers</button>
    <p>{{ numbers }}</p>
  </div>
</template>

<script>
import _ from 'lodash'
export default {
  name: 'LottoView',
  data: function(){
    return {
      numbers: ''
    }
  },
  methods: {
    getLottoNumber(){
      this.numbers = _.sampleSize(_.range(1, 46), this.$route.params.lottoNum)
    }
  }
}
</script>
```



**App.vue**

```vue
<template>
  <div id="app">
    <nav>
      <router-link :to="{ name: 'lunch' }">Lunch</router-link> |
      <router-link :to="{ name: 'lotto', params: { lottoNum: 6} }">Lotto</router-link>
    </nav>
    <router-view/>
  </div>
</template>
```



### .gitignore

```

# Created by https://www.toptal.com/developers/gitignore/api/django,python,venv,visualstudiocode,windows
# Edit at https://www.toptal.com/developers/gitignore?templates=django,python,venv,visualstudiocode,windows

### Django ###
*.log
*.pot
*.pyc
__pycache__/
local_settings.py
db.sqlite3
db.sqlite3-journal
media

# If your build process includes running collectstatic, then you probably don't need or want to include staticfiles/
# in your Git repository. Update and uncomment the following line accordingly.
# <django-project-name>/staticfiles/

### Django.Python Stack ###
# Byte-compiled / optimized / DLL files
*.py[cod]
*$py.class

# C extensions
*.so

# Distribution / packaging
.Python
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
share/python-wheels/
*.egg-info/
.installed.cfg
*.egg
MANIFEST

# PyInstaller
#  Usually these files are written by a python script from a template
#  before PyInstaller builds the exe, so as to inject date/other infos into it.
*.manifest
*.spec

# Installer logs
pip-log.txt
pip-delete-this-directory.txt

# Unit test / coverage reports
htmlcov/
.tox/
.nox/
.coverage
.coverage.*
.cache
nosetests.xml
coverage.xml
*.cover
*.py,cover
.hypothesis/
.pytest_cache/
cover/

# Translations
*.mo

# Django stuff:

# Flask stuff:
instance/
.webassets-cache

# Scrapy stuff:
.scrapy

# Sphinx documentation
docs/_build/

# PyBuilder
.pybuilder/
target/

# Jupyter Notebook
.ipynb_checkpoints

# IPython
profile_default/
ipython_config.py

# pyenv
#   For a library or package, you might want to ignore these files since the code is
#   intended to run in multiple environments; otherwise, check them in:
# .python-version

# pipenv
#   According to pypa/pipenv#598, it is recommended to include Pipfile.lock in version control.
#   However, in case of collaboration, if having platform-specific dependencies or dependencies
#   having no cross-platform support, pipenv may install dependencies that don't work, or not
#   install all needed dependencies.
#Pipfile.lock

# poetry
#   Similar to Pipfile.lock, it is generally recommended to include poetry.lock in version control.
#   This is especially recommended for binary packages to ensure reproducibility, and is more
#   commonly ignored for libraries.
#   https://python-poetry.org/docs/basic-usage/#commit-your-poetrylock-file-to-version-control
#poetry.lock

# PEP 582; used by e.g. github.com/David-OConnor/pyflow
__pypackages__/

# Celery stuff
celerybeat-schedule
celerybeat.pid

# SageMath parsed files
*.sage.py

# Environments
.env
.venv
env/
venv/
ENV/
env.bak/
venv.bak/

# Spyder project settings
.spyderproject
.spyproject

# Rope project settings
.ropeproject

# mkdocs documentation
/site

# mypy
.mypy_cache/
.dmypy.json
dmypy.json

# Pyre type checker
.pyre/

# pytype static type analyzer
.pytype/

# Cython debug symbols
cython_debug/

# PyCharm
#  JetBrains specific template is maintained in a separate JetBrains.gitignore that can
#  be found at https://github.com/github/gitignore/blob/main/Global/JetBrains.gitignore
#  and can be added to the global gitignore or merged into this file.  For a more nuclear
#  option (not recommended) you can uncomment the following to ignore the entire idea folder.
#.idea/

### Python ###
# Byte-compiled / optimized / DLL files

# C extensions

# Distribution / packaging

# PyInstaller
#  Usually these files are written by a python script from a template
#  before PyInstaller builds the exe, so as to inject date/other infos into it.

# Installer logs

# Unit test / coverage reports

# Translations

# Django stuff:

# Flask stuff:

# Scrapy stuff:

# Sphinx documentation

# PyBuilder

# Jupyter Notebook

# IPython

# pyenv
#   For a library or package, you might want to ignore these files since the code is
#   intended to run in multiple environments; otherwise, check them in:
# .python-version

# pipenv
#   According to pypa/pipenv#598, it is recommended to include Pipfile.lock in version control.
#   However, in case of collaboration, if having platform-specific dependencies or dependencies
#   having no cross-platform support, pipenv may install dependencies that don't work, or not
#   install all needed dependencies.

# poetry
#   Similar to Pipfile.lock, it is generally recommended to include poetry.lock in version control.
#   This is especially recommended for binary packages to ensure reproducibility, and is more
#   commonly ignored for libraries.
#   https://python-poetry.org/docs/basic-usage/#commit-your-poetrylock-file-to-version-control

# PEP 582; used by e.g. github.com/David-OConnor/pyflow

# Celery stuff

# SageMath parsed files

# Environments

# Spyder project settings

# Rope project settings

# mkdocs documentation

# mypy

# Pyre type checker

# pytype static type analyzer

# Cython debug symbols

# PyCharm
#  JetBrains specific template is maintained in a separate JetBrains.gitignore that can
#  be found at https://github.com/github/gitignore/blob/main/Global/JetBrains.gitignore
#  and can be added to the global gitignore or merged into this file.  For a more nuclear
#  option (not recommended) you can uncomment the following to ignore the entire idea folder.

### venv ###
# Virtualenv
# http://iamzed.com/2009/05/07/a-primer-on-virtualenv/
[Bb]in
[Ii]nclude
[Ll]ib
[Ll]ib64
[Ll]ocal
[Ss]cripts
pyvenv.cfg
pip-selfcheck.json

### VisualStudioCode ###
.vscode/*
!.vscode/settings.json
!.vscode/tasks.json
!.vscode/launch.json
!.vscode/extensions.json
!.vscode/*.code-snippets

# Local History for Visual Studio Code
.history/

# Built Visual Studio Code Extensions
*.vsix

### VisualStudioCode Patch ###
# Ignore all local history of files
.history
.ionide

# Support for Project snippet scope

### Windows ###
# Windows thumbnail cache files
Thumbs.db
Thumbs.db:encryptable
ehthumbs.db
ehthumbs_vista.db

# Dump file
*.stackdump

# Folder config file
[Dd]esktop.ini

# Recycle Bin used on file shares
$RECYCLE.BIN/

# Windows Installer files
*.cab
*.msi
*.msix
*.msm
*.msp

# Windows shortcuts
*.lnk

# End of https://www.toptal.com/developers/gitignore/api/django,python,venv,visualstudiocode,windows

.env

# Created by https://www.toptal.com/developers/gitignore/api/vuejs
# Edit at https://www.toptal.com/developers/gitignore?templates=vuejs

### Vuejs ###
# Recommended template: Node.gitignore

node_modules/
dist/
npm-debug.log
yarn-error.log

# End of https://www.toptal.com/developers/gitignore/api/vuejs
```

