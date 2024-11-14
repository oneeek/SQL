*홍쌤의 데이터랩 SQLD_NEW 강의를 참고한 정리

## SQL 기본문법

구분|종류
:---:|:---:
**DDL** | CREATE, ALTER, DROP, TRUNCATE
**DML** | INSERT, DELETE, UPDATE, MERGE
**DCL** | GRANT, REVOKE
**TCL** | COMMIT, ROLLBACK
**DQL** | SELECT



## DML

- [x] 종류 : INSERT, UPDATE, DELETE, MERGE
- [x] 저장(COMMIT) 혹은 취소(ROLLBACK) 반드시 필요


### INSERT

- 한 번에 한 행만 입력 가능(SQL Server는 여러 행 동시 입력 가능)
- 하나의 컬럼에는 한 값만 입력 가능
- 컬럼별 데이터 타입과 사이즈에 맞게 입력
- 일부 컬럼만 입력 가능, 작성하지 않은 컬럼은 NULL이 입력(NOT NULL 컬럼의 경우 오류 발생)


```SQL
# 문법

INSERT INTO 테이블명 VALUES(값1, 값2, ...);
INSERT INTO 테이블명(컬럼1, 컬럼2) VALUES(값1, 값2);
```


### UPDATE

- 컬럼 단위, 다중 컬럼 수정 가능


```SQL
# 단일컬럼 수정

UPDATE 테이블명
SET 수정할컬럼명 = 수정값
WHERE 조건;
```

```SQL
# 다중컬럼 수정

UPDATE 테이블명
SET 수정할컬럼명1 = 수정값1, 수정할컬럼명2 = 수정값2, ...
WHERE 조건;
```
```SQL
# 다중컬럼 수정(서브쿼리 사용)

UPDATE 테이블명
SET (수정할컬럼명1, 수정할컬럼명2) = (SELECT 수정값1, 수정값2)
WHERE 조건;
```


### DELETE

```SQL
# 문법

DELETE[FROM] 테이블명
[WHERE 조건];
```


### MERGE

- 참조 테이블과 동일하게 맞추기(참조 테이블의 값으로 수정 등)
- INSERT, UPDATE, DELETE 동시 수행


```SQL
# 문법

MERGE INTO 테이블명
USING 참조테이블명
ON (연결조건) #괄호필수
WHEN MATCHED THEN
     UPDATE
     SET 수정내용
     DELETE (조건)
WHEN NOT MATCHED THEN
     INSERT VALUES(값1, 값2, ...);
```



## TCL

- [x] DML에 의해 조작된 결과를 제어하는 명령어, DML 수행 후 트랜잭션을 정상 종료하지 않는 경우 LOCK 발생
- [x] 분할 할 수 없는 최소 단위 (ALL OR NOTHING)
- [x]  **특징**
  원자성(atomicity): 트랜잭션 정의된 연산 모두 성공적으로 실행 or 전혀 실행되지 않은 상태로 있어야 함 <br/>
  일관성(consistency): 트랜잭션 실행 전 데이터베이스 내용이 잘못되어 있지 않다면, 실행 후에도 잘못이 있으면 안 됨 <br/>
  고립성(isolation): 트랜잭션 실행 중 다른 트랜잭션의 영향을 받아 잘못된 결과를 만들어서는 안 됨 <br/>
  지속성(durability): 트랜잭션이 성공적으로 수행되면, 수정된 데이터베이스 내용 영구 저장 <br/>



### COMMIT

- 데이터 저장, COMMIT을 수행하면 COMMIT 이전 수행된 DML은 모두 저장되며 되돌릴 수 없음


### ROLLBACK

- 데이터 변경 취소, 최종 COMMIT 시점 이전까지 원복 가능
- SAVEPOINT를 설정하여 최종 COMMIT 이후 원하는 시점으로의 원복 가능
- SAVEPOINT 이전 수행한 UPDATE는 취소되지 않음

```SQL
# SAVEPOINT 설정

SAVEPOINT savepoint_name;
```



## DDL

- [x] 종류 : CREATE(객체 생성), ALTER(객체 변경), DROP(객체 삭제), TRUNCATE(데이터 전부 삭제)
- [x] AUTO COMMIT, 명령어 수행 시 즉시 저장(원복 불가)


### CREATE

- 테이블이나 인덱스와 같은 객체를 생성하는 명령어
- 테이블 생성 시 테이블명, 컬럼명, 컬럼순서, 컬럼크기, 컬럼 데이터타입 정의 필수
- 테이블 생성 시 소유자 명시 가능(생략 시 명령어 수행 계정 소유)

```SQL
# 테이블 생성 문법

CREATE TABLE [소유자.]테이블명(
컬럼1 테이터타입 [DEFAULT 기본값] [제약조건],
컬럼2 테이터타입 [DEFAULT 기본값] [제약조건]
);
```

```SQL
# 테이블 복제 문법

CREATE TABLE 테이블명
AS
SELECT * FROM 복제테이블명;
```

```SQL
# 테이블 구조만 복제, 항상 거짓인 조건을 전달하면 테이블 구조만 복제 가능

CREATE TABLE 테이블명
AS
SELECT *
FROM 복제테이블명
WHERE 1=2;
```

```SQL
# 테이블 복제 시 컬럼명 변경

CREATE TABLE 테이블명(새컬럼명1, 새컬럼명2) 
AS
SELECT 컬럼명1, 컬럼명2
FROM 복제테이블명;
```


> 데이터 타입

데이터 타입|설명
:--|:--
CHAR(n) | 사이즈 전달 필수, 고정형 문자 타입(빈자리는 공백을 채워 사이즈만큼 데이터 입력)
VARCHAR2(n) | 사이즈 전달 필수, 가변형 문자 타입(사이즈 보다 작은 문자값 그대로 입력)
NUMBER(p, s) | 사이즈 생략 가능, 숫자형으로 p는 총 자릿수/ s는 소수점 자릿수
DATE | 사이즈 전달 불가, 날짜형

- SQL Server <br/>
  VARCHAR2 > VARCHAR <br/>
  NUMBER > NUMERIC <br/>
  문자타입 사이즈 생략 가능 (생략 시 1) <br/>



### ALTER

- 테이블 구조 변경(컬럼명, 컬럼 데이터타입, 컬럼 사이즈, 컬럼 삭제, 컬럼 추가, 제약조건 등)
- 컬럼순서 변경 불가, 재생성으로 해결


1. 컬럼 추가
   - 새로 추가된 컬럼 위치는 맨 마지막(중간 위치에 추가 불가)
   - 여러 컬럼 동시 추가 가능, 반드시 괄호 사용
   - 데이터가 있는 테이블에 컬럼 추가 시 NOT NULL 속성 전달 불가, 데이터가 없는 테이블은 가능
   - DEFAULT를 선언하면 NOT NULL 속성 컬럼 추가 가능

```SQL
# 문법

ALTER TABLE 테이블명 ADD 컬럼명 데이터타입 [DEFAULT] [제약조건];
ALTER TABLE 테이블명 ADD (컬럼명1 데이터타입, 컬럼명2 데이터타입);
```

2. 컬럼 변경
   - 사이즈 변경: 증가는 항상 가능, 축소는 기존 데이터의 최대 사이즈 만큼 가능
   - 동시 변경 가능, 반드시 괄호 사용

```SQL
# 문법

ALTER TABLE 테이블명 MODIFY (컬럼명1 데이터타입(사이즈), 컬럼명2 데이터타입(사이즈));
ALTER TABLE 테이블명 MODIFY (컬럼명 DEFAULT DEFAULT값);
```

3. 컬럼 이름 변경
   - 항상 가능
   - 동시 이름 변경 불가

```SQL
# 문법

ALTER TABLE 테이블명 RENAME COLUMN 기존컬럼명 TO 새컬럼명;
```


3. 컬럼 삭제
   - 항상 가능, 데이터 있어도 삭제 가능(복구 불가)
   - 동시 삭제 불가

```SQL
# 문법

ALTER TABLE 테이블명 DROP COLUMN 컬럼명;
```


### DROP

- 객체(테이블, 인덱스 등) 삭제
- DROP 후 조회 불가

```SQL
# 문법, PURGE로 삭제 시 RECYCLEBIN에서 조회 불가

DROP TABLE 테이블명 [PURGE];
```


### TRUNCATE

- 테이블 구조 남기고 데이터는 즉시 삭제, 즉시 반영(AUTO COMMIT)
- RECYCLEBIN에 남지 않음
- TRUNCATE 후 조회 가능, 데이터는 없음

```SQL
# 문법

TRUNCATE TABLE 테이블명;
```


- [x] **`DEFAULT`**
- 값이 생략될 때 자동으로 부여되는 값
- INSERT에서 NULL 직접 입력 시, DEFAULT값 대신 NULL 입력
- 이미 데이터가 존재하는 테이블에 DEFAULT값 선언 시, 기존 데이터는 수정 X
- DEFAULT값 해제 시, DEFAULT값을 NULL로 선언


- [x] **`제약조건`**
- 데이터 무결성을 위해 컬럼에 생성하는 데이터의 제약 장치
- 테이블 생성 시 정의 가능, 컬럼 추가 시 정의 가능, 이미 생성된 컬럼에 제약조건만 추가 가능




















