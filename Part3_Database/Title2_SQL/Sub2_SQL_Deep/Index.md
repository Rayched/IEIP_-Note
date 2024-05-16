
## Index

- 데이터를 빠르게 찾을 수 있는 수단
- 테이블에 대한 조회 속도를 높여 주는 자료 구조
- `Index`는 테이블의 특정 레코드 위치를 알려주는 용도로 사용하며 <br/>
	자동으로 생성되지 않는다.
- `Primary Key`가 적용된 Column은 자동으로 `Index`가 생성된다.

---

#### Index 생성

``` sql
CREATE INDEX A ON STUDENT(ID);
/*CREATE INDEX '인덱스_명 ON '테이블_명(Column_Name)';*/
```

- 위의 명령어를 통해 `Index` 생성할 수 있으며, `UNIQUE` 키워드를 추가해서 <br/>
	인덱스가 걸린 Column에 중복 값이 들어가지 않게 할 수 있다.

``` sql
CREATE UNIQUE INDEX A ON STUDENT(ID);
/* UNIQUE는 필수가 아닌 선택 사항 */
```

---

#### Index 변경 및 삭제

``` sql
/*Index 변경*/
ALTER INDEX A ON STUDENT(ID);
ALTER UNIQUE INDEX A ON STUDENT(ID);
/*ALTER INDEX '인덱스_명' ON '테이블_명(Column)'*/

/*Index 삭제*/
DROP INDEX A;
/*DROP INDEX '인덱스_명*/
```

- `Index`를 Table의 종속 구조로 간주, 삭제 시 테이블 변경 명령어가 사용된다.
- 일부 DBMS에서는 `Index` 변경 Query가 지원하지 않는 경우도 있기 때문에  <br/>
	`ALTER` 문으로 변경하지 않고, 기존 `Index` 삭제하고 <br/>
	신규 `Index` 생성하는 방식도 존재한다.

---

