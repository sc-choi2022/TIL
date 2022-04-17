# Django_DB

## DB

체계화된 데이터의 모임

몇 개의 자료 파일을 조직적으로 통합하여 자료 항목의 중복을 없애고 자료를 구조화하여 기억시켜 놓은 자료의 집합체

**SQL** DB를 핸들링하는 언어

### 장점

데이터 중복 최소화, 데이터 무결성(정확한 정보를 보장), 데이터 일관성, 데이터 독립성(물리적/논리적), 데이터 표준화, 데이터 보안 유지



## 관계형 데이터베이스 (RDB)

키(key)와 값(value)들의 간단한 관계(relation)를 표(table) 형태로 정리한 데이터베이스

### 용어

스키마(schema) : 데이터베이스에서 자료의 구조, 표현방법, 관계등 전반적인 명세를 기술한 것

테이블(table) : 열(컬럼/필드)과 행(레코드/값)의 모델을 사용해 조직된 데이터 요소들의 집합

열(column) : 각 열에는 고유한 데이터 형식이 지정된다.

행(row) : 실제 데이터가 저장되는 형태, Header를 제외하고 n개의 레코드가 담긴다.

기본키(primary key) : 각 행(레코드)의 고유 값, **반드시 설정 필요**, 데이터베이스 관리 및 관계 설정 시 주요하게 활용된다.



## 관계형 데이터베이스 관리시스템 (RDBMS)

Relational Database Management System

관계형 모델을 기반으로 하는 데이터베이스 관리시스템을 의미한다.

MySQL, SQLite, PostgreSQL, ORACLE, MS SQL

### Sqlite Data Type

NULL, INTEGER, REAL, TEXT, BLOB(별다른 타입 없이 그대로 저장)

**Sqlite Type Affinity**

특정 컬럼에 저장하도록 권장하는 데이터 타입



## SQL(Structured Query Language)

관계형데이터베이스 관리시스템 데이터 관리를 위해 설계된 특수 목정 프로그래밍 언어

데이터베이스 스키마 생성 및 수정

자료의 검색 및 관리

데이터베이스 객체 접근 조정 관리



### DDL

데이터 정의 언어(Data Definition language)

CREATE, DROP, ALTER



### DML

데이터 조작 언어(Data Manipulation Language)

INSERT : 새로운 데이터 삽입(추가)

SELECT: 저장되어있는 데이터 조회

UPDATE: 저장되어 있는 데이터 갱신

DELETE: 저장되어있는 데이터 삭제



### DCL

데이터 제어 언어 (Data Control Language)

GRANT, REVOKE, COMMIT, ROLLBACK



# Practice

```bash
$ sqlite3 tutorial.sqlite3
```

```sqlite
sqlite> .database
sqlite> .mode csv
sqlite> .import hellodb.csv examples
sqlite> .tables
example
```

```sqlite
.headers on
.mode column
SELECT * FROM example;
```

```sqlite
.schema classmates
```



### 조회(SELECT)

```sql
SELECT * FROM example;
```

**;까지 하나의 명령(SQL Query)로 간주된다.**



### 테이블 생성 및 제거(CREATE, DROP)

CREATE TABLE

```sql
CREATE TABLE classmates ( id INTEGER PRIMARY KEY, name TEXT );
```



데이터베이스에서 테이블 생성

DROP TABLE

```sql
DROP TABLE classmates;
```

데이터베이스에서 테이블 삭제



테이블 생성 스키마 실습

```sql
CREATE TABLE classmates (
	name TEXT,
    age INTEGER,
    address TEXT
);
```



### CRUD

#### INSERT

테이블에 단일 행(레코드) 삽입

INSERT INTO (컬럼1, 컬럼2) VALUES (값1, 값2, ...);

```sql
INSERT INTO classmates (name, age) VALUES ('홍길동', 23);
```

classmates 테이블에 이름이 홍길동, 나이가 30, 주소가 서울인 데이터를 넣고 SELECT문을 통해 확인해보세요.

```sql
INSERT INTO classmates (name, age, address) VALUES ('홍길동', 30, '서울');
SELECT * FROM classmates;
```

모든 열에 데이터가 있는 경우 column을 명시하지 않아도 된다.

```sql
INSERT INTO classmates VALUES ('홍길동', 30, '서울');
```



id는 기본적으로 출력되지 않는다. 

```sqlite
SELECT rowid, * FROM classmates;
```



비어있는 값이 있으면 안될 경우 NOT NULL 설정이 필요하다.

지우고 새로 만들기

```sql
DROP TABLE classmates;
CREATE TABLE classmates (
    id INTEGER PRIMARY KEY,
	name TEXT NOT NULL,
    age INTEGER NOT NULL,
    address TEXT NOT NULL
);
```

:heavy_check_mark:CREATE TABLE

**PRIMARY KEY를 작성할 때는 INTEGER라고 작성해야한다.**

**다른 column의 경우에는 INT로 작성하여도 동적데이터이기 때문에 INTEGER로 통합된다. **

**위 코드처럼 id를 직접 작성하는 경우 없을 때와 달리 자동으로 입력되지 않는다.**



**방법1**

id를 포함한 모든 value 작성

```sql
INSERT INTO classmates VALUES (1, '홍길동', 30, '서울');
```

**방법2**

각 value에 맞는 column들을 명시적으로 작성

```sql
INSERT INTO classmates (name, age, address) VALUES ('홍길동', 30, '서울');
```



**아래 실습부터는 rowid를 이용한 테이블을 기준으로 SQL작성**

```sql
INSERT INTO classmates VALUES
('홍길동', 30, '서울'),
('김철수', 30, '대전'),
('이싸피', 26, '광주'),
('박삼성', 29, '구미'),
('최전자', 28, '부산');
```



#### READ

테이블에서 데이터를 조회

SELECT문은 SQLite에서 가장 복잡한 문이며 다양한 절(clause)와 함께 사용한다.

ORDER BY, DISTINCT, WHERE, LIMIT, GROUP BY...

##### SELECT와 함께 사용하는 clause

**LIMIT**

쿼리에서 반환되는 행 수를 제한

특정 행부터 시작해서 **OFFSET**키워드와 함께 사용하기도 한다.

**WHERE**

쿼리에서 반환된 행에 대한 특정 검색 조건을 지정한다(IF문과 유사하다.)

**SELECT DISTINCT**

조회 결과에서 중복 행을 제거한다.

DISTINCT절은 SELECT키워드 바로 뒤에 작성해아한다.



모든 컬럼 값이 아닌 특정 컬럼만 조회하기

```sql
SELECT 컬럼1, 컬럼2, ... FROM 테이블 이름;
```

classmates 테이블에서 id, name 컬럼 값만 조회하세요.

```sql
SELECT id, name FROM classmates;
```



##### LIMIT

원하는 수 만큼 데이터 조회하기

```Sql
SELECT 컬럼1, 컬럼2, ... FROM 테이블 이름 LIMIT 숫자;
```

classmates 테이블에서 id, name 컬럼 값을 하나만 조회하세요.

```Sql
SELECT rowid, name FROM classmates LIMIT 1;
```



##### OFFSET

특정 부분에서 원하는 수 만큼 데이터 조회하기

```Sql
SELECT 컬럼1, 컬럼2, ... FROM 테이블 이름 LIMIT 숫자 OFFSET 숫자;
```

classmates 테이블에서 id, name 컬럼 값을 세 번째에 있는 하나만 조회하세요.

```Sql
SELECT rowid, name FROM classmates LIMIT 1 OFFSET 2;
```



**OFFSET**

동일 오브젝트 안에서 오브젝트 처음부터 주어진 요소나 지점까지의 위치변화량을 나타내는 정수형

1. 문자열 'abcedf'에서 문자 'c'는 시작점'a'에서 2의 offset을 지닌다.

2. SELECT * FROM MY_TABLE LIMIT 10 OFFSET 5;

   6번째 행부터 10개의 행을 조회

   0부터 시작



##### WHERE

특정 데이터(조건) 조회하기

```SQL
SELECT 컬럼1, 컬럼2, ... FROM 테이블 이름 WHERE 조건;
```

classmates 테이블에서 id, name 컬럼 값 중에 주소가 서울인 경우의 데이터를 조회하세요.

```sql
SELECT rowid, name FROM classmates WHERE address = '서울';
```



##### DISTINCT

특정 칼럼을 기준으로 중복없이 가져오기

```SQL
SELECT DISTINCT 컬럼1, 컬럼2, ... FROM 테이블명;
```

classmates 테이블에서 age값 전체를 중복없이 조회하세요.

```sql
SELECT DISTINCT age FROM classmates;
```



#### DELETE

테이블에서 행을 제거



조건을 통해 특정 레코드 삭제하기

**중복 불가능한(UNIQUE) 값이 rowid를 기준으로 삭제한다.**

```Sql
DELETE FROM 테이블 이름 WHERE 조건;
```

classmates 테이블에 id가 5인 레코드를 삭제하세요.

```sql
DELETE FROM classmates WHERE rowid=5;
```



##### AUTOINCREMENT

삭제하고 난 후 SQLite는 기본적으로 id를 재사용한다.

그러나 Django는 재활용을 하지 않고 위 경우 id 6에 값이 들어가게 된다.

SQLite가 사용되지 않은 값이나 이전에 삭제된 행의 값을 재사용하는 것을 방지한다.

```sql
CREATE TABLE (
	id INTEGER PRIMARY KEY AUTOINCREMENT,
    ...
);
```

django에서 기본 값으로 사용되는 설정 AUTOINCREMENT, NOT NULL



#### UPDATE

기존 행의 데이터를 수정

SET caluse에서 테이블의 각 열에 대해 새로운 값을 설정한다.

조건을 통해 특정 레코드 수정하기

**중복 불가능한(UNIQUE)값인 rowid를 기준으로 수정하자**

```sql
UPDATE 테이블이름 SET 컬럼1 = 값1, 컬럼2 = 값2, ... WHERE 조건;
```

classmates 테이블에 id가 5인 레코드를 수정하세요. 이름을 홍길동으로, 주소를 제주도로 바꿔주세요.

```sql
UPDATE classmates SET name='홍길동', address='제주도' WHERE rowid=5;
```



### WHERE

WHERE 복습

#### 특정 조건으로 데이터 조회하기

users 테이블에서 age가 30 이상인 유저의 모든 컬럼 정보를 조회하세요.

```sql
SELECT * FROM users WHERE age>=30;
```

users 테이블에서 age가 30 이상인 유저의 이름만 조회하세요.

```sql
SELECT first_name FROM users WHERE age>=30;
```

users 테이블에서 age가 30 이상이고 성이 '김'인 사람의 나이와 성만 조회하세요.

```sql
SELECT age, last_name FROM users WHERE age>= 30 AND last_name='김';
```



### SQLite Aggregate Functions

집계 함수

값 집합에 대한 계산을 수행하고 단일 값을 반환한다.

* 여러 행으로부터 하나의 결괏값을 반환하는 함수

SELECT 구문에서만 사용된다.

#### COUNT

테이블 전체 행 수를 구한다.

그룹의 항목 수를 가져온다.

레코드의 개수 조회하기

```sql
SELECT COUNT (컬럼) FROM 테이블 이름;
```

users 테이블의 레코드 총 개수를 조회하세요.

```sql
SELECT COUNT(*) FROM users;
```



#### AVG

age 컬럼 전체 평균 값을 구한다.

모든 값의 평균을 계산한다.

#### MAX

그룹에 있는 모든 값의 최대값을 가져온다.

#### MIN

그룹에 있는 모든 값의 최소값을 가져온다.

#### SUM

모든 값을 합을 계산한다.

```sql
SELECT AVG(컬럼) FROM 테이블 이름;
SELECT MIN(컬럼) FROM 테이블 이름;
SELECT MAX(컬럼) FROM 테이블 이름;
SELECT SUM(컬럼) FROM 테이블 이름;
```

위 함수들은 기본적으로 해당 컬럼이 숫자(INTEGER)일 때만 사용가능하다.



30살 이상인 사람들의 평균나이를 구하세요.

```sql
SELECT AVG(age) FROM users WHERE age>=30;
```

계좌 잔액(balance)이 가장 높은 사람과 그 액수를 조회하세요.

```Sql
SELECT first_name, MAX(balance) FROM users;
```

나이가 30 이상인 사람의 계좌 평균 잔액을 조회하세요.

```Sql
SELECT AVG(balance) FROM users WHERE age>=30;
```



### LIKE

LIKE operator

패턴 일치를 기반으로 데이터를 조회하는 방법

SQLite는 패턴 구성을 위한 2개의 wildcards를 제공한다.

* %(percent sign)
  * 0개 이상의 문자
  * 이 자리에 문자열이 있을 수도, 없을 수도 있다.
* _(underscore)
  * 임의의 단일 문자
  * 반드시 이 자리에 한 개의 문자가 존재해야 한다.

#### sildcard character

파일을 지정할 때, 구체적인 이름 대신에 여러 파일을 동시에 지정할 목적으로 사용하는 특수 기호



LIKE statement

패턴을 확인하여 해당하는 값을 조회하기

```sql
SELECT * FROM 테이블 WHERE 컬럼 LIKE '와일드카드패턴';
```



| 와일드카드패턴   | 의미                                          |
| ---------------- | --------------------------------------------- |
| 2%               | 2로 시작하는 값                               |
| %2               | 2로 끝나는 값                                 |
| %2%              | 2가 들어가는 값                               |
| _2%              | 아무 값이 하나 있고 두 번째가 2로 시작하는 값 |
| 1____            | 1로 시작하고 총 4자리인 값                    |
| 2\_%\_% / 2\_\_% | 2로 시작하고 적어도 3자리인 값                |



#### wildcards 실습

users 테이블에서 나이가 20대인 사람만 조회하세요.

```sql
SELECT * FROM users WHERE age LIKE='2_';
```

users 테이블에서 지역 번호가 02인 사람만 조회하세요.

```sql
SELECT * FROM users WHERE phone LIKE='02-%';
```

users 테이블에서 이름이 '준'으로 끝나는 사람만 조회하세요.

```sql
SELECT * FROM users WHERE first_name LIKE='%준';
```

users 테이블에서 중간 번호가 5114인 사람만 조회하세요.

```sql
SELECT * FROM users WHERE phone LIKE='%-5114-%';
```



### ORDER BY

조회 결과 집합을 정렬

SELECT문에 추가하여 사용한다.

정렬 순서를 위한 2개의 keyword제공

* ASC: 오름차순(default)
* DESC: 내림차순

```sql
SELECT * FROM 테이블 이름 ORDER BY 컬럼1 ASC;
SELECT * FROM 테이블 이름 ORDER BY 컬럼1, 컬럼2 DESC;
```

users에서 나이순으로 오름차순 정렬하여 상위 10개만 조회하세요.

```sql
SELECT * FROM users ORDER BY age ASC LIMIT 10;
```

나이 순, 성 순으로 오름차순 정렬하여 상위 10개만 조회하세요.

```sql
SELECT * FROM users ORDER BY age, last_name ASC LIMIT 10;
```

계좌 잔액 순으로 내림차순 정렬하여 해당 유저의 성과 이름을 10개만 조회하세요.

```sql
SELECT last_name, fist_name FROM users ORDER BY balance DESC LIMIT 10;
```



### GROUP BY

행 집합에서 요약 행 집합을 만든다.

SELECT문의 optional 절이다.

**문장에 WHERE 절이 포함된 경우 반드시 WHERE 절 뒤에 작성한다.**

지정된 기준에 따라 행 세트를 그룸으로 결합한다.

데이터를 요약하는 상황에 주로 사용한다.

```sql
SELECT 컬럼1, aggregate_function(컬럼2) FROM 테이블 이름 GROUP BY 컬럼1, 컬럼2;
```



users에서 각 성(last_name)씨가 몇 명씩 있는지 조회하세요

```sql
SELECT last_name, COUNT(*) FROM users GROUP BY last_name;
```

AS를 활용해서 COUNT에 해당하는 컬럼 명을 바꿔서 조회할 수 있다.

```sql
SELECT last_name, COUNT(*) AS name_count GROUP BY last_name;
```



### ALTER TABLE

title과 content라는 컬럼을 가진 articles라는 이름의 table을 새롭게 만들어보세요.

(두 컬럼 모두 비어 있으면 안되며, rowid를 사용합니다.)

```sql
CREATE TABLE articles (
	title TEXT NOT NULL,
    content TEXT NOT NULL
);
```

articles 테이블에 값을 추가하세요.

title은 '1번제목', content는 '1번내용'

```sql
INSERT INTO articles (title, content) VALUES ('1번제목', '1번내용');
```



#### ALTER TABLE statement

ALTER TABLE의 3가지 기능

1. table 이름 변경
2. 테이블에 새로운 column 추가
3. [참고] column 이름 수정 (new in sqlite 3.25.0)
4. DROP column (new in sqlite 3.35.0)

```sql
ALTER TABLE 테이블 이름 RENAME COLUMN current_name TO new_name;
```



ALTER TABLE 실습

방금 만든 테이블의 이름을 변경하세요.

```sql
ALTER TABLE articles RENAME TO news;
```

방금 만든 테이블에 새로운 컬럼을 추가하세요.

```sql
ALTER TABLE article ADD COLUMN created_at TEXT NOT NULL;
```

테이블에 기존 레코드가 있는 경우 Error가 발생한다.

**테이블에 있던 기존 레코드들에는 새로 추가할 필드에 대한 정보가 없다. NOT NULL형태의 컬럼은 추가 불가능하다.**

해결 방법 2가지

1. NOT NULL 설정 없이 추가하기

   ```sql
   ALTER TABLE news ADD COLUMN create_at TEXT;
   ```

2. 기본 값(default) 설정하기

   ```sql
   ALTER TABLE news ADD COLUMN subtitle TEXT NOT NULL DEFAULT '소제목';
   ```

   
