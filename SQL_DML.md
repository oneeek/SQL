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
# 단일컬럼 수정

UPDATE 테이블명
SET 수정할컬럼명1 = 수정값1, 수정할컬럼명2 = 수정값2, ...
WHERE 조건;
```




















