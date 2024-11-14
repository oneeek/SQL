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


- **특징** <br/>
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

- 데이터 저장, COMMIT을 수행하면 COMMIT 이전 수행된 DML은 모두 저장되며 되돌릴 수 없음



