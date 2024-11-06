## SQL 기본문법

- **DDL** : 데이터 정의어 (테이블 생성, 삭제, 변경)
- **DML** : 데이터 조작어 (데이터 조회, 추가, 수정)
- **DCL** : 데이터 제어어 (권한 부여, 회수)
- **TCL** : 트랜잭션 제어어 (영구 반영, 작업 취소 및 복구)


## DML
```SQL
SELECT [ALL/DISTINCT] 속성명
FROM 테이블명
WHERE 검색조건
GROUP BY 속성명
HAVING 검색조건
ORDER BY 속성명 [ASC/DESC]
```
- [x] ALL : 중복 허용 / DISTINCT : 중복 허용 X
- [x] ASC : 오름차순(기본) / DESC : 내림차순
- [x] WHERE : 그룹화 전 조건 / HAVING : 그룹화 후 조건


### SELECT/FROM
> 여러 속성 조회
```SQL
SELECT 속성1, 속성2
FROM 테이블;
```

> 모든 속성 조회
```SQL
SELECT *
FROM 테이블;
```

> 중복 없이 속성 조회
```SQL
SELECT DISTINCT 속성
FROM 테이블;
```


### WHERE
> 조건식 종류

분류|종류
:---:|:---:
비교 | =, <>, <, <=, >, >=
범위 | BETWEEN
집합 | IN, NOT IN
패턴 | LIKE
NULL | IS NULL, IS NOT NULL
복합 | AND, OR, NOT

> 주소가 입력되지 않은 고객의 이름 검색
```SQL
SELECT name
FROM Customer
WHERE address IS NULL;
```


### ORDER BY
> 고객 ID를 기준으로 내림차순 검색
```SQL
SELECT *
FROM Customer
ORDER BY ID DESC;
```


### GROUP BY/HAVING
> 고객별 주문 수량이 2개 이상인 고객 검색
```SQL
SELECT ID, COUNT(*)
FROM Order
GROUP BY ID
HAVING COUNT(ID) >= 2;
```
