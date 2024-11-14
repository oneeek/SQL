*홍쌤의 데이터랩 SQLD_NEW 강의를 참고한 정리

## SQL 기본문법

구분|종류
:---:|:---:
**DDL** | CREATE, ALTER, DROP, TRUNCATE
**DML** | INSERT, DELETE, UPDATE, MERGE
**DCL** | GRANT, REVOKE
**TCL** | COMMIT, ROLLBACK
**DQL** | SELECT



## DQL
```SQL
SELECT [ALL/DISTINCT] 컬럼명
FROM 테이블명
WHERE 검색조건
GROUP BY 컬럼명
HAVING 검색조건
ORDER BY 컬럼명 [ASC/DESC]
```
- [x] ALL : 중복 허용 / DISTINCT : 중복 허용 X
- [x] ASC : 오름차순(기본) / DESC : 내림차순
- [x] WHERE : 그룹화 전 조건 / HAVING : 그룹화 후 조건


### SELECT/FROM

```SQL
# 여러 컬럼 조회
 
SELECT 컬럼1, 컬럼2
FROM 테이블;
```
