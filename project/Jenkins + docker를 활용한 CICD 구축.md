## Jenkins + docker를 활용한 CI/CD 구축

CI/CD란?

CI(Continuous Integration) / CD(Continuous Deployment)

지속적 통합 / 지속적 배포

:heavy_check_mark:코드 오타가 많이 나는 부분이다. 확인!



### LEARNING GOALS

Jenkins로 CICD환경을 구축하여 프로젝트 배포를 지속적으로 쉽게 할 수 있다.

Docker로 Jenkins를 설치하고 설정할 수 있다.

Jenkins를 이용하여 도커라이징(컨테이너화)하여 배포할 수 있다.



### 설치 과정에서 확인할 Point

#### :heavy_check_mark: Docker 설치

설치 사이트

https://docs.docker.com/get-docker



❗ 설치 과정에서 restart를 하고 다시 docker를 열 때 다음과 같은 오류창이 뜰 경우!

![image-20220617020953226-16554270360581](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617020953226-16554270360581-16556486217951.png)

https://aka.ms/wsl2kernel

주소로 이동하여 x64 머신용 최신 WSL2 Linux 커널 업데이트 패키지를 설치해준다.![image-20220617095219206](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617095219206-16556486217952.png)

**도커 설치 확인**

![image-20220617095355652](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617095355652-16556486217963.png)



### Docker를 이용하여 Jenkins 설치 및 확인

```
docker run -d -p 9090:8080 -p 50000:50000 -v /var/jenkins:/war/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock --name jenkins -u root jenkins/jenkins:lts-jdk11
```



**설치 확인**

![image-20220617100749527](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617100749527-16556486217964.png)

![image-20220617100520611](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617100520611-16556486217965.png)

❓ Administartor password는 확인방법

![image-20220617101645354](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617101645354-16556486217966.png)

![image-20220617101914583](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617101914583-16556486217967.png)

위 빨간 부분의 위치에서 password를 확인할 수 있다.



:heavy_check_mark: Install suggested plugins

![image-20220617102042512](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617102042512-16556486217978.png)

**설치 확인**

![image-20220617105942774](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617105942774-16556486217979.png)



**Jenkins 플러그인 설치**

**:heavy_check_mark:Gitlab과 docker를 설치**(관련 파일 모두를 설치!)

![image-20220617110355894](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617110355894-165564862179710.png)



**Gitlab**

![image-20220617110737249](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617110737249-165564862179811.png)

![image-20220617111021405](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617111021405-165564862179812.png)



:heavy_check_mark:docker 또한 동일하게 설치해준다.



### Jenkins 컨테이너안 도커 설치

```
docker exec -it jenkins bash
curl https://get.docker.com/ > dockerinstall && chmod 777 dockerinstall && ./dockerinstall
```

![image-20220617115158037](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617115158037-165564862179813.png)

**설치 확인**

```
docker exec -it jenkins sh
```

![image-20220617115349436](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617115349436-165564862179814.png)

![image-20220617141946700](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617141946700-165564862179815.png)

![image-20220617142258093](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617142258093-165564862179816.png)

:heavy_check_mark:위 이름은 test_jenkins_docker와 repo이름또한 test_jenkins_docker 이름을 동일하게 맞춰주었다.



:heavy_check_mark: Credentials를 삭제하고 싶다면 다음 화면에서 해당 credential를 확인하고 삭제해주면 된다.

![image-20220617143514087](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617143514087-165564862179917.png)

![image-20220617144625642](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617144625642-165564862179918.png)

![image-20220617144648293](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617144648293-165564862179919.png)

**Username**: Gitlab에 로그인 하는 이메일에서의 아이디

**Password**: Gitlab에 로그인할 때 사용하는 비밀번호

**ID**: 식별을 위한 ID

![image-20220617144827957](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617144827957-165564862179920.png)

![image-20220617144851873](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617144851873-165564862180021.png)

![image-20220617144944909](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617144944909-165564862180022.png)

```
docker build -t hello_ssafy:latest .
docker run -d -p 80:80 hello_ssafy
```

:heavy_check_mark: Save



![image-20220617145029475](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617145029475-165564862180023.png)

![image-20220617234057600](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617234057600-165564862180024.png)

![image-20220617235710001](Jenkins%20+%20docker%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20CICD%20%EA%B5%AC%EC%B6%95.assets/image-20220617235710001-165564862180025.png)
