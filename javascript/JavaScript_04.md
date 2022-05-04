**axios.get(URL)
  .then(res => res.data)
  .then(todo => todo.title)
  .then(title => console.log( title ))
  .catch(error => {
    if (error.response.status === 404){
        alert('No such a thing')
    }
  })
  .finally(() => console.log('Done!'))javascript event loop visualizer**

```javascript
console.log('Start')
function after3 (){ console.log('3s') }
function after0 (){ console.log('0s') }

setTimeout(after3, 3000)
setTimeout(after0, 0)

console.log('End')
```

**Callback Queue는 Call Stack이 비어있을 때 callback함수가 Call Stack으로 가게 된다.**



```javascript
// chain의 예시를 보여주기 위한 코드
axios.get(URL)
  .then(res => res.data)
  .then(todo => todo.title)
  .then(title => console.log( title ))
  .catch(error => {
    if (error.response.status === 404){
        alert('No such a thing')
    }
  })
  .finally(() => console.log('Done!'))
```

```javascript
// 위 코드와 동일한 코드
axios.get(URL)
  .then(res => console.log(res.data.title))
  .catch(error => {
    if (error.response.status === 404){
        alert('No such a thing')
    }
  })
  .finally(() => console.log('Done!'))
```


```javascript
axios.get(URL)
  .then(res => {
    const todosArray = res.data							// 전체 data 받아온다.
    const todo = todosArray.find(todo => todo.id === 10)// 원하는 조건 찾아온다.
    return axios.get(`${URL}${todo.id}`)				// todo 가지고 작업한다.
  })
  .then(res => console.log(res.data))
  .catch(error => {
    if (error.response.status === 404){
        alert('No such a thing')
    }
  })
  .finally(() => console.log('Done!'))
```



Promise

```javascript
const URL = 'https://dog.ceo/api'

axios.get(URL + '/breeds/list/all')
  .then(res =>{
    const breedObj = res.data.message
    const breedArray = Object.keys(breedObj)
    const breed = breedArray[0]
    return axios.get(URL + `/breed/${breed}/images`)
  })
  .then(res => {
    console.log(res)
  })
  .catch(err => {
    console.error(error.response)
  })
```

async & await 적용

```javascript
const URL = 'https://dog.ceo/api'
// 0. async-await를 사용하려면, 함수로 묶어야 한다.
// 1. 해당 함수 맨 앞에 async라는 키워드로 표시를 남긴다.
// 2. 함수 블록 내부에 비동기로 동작하는 함수들을 찾아서 앞에 await를 남긴다.
async function fetchDogImages(){
  const res = await axios.get(URL + '/breeds/list/all')
  const breedObj = res.data.message
  const breedArray = Object.keys(breedObj)
  const breed = breedArray[0]
  const images = await axios.get(URL + `/breed/${breed}/images`)
  console.log(images)
}

fetchDogImages()
  .catch(error => console.error(error.response))
```



### 1. javascript이 동작할 때 뒤에서 어떻게 동작하는 지에 대한 이해

### 2. AJAX요청(비동기적 요청)을 보낼때 때 axios를 사용할 것이다. axios 코드를 어떻게 쓸 것인가



```html
  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
```

from django.http import JsonResponse

