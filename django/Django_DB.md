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
)
```

