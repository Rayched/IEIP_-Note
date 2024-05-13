
## 데이터 정의어 (DDL)
- `Data Definition Language`의 약어
- 말 그대로 **"데이터를 정의하는 언어"**, 데이터를 담는 그릇을 정의하는 언어
- DB 생성하고, 데이터를 담을 Table을 정의하는 데 사용되는 명령어
- 특정 구조를 생성(Create), 삭제(Delete), 이름을 바꾸는 등(Update) <br/>
    데이터 구조와 관련된 명령어
- DDL의 대상에는 `Domain`, `Schema`, `Table`, `View`, `Index`가 있다.

| 대상       | 설명                                                             |
| -------- | -------------------------------------------------------------- |
| `Domain` | 하나의 속성이 가질 수 있는 원자 값들의 집합 <br/>속성의 데이터 타입과 크기, 제약 조건 등의 정보     |
| `Schema` | DB의 구조, 제약 조건 등의 정보를 담고 있는 기본적인 구조<br/>`외부/개념/내부` 3 계층으로 구성됐다. |
| `Table`  | 데이터 저장 공간                                                      |
| `View`   | 하나 이상의 물리 테이블에서 유도되는 가상의 테이블                                   |
| `Index`  | 검색을 빠르게 하기 위한 데이터 구조                                           |

```
Schema

1. 외부 스키마
- 사용자나 개발자 관점에서 필요로 하는 DB의 논리적 구조
- 사용자 View를 나타내며, Sub Schema라고도 불린다.

2. 개념 스키마
- DB의 전체적인 논리 구조
- 전체적인 View를 나타낸다.
- 개체 간 관계, 제약 조건, 접근 권한, 무결성, 보안에 대해 정의

3. 내부 스키마
- 물리적 저장장치 관점에서 보는 DB 구조
- 실제로 DB에서 저장될 레코드 형식을 정의하고, 저장 데이터 항목의 표현 방법
  내부 레코드의 물리적 순서 등을 표현한다.
- Storage Schema (저장 스키마)라고도 불린다.
```

<br/>

``` mySQL
#DDL 예제

#create 문
#DB Object를 생성하는 명령어
#a2 DB 생성
CREATE DATABASE a2;

USE a2;

#deps(사원) table 생성
CREATE TABLE deps (
	`name` VARCHAR(10) NOT NULL,
	id INT NOT NULL PRIMARY KEY,
	`date` DATE NOT NULL
);

#Drop 문
#DB Object 삭제
#DB, Table 삭제 가능
DROP DATABASE IF EXISTS a2;
DROP TABLE deps;

# alter 문
# DB Object 변경하는 명령어

#Add, modify, drop, rename 사용 가능
#Add: 테이블에 Column 추가
#modify: 테이블 column 수정
#drop: column 삭제
#rename: column 이름 변경

#birth(생년월일), testcol 컬럼 생성
ALTER TABLE deps ADD COLUMN birth INT UNSIGNED NOT NULL;
ALTER TABLE deps ADD COLUMN testcol VARCHAR(100) NOT NULL UNIQUE;

#id 컬럼의 타입을 int unsigned 변경
ALTER TABLE deps MODIFY COLUMN id INT UNSIGNED NOT NULL;

#testcol 컬럼 삭제하기
ALTER TABLE deps DROP COLUMN testcol;

#Truncate 문: db object 내용 삭제
#deps table 추가한 데이터 전부 삭제
TRUNCATE TABLE deps
```

---

## 데이터 조작어 (DML) ☆☆☆

- Data Manipulation Language 약어
- DB에 저장된 자료들을 `CRUD`하는 언어이다. <br/>
	`create (생성)`, `read(조회)`, `update(수정)`, `delete(삭제)`

| 구문       | 동작     | 설명                                                                         |
| -------- | ------ | -------------------------------------------------------------------------- |
| `SELECT` | 데이터 조회 | 해당 테이블을 구성하는 Tupe 중에서 전체 또는 조건을 만족하는 <br/>튜플을 검색하여 메모리 상에 임시 테이블로 구성하는 명령문 |
| `INSERT` | 데이터 생성 | 해당 테이블에 새로운 데이터를 삽입할 때 사용하는 명령어                                            |
| `UPDATE` | 데이터 수정 |                                                                            |
| `DELETE` | 데이터 삭제 |                                                                            |
|          |        |                                                                            |

``` mysql
# Insert
# 테이블에 데이터 추가할 때 사용하는 구문
#insert into [테이블 명] set [Column에 추가할 데이터's];

# 임의의 데이터 3개 추가
INSERT INTO deps SET 
`name`="홍길동", id=1234, `date`=NOW(), birth=19980131;

INSERT INTO deps SET 
`name`="홍길순", id=5678, `date`=NOW(), birth=20000310;

INSERT INTO deps SET 
`name`="임꺽정", id=9012, `date`=NOW(), birth=19970514;
```

``` mysql
# select
# 해당 테이블 컬럼 조회할 수 있음.
# '*' 설정하면  해당 테이블의 전체 컬럼 조회함
# select [조회할 Column] from [테이블 명};


SELECT `name`, birth FROM deps;
# deps table의 `name`, birth column 조회

SELECT * FROM deps;
# deps table의 column 전체 조회
```

``` mysql
# Update
# 해당 테이블에서 특정 데이터를 수정할 때 사용하는 구문
# update [테이블 명] set [수정할 데이터]

UPDATE deps SET `name`="James" WHERE id=5678;
# id가 5678인 행의 `name`을 James로 수정
UPDATE deps SET birth=20000131 WHERE id=1234;
# id가 1234인 행의 birth(생년월일)을 20000131로 변경
```

``` mysql
# delete
# 테이블에서 특정 데이터 행을 삭제할 때 사용하는 구문
# delete from [테이블 명] where 조건식

DELETE FROM deps WHERE id=5678;
# deps 테이블에서 id가 5678인 행을 찾아서 삭제한다.
```

---

#### `where`, `order by`

| 구문         | 설명                                                                                                                        |
| ---------- | ------------------------------------------------------------------------------------------------------------------------- |
| `where`    | 검색할 조건을 설정하는 문법 <br/>`SELECT * FROM deps WHERE 'date'="2024-05-13";`<br/>`deps 테이블에서 date(입사일)가 "2024-05-13"인 행 전체 조회한다.` |
| `order by` | 속성 값을 정렬하고자 할 때 사용하는 문법 <br/>`ASC`, `DESC` 키워드 생략 시 오름차순으로 정렬한다.<br/>`ASC`: 오름차순 정렬 / `DESC`: 내림차순 정렬                     |


---

## 데이터 제어어 (DCL)

- Data Control Language
- DB 관리자가 데이터 보안, 무결성 유지, 병행 제어, 회복을 위해 사용하는 언어
- DCL의 기능은 다음과 같다.

| 기능       | 설명                                                                         |
| -------- | -------------------------------------------------------------------------- |
| 데이터 보안   | 불법적인 사용자로부터 데이터를 보호하는 기능                                                   |
| 무결성 유지   | 데이터의 정확성과 일관성을 유지하는 기능                                                     |
| 병행 수행 제어 | 여러 Transaction 수행할 때, 트랜잭션들이 DB의 일관성을 <br/>파괴하지 않도록 트랜잭션 간의 상호 작용을 제어하는 기능 |
| 회복       | DB 장애가 발생할 경우, 장애 발생 이전 상태로 복원하는 기능                                        |

---
### DCL 명령어 ☆☆☆

#### `GRANT`

- DBA(DB 관리자)가 사용자에게 DB에 대한 권한을 부여하는 명령어
- `grant` 구문 마지막에 `with grant option` 추가하면 권한이 필요한 <br/>
	다른 사용자에게 권한을 부여할 수 있는 권한을 부여한다.

``` mysql
GRANT 권한 TO 사용자
#관리자가 사용자에게 테이블/뷰/프로시저 등을 생성 및 삭제하는 권한 부여한다.
#시스템 권한 부여

GRANT 권한 ON 테이블 명 TO 사용자
#관리자가 사용자에게 테이블을 CRUD와 프로시저 실행을 할 수 있는 권한 부여
#모든 사용자에게 권한을 부여할 때, 사용자에 PUBLIC 사용한다
```

#### `REVOKE`

- DBA가 사용자에게 부여했던 권한을 회수하기 위한 명령어
- `revoke` 구문에 `cascade constraints` 추가하면 <br/>
	`with grant option`으로 부여된 사용자들의 권한까지 회수 가능하다.

``` mysql
REVOKE 권한 FROM 사용자
#관리자가 사용자에게 `테이블/뷰/프로시저` 등을
#생성하고 삭제할 수 있는 권한을 회수하는 구문

REVOKE 권한 ON 테이블 FROM 사용자
#관리자가 사용자에게 특정 테이블을 CRUD하고
#프로시저 실행할 수 있었던 권한을 회수하는 구문
```

---
