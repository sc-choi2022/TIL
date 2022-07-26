# FE에서 빌드하기

:ballot_box_with_check:Build란?

소스 코드 파일을 컴퓨터에서 실행할 수 있는 독립적인 형태로 변환하는 과정과 결과

**컴파일 된 코드를 실제 실행할 수 있는 상태로 만드는 일**



## 프로젝트 Dependencies  설치

Front-end Project을 실행하기 위해 Dependencies을 설치하는 것이 필요하다.

```bash
npm install
```



## 프로젝트 Dev. 모드 실행

Dependencies 설치 후 Project을 구동시킨다.

Webpack dev 서버를 실행한다.

```bash
npm run serve
```

정상적으로 Webpack dev 서버가 실행된다면 localhost:8083에서 FE Project의 동작을 확인할 수 있다.

:question:[.../api/v1]으로 시작되는 URL은 localhost:8080으로 Proxy 처리되기 때문에 Back-end API로의 호출을 확인하려면 Back-end 프로젝트가 실행되어 있어야한다.

:ballot_box_with_check:Proxy?

대리, 대리인, 중계를 뜻하는 단어

내부 네트워크에서 인터넷 접속을 할 때, 빠른 액세스나 안전한 통신등을 확보하기 위한 중계서버를 **프록시 서버**라고 한다.

Client와 Web Server의 중간에 위치하여 대신 통신을 받아주즌 것이 프록시 서버이다.



## 프론트엔드 빌드

Front-end 프로젝트의 빌드(Webpack 번들링)을 위해 /fronted directory에서 명령어를 입력한다.

```bash
npm run build
```

:heavy_check_mark:프로젝트 빌드 수행이 정상적으로 완료된다면 번들링된 산출물이 생성된다.

![image-20220726125620587](.\Build.assets\image-20220726125620587.png)

위치는 dist에 생성이 되었다.

다만 가이드라인에 따르면 이는 backend\src\main\resources에 생성되는 것이 적절하여 폴더를 이동했다.



## MySQL DB 접속 계정 입력

backend/build/libs 위치의 application.properties파일을 편집기를 통해 열고 다음 내용을 변경한다.

```properties
#database

spring.datasource.hikari.username=
spring.datasource.hikari.password=
```



## 통합 빌드 및 실행

Front-end 프로젝트와 Back-end 프로젝트 전체를 통합 빌드한다.

/backend directory에서 다음 명령어을 입력한다.

```bash
gradlew clean build
```

**BUILD SUCCESSFUL**이 되면 backend/build/libs에 jar파일이 생성된다.



backend\build\libs 위치에서 다음 명령어을 실행

```bash
java -jar "./파일명.jar"
```

![image-20220726131641821](.\Build.assets\image-20220726131641821.png)



## 확인

http://localhost:8080에 접속

http://localhost:8080/swagger-ui/ 에 접속