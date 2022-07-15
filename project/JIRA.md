# JIRA

:white_check_mark:개발 일감(Epic, User Story), 버그 등을 작성, 개발자를 할당

:arrow_right:개발 상태 및 릴리스(배포) 관리



:ok:기획자, 팀원, 검토자간 협업을 도와주는 도구

:x:팀원을 관리하는 목적의 도구



## JIRA(Kanban)

Planning: user story 및 issue(일감)을 생성하고 sprint을 계획

Tracking: 팀 업무의 우선순위를 정하고, 수행 상태 등 가시성 제공

Release: 일감의 개발완료 등 최신 정보를 가지고 제품 출시 관리

Report: 실시간 시각적 데이터를 기반으로 팀 효율을 향상



### 0. 사전 준비 (Admin 권한자가 수행)

#### 0.1 프로젝트 생성

Jira Software 네비게이션바 - 프로젝트 -프로젝트 만들기



**프로젝트 만들기**

프로젝트 종류 및 설정된 프로세스

* 스크럼 스포트웨어 개발: To Do :arrow_right: In Progress :arrow_right: Done
* 기본 소프트웨어 개발: To Do :arrow_right: In Progress :arrow_right: In Review :arrow_right: Done



**기본 소프트웨어 개발**

프로젝트 명 및 키 작성

* 이름
* 키
* 프로젝트 담당

키는 일감(Issue) ID의 prefix명으로 사용



#### 0.2 Project Role 추가

JIRA 관리 > 시스템 > 프로젝트 역할

프로젝트 역할별 권한 변경



#### 0.3 Kanban 보드 생성

##### 0.3.1 보드의 종류 선택

Kanban 보드 vs Scrum 보드 차이

* Kanban 보드: 일감 전체가 보드에 보임
* Scrum 보드: 현재 실행중인 Sprint에 할당된 일감만 보인다.

Kanban보드가 익숙해지면, Sprint 단위로 관리하는 스크럼 보드를 활용하는 것을 추천

생성한 일감(issue)이 보이지 않아 어려움이 있다.



**애자일 보드 만들기**

* 스크럼 보드 만들기
* 칸반 보드 만들기

**보드 이름 작성**

이 보드에 이름 짓기



##### 0.3.2 보드 설정

생성된 보드에서 환경설정 버튼을 통해 보드 환경 설정

일반 - 일반 및 필터 - 필터 - 공유 - 필터 공유 편집

**현재 필터 편집**

편집기 추가



**칸반보드 설정**

열(컬럼) 추가

상태의 수만큼 컬럼을 추가할 필요가 있을 때 추가한다.

예시의 경우: "할일 :arrow_right: 진행 중 (:arrow_right:IN REVIEW) :arrow_right: 완료" :heavy_check_mark:IN REVIEW 추가

:heavy_check_mark:열 관리



#### 0.4 프로젝트 설정

프로젝트 설정 > 이슈 유형 > 이슈 유형 수정

일감 생성 시 사용할 디폴트 유형 선택

현재 사용중인 이슈 유형에서 불필요한 유형은 사용 가능한 이슈 유형으로 이동하여 프로젝트에서 사용할 이슈 유형을 정한다.



프로젝트 설정 > 사용자의 역할 > 역할에 사용자 추가 > 사용자 또는 그룹, 역할 **추가하기**

:heavy_check_mark:필요할 경우 사용 권한을 사용한다.

예) 이슈 생성, 이슈 할당

프로젝트 설정 > 사용 권한 > 권한 도우미 - 권한 편집



### 1. 일감(Issue) 작성 및 상태 관리

#### 1.1 일감(Issue) 종류

**Epic**: 큰 단위의 업무(여러 User Story, Task 등을 묶는 단위)

**User Story**: 최종 고객에게 가치를 제공하는 기능

* 작성 방법: "I as WHO want to do WHAT, so that WHY"
* **TIP**: User story의 크기는 sprint내에 완료 가능한 단위로 분할이 필요하다.
* 예) 사용자 관리 개발

**Task**: User Story외의 기술적, 관리적 업무

* 예) 설계, 서버 설치, 클라우드 도입 등

**Sub-Task**

* Story, Task을 더 작은 단위로 나눈 업무
* 모든 Sub-Task가 끝나야 해당 업무가 종료된다.
* 예) 사용자 관리(UI)개발, 사용자 관리(Service) 개발

[참고]

 JIRA에서는 Story와 Task을 같은 레벨로 구분하지만, 일반적으로 Story를 더 작게 나눈 것을 Task라고 정의하기도 한다.



#### 1.2 일감 작성

**Epic 생성**

이슈 만들기

(필수)

프로젝트(Project), 이슈 유형 **Epic**(Issue Type), Epic Name, 요약(Summary), 보고자(Reporter)

(선택)

우선순위(Priority) - Highest, High, Medium, Low, Lowest

Story Points



**User Story 추가**

Story을 추가하고 관련된 Epic link을 연결한다.

(필수)

프로젝트(Project), 이슈 유형 **Story**(Issue Type), 요약(Summary), 보고자(Reporter) + Epic Link

(선택)

우선순위(Priority) - Highest, High, Medium, Low, Lowest

Story Points



**Sub Task 생성**

Story 혹은 Task에서 

더 많은 조치(More) > 하위 작업 생성(Create sub-task)

(필수)

이슈 유형 **자동 선택**(Issue Type), 요약(Summary), 보고자(Reporter), 담당자(Assignee) **만들기**

(선택)

우선순위(Priority) - Highest, High, Medium, Low, Lowest

Story Points



**칸반보드 Swimlane 설정**

Epic(큰틀): Epic 단위로 그룹핑해서 보기

Story(이야기): 이야기 단위로 그루핑해서 보기

:heavy_check_mark:Epic, user story, 담당자 별로 그루핑해서 볼 수 있다.



환경설정 - 수영레인[기본 레인: 큰틀(Epic)]

:heavy_check_mark:Epic 별 Story와 Task을 볼 수 있다.

Epic

​	User Story

​		Sub-Task



#### 1.3 보고자 및 담당자 할당

Reporter(보고자): 일감 업무 내용을 작성하고, 진행 상황을 보고 받는 자

(원래: 일을 시키는 사람이 작성, 일감 작성자로 기본 할당된다.)

Assignee(담당자): 해당 일감을 수행하고, 일감상태를 현행화할 담당자



#### 1.4 우선순위 조정

Product owner는 일감의 우선순위로 정렬

* 특히 담당자별 수행해야 할 작업이 여러개라면



#### 1.5 일감 진행 상태 변경

**Drag & Drop으로 상태명의 컬럼간 이동**

**작업 요청자(기획자)가 검토 후 최종 완료 상태로 이동**

* 개발자가 완료하면 "리뷰 중" 상태로 변경
* 기획자는 검토하고 "완료" 상태로 변경



#### 1.6 덧글 작성

@이름으로 전달할 사람을 선택하는 기능 사용 시 유용



#### 1.7 Watcher(지켜보기)

JIRA는 기본적으로 보고자, 담당자에게만 일감 변경, 덧글 발생시 알림이 가며, 담당자를 1명만 선택가능

방법 1) 숫자(Watch하고 있는 사람수)를 클릭해서 다른 사람 추가

방법 2) 본인이 관심있는 일감을 클릭하여 추가



#### 1.8 일감 완료



### 2. 필터 기능 사용

#### 2.1. 기본 Quick Filter(빠른 필터) 사용

[내이슈만] : assignee = currentUser()

* 담당자가 현재 로그인한 사용자

[최근 업데이트] : updatedDate >= -1d

* 수정한 기간이 1일 미만



#### 2.2 Quick Filter 추가하여 사용

* 보드 환경설정으로 이동
* Quick Filter(빠른 필터) 추가
  * 예시
  * 개발자1의 업무만 선택



### 3. 배포(릴리스) 관리

배포.. > 배포(릴리스) 생성

좌측의 윈도우 > 배포(배포 릴리스를 보는 것이 가능)

배포 버전 상세 보기도 가능하다.



### 4. 보고서

:chart:보고서 > 누적 흐름 도표

:chart:보고서 > 최근 생성된 이슈 보고서



## JIRA(Scrum)

### 1. Scrum Board와 Kanban Board

**Scrum 보드**

* Timebox(Sprint) 단위로 일감관리를 하는 프로젝트
  * 2주 단위로 sprint planning을 수립 후 수행하는 프로젝트
* JIRA Scrum 보드에는 전체 일감이 아닌, Sprint내에 할당된 일감만 보인다.

**Kanban 보드**

* Timebox없이 일감관리를 하는 프로젝트
  * 요청(Ticket)이 발생되면 최단시간(Lead time)에 처리해야하는 프로젝트
* JIRA Kanban 보드에는 등록된 전체 일감이 보인다.

[비교 참고] : https://medium.com/hgmin/devops-jira%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%9C-%ED%98%91%EC%97%85-ii-fe28e7ab829c



### 2. Scrum board 관리

#### 2.1 Scrum board 만들기

보드 만들기 > 스크럼 보드

* 보드 이름
* 프로젝트



#### 2.2 Scrum보드 환경설정

* Scrum 보드 컬럼명 수정



#### 2.3 Scrum보드 확인

* 백로그 확인
* Scrum 보드 확인
  * 현재 상태에서는 일감이 Backlog에만 있고, 수행 중인 sprint에 할당이 되어 있지 않기 때문에 아래와 같이 scrum 보드에 일감이 보이지 않습니다.



### 3. Sprint 관리

#### 3.1 Sprint 생성

백로그 > **스프린트 만들기**

* 스프린트 이름

* 기간

* 시작일

  **만들기**



#### 3.2 Sprint Planning

* Backlog에서 일감을 Sprint로 이동(Drag & Drop) 또는 [이슈 생성] 버튼으로 신규 일감 생성 가능



#### 3.3 Story Point 입력

일감에 story point을 입력

:heavy_check_mark:입력 항목이 보이지 않는 경우

* 필드 구성에서 Story pint항목을 선택
* Systme Admin이 추가가능



#### 3.4 작업자 할당

담당자: 실무자, 일감의 상태 현행화 책임자 등

보고자: 작업지시자, Product Owner 등



#### 3.5 일감량 확인

일감에 업무량(Story points)을 입력해 놓으면, 할당 된 담당자별 일감량 확인을 통해 업무 분장 가능



### 4. 버전/배포 계획

#### 4.1 버전 등록

Backlog > [+] 버튼 버전 만들기

* 프로젝트명
* 이름



#### 4.2 버전 계획

개발이 예정된 버전에 drag & drop으로 mapping 가능



### 5. Sprint 시작

#### 5.1. [스프린트 시작] 버튼 클리

* 스프린트 이름(필수)

* 목표

* 기간

* 시작일, 종료일

  **시작**



#### 5.2 Scrum 보드 확인

수행 중인 Sprint에 할당된 일감만 보인다.

Scrum board 환경설정에서 Swim Lane에 그룹핑해서 보여주기 위한 기준 설정 가능하다.



### 6. Sprint 완료

#### 6.1 일감 진행 상태 현행화

#### 6.2 Sprint 완료 처리

**Sprint 완료**

* 포함된 사항 확인 가능

  * 완료된 Issue

  * 완료되지 않은 Issue

    **완료**



**Sprint 계획**

* 이전 Sprint에 미완성 일감이 다음 Sprint에 할당된다.



**배포(릴리스) 관리**

버전의 완료 진행사항 



### 7. 보고서 및 대시보드 관리

#### 7.1 보고서

보고서 선택

* 번다운 차트(소멸 차트)
* 누적 흐름 도표



#### 7.2 Dashboard(대시보드) 관리

Dashboard > 대시보드 관리 > 대시보드 생성

* 이름
* 편집기 추가

가젯 추가

보여줄 항목 편집

* 프로젝트 선택 등

