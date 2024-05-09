
### 관계 대수

- 관계형 DB에서 원하는 정보와 그 정보를 어떻게 유도하는 가를 기술하고 <br/>
	관계로 표현된 데이터를 취급하는 대수적인 연산 체계이자 절차적 정형 언어
- 관계 대수 연산자는 `일반 집합 연산자`, `순수 관계 연산자`로 나뉘어 진다.

---
#### 일반 집합 연산자

- 수학의 집합 개념을 Relation에 적용한 연산자

| 연산자               | 표현          | 설명                                                     |
| ----------------- | ----------- | ------------------------------------------------------ |
| 합집합               | **`R ∪ S`** | 합병 가능한 두 Relation R과 S의 합집합                            |
| 교집합               | **`R ∩ S`** | Relation R과 S에 속하는 모든 Tuple로 결과 Relation 구성            |
| 차집합               | **`R - S`** | R에 존재하고, S에 존재하지 않는 Tuple로 결과 Relation 구성              |
| CARTESIAN Product | **`R X S`** | R과 S에 속한 모든 Tuple 연결해 만들어진 <br/>새로운 Tuple로 Relation 구성 |

---

#### 순수 관계 연산자

* 관계 DB에 적용할 수 있도록 특별히 개발한 관계 연산자

| 연산자      | 표현               | 설명                                         |
| -------- | ---------------- | ------------------------------------------ |
| Select   | **`σ_조건(R)`**    | Relation R에서 조건을 만족하는 Tuple 반환             |
| Project  | **`π_속성리스트(R)`** | R에서 주어진 속성들의 값으로만 구성된 Tuple 반환             |
| Join     | **`R \|X\| S`**  | 공통 속성을 이용해 R과 S의 Tuple들을 연결해 만들어진 Tuple 반환 |
| Division | **`R ÷ S`**      | Relation S의 모든 Tuple과 관련 있는 R의 tuple 반환    |

---

<br/>

### 관계 해석

- 관계 해석은 'Tuple 관계 해석', 'Domain 관계 해석' 하는 비절차적 언어
- Predicate Calculas (`프레디킷 해석`)에 기반한 언어, 비절차적 언어 <br/>
	(비절차적 언어 => 원하는 정보가 무엇이라는 것만 선언)
	
- Domain 관계 해석 => 원하는 Relation을 ***`도메인 해석식`***으로 정의하는 표기법

```
도메인 해석식 Domain Calculus Expression
- Tuple 변수 대신 Domain 변수를 사용하고
- 각 변수는 한 Attribute의 Domain을 범위로 갖는 해석식
```

---

#### Tuple 관계 해석

- 원하는 Relation을 `튜플 해석식 Tuple Calculas Expression`으로 정의하는 표기법
- `튜플 변수`, `한정 Attribute`, `원자식`, `정형식`로 구성됐다.
- 원자식 간 연산을 위해 논리 기호를 사용한다.

| 구분  | 구성 요소                                 | 기호      | 설명                                         |
| --- | ------------------------------------- | ------- | ------------------------------------------ |
| 연산자 | OR                                    | **`∨`** | 원자식 간 "또는"이라는 관계로 연결                       |
| 연산자 | AND                                   | **`∧`** | 원자식 간 "그리고"라는 관계로 연결                       |
| 연산자 | NOT                                   | **`￢`** | 원자식 부정                                     |
| 정량자 | `전칭 정량자`<br/>`Universal Quantifier`   | **`∀`** | 모든 가능한 Tuple <br/>("for all"로 읽음)          |
| 정량자 | `존재 정량자`<br/>`Existential Quantifier` | **`∃`** | 어떤 Tuple 하나라도 존재 <br/>("there exists"로 읽음) |

---

### System Catalog

- DB에 저장되는 Table, View, Index, 접근 권한 등에 대한 정보를 저장하는 DB
- DDL 실행으로 생성되는 `Table`, `View`, `Index`, `Package`, `Access Modifier`등 <br/>
	DB 구조 및 통계 정보를 저장한다.

#### 특징

- Data Dictionary (자료 사전)라고도 부른다.
- 저장된 정보 == Metadata
- Table로 구성되어 있기 때문에 SQL 이용하여 내용을 검색할 수 있다.
- `INSERT`, `DELETE`, `UPDATE` 문으로 System Catalog 갱신하는 것은 허용되지 않음 <br/>
	(시스템 카탈로그는 DBMS가 스스로 생성하고 유지하기 때문)
- 사용자가 SQL 문을 실행, 기본 Table, View, Index 등에 변화를 주면 <br/>
	시스템이 자동으로 갱신된다.
- 보통의 Relation, Index, User 등에 정보를 포함할 뿐 아니라 <br/>
	위치 / 중복 투명성을 제공하기 위해 필요한 모든 제어 정보가 포함된다.

---

