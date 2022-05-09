# Vue 01

## Vue.js

#### Front-End Development

HTML, CSS 그리고 JavaScript를 활용해서 데이터를 볼 수 있게 만들어 준다.

* 이 작업을 통해 사용자(User)는 데이터와 상호작용(Interaction)할 수 있다.

대표적인 프론트엔드 프레임워크

* Vue.js, React, Angular



#### Vue.js

사용자 인터페이스(화면)를 만들기 위한 진보적인 자바스크립트 프레임워크

현대적인 tool과 다양한 라이브러리를 통해 SPA(Single Page Application)를 완벽하게 지원한다.



#### SPA

Single Page Application (단일 페이지 애플리케이션)

현재 페이지를 통적으로 렌더링함으로써 사용자와 소통하는 웹 애플리케이션

단일 페이지로 구성되며 서버로부터 최초에만 페이지를 다운로드하고, 이후에는 동적으로 DOM을 구성한다.

* 처음 페이지를 받은 이후부터는 서버로부터 새로운 전체 페이지를 불러오는 것이 아닌, 현재 페이지 중 필요한 부분만 동적으로 다시 작성한다.

연속되는 페이지 간의 사용자 경험(UX)을 향상한다.

* 모바일 사용량이 증가하고 있는 현재 트래픽의 감소와 속도, 사용성, 반응성의 향상은 매우 중요하기 때문이다.

동작 원리의 일부가 **CSR(Client Side Rendering)**의 구조를 따른다.

(SPA와 CSR은 분리하여 이해한다.)



#### SPA의 등장 배경

과거 웹 사이트들은 요청에 따라 매번 새로운 페이지를 응답하는 방식

* MPA(Multi Page Application)

스마트폰이 등장하면서 모바일 최적화의 필요성이 대두되었다.

* 모바일 네이티브 앱과 같은 형태의 웹 페이지가 필요해졌다.

이러한 문제를 해결하기 위해 Vue.js와 같은 프론트엔드(Front-End) 프레임워크가 등장했다.

* **CSR(Client Sid Rendering), SPA(Single Page Application)**의 등장

1개의 웹 페이지에서 여러 동작이 이루어지며 모바일 앱과 비슷한 형태의 사용자 경험을 제공한다.



#### CSR

Client Side Rendering

서버에서 화면을 구성하는 SSR방식과 달리 클라이언트에서 화면을 구성한다.

최초 요청 시 HTML, CSS, JS 등 데이터를 제외한 각종 리소스를 응답받고 이후 클라이언트에서는 필요한 데이터만 요청해 JS로 DOM을 렌더링하는 방식이다.

즉, 처음엔 뼈대만 맏고 브라우저에서 동적으로 DOM을 그린다.

SPA가 사용하는 렌더링 방식

**장점**

1. 서버와 클라이언트 간 트래픽 감소
   * 웹 애플리케이션에 필요한 모든 정적 리소스를 최초에 한 번 다운로드 후 필요한 데이터만 갱신한다.
2. 사용자 경험(UX) 향상
   * 전체 페이지를 다시 렌더링하지 않고 변경되는 부분만을 갱신하기 때문이다.

**단점**

1. SSR에 비해 전체 페이지 최종 렌더링 시점이 느리다.
2. SEO(검색 엔진 최적화)에 있다. (최초 문서에 데이터 마크업이 없기 때문이다.)



#### SSR

Server Side Rendering

서버에서 클라이언트에게 보여줄 페이지를 모두 구성하여 전달하는 방식

JS웹 프레임워크 이전에 사용되던 전통적인 렌더링 방식

**장점**

1. 초기 구동 속도가 빠르다.
   * 클라이언트가 빠르게 컨텐츠를 볼 수 있다.
2. SEO(검색 엔진 최적화)에 적합하다.
   * DOM에 이미 모든 데이터가 작성되어 있기 때문이다.

**단점**

모든 요청마다 새로운 페이지를 구성하여 전달한다.

* 반복되는 전체 새로고침으로 인해 사용자 경험이 떨어진다.
* 상대적으로 트래픽이 많아 서버의 부담이 클 수 있다.



#### SSR & CSR

두 방식의 차이는 최종 HTML 생성 주체가 누구인가에 따라 결정된다.

즉, 실제 브라우저에 그려질(렌더링) HTML

* 서버가 만든다: **SSR**
* 클라이언트가 만든다: **CSR**

SSR과 CSR을 단순 비교하여 '어떤 것이 더 좋다'가 아닌 내 서비스 또는 프로젝트 구성에 맞는 방법을 적절하게 선택하는 것이 중요하다.

예)

Django에서 Axios를 활용한 좋아요/팔오우 로직의 경우 대부분은 Server에서 완성된 HTML을 제공하는 구조 (**SSR**)

특정 요소(좋아요/팔로우)만 JS(AJAX & DOM조작)를 활용한다(**CSR**)

* AJAX를 활용하여 비동기 요청으로 필요한 데이터를 클라이언트에서 서버로 직접 요청을 보내 받아오고 JS를 활용하여 DOM을 조작한다.



#### [참고] SEO