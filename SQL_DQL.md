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
> 여러 컬럼 조회
```SQL
SELECT 컬럼1, 컬럼2
FROM 테이블;
```

> 모든 컬럼 조회
```SQL
SELECT *
FROM 테이블;
```

> 중복 없이 컬럼 조회
```SQL
SELECT DISTINCT 컬럼
FROM 테이블;
```


> 프로그래머스 <잡은 물고기의 평균 길이 구하기>
```SQL
SELECT ROUND(AVG(IFNULL(LENGTH, 10)),2) AS AVERAGE_LENGTH
FROM FISH_INFO;
```


### WHERE
> 조건식 종류

구분|종류
:---:|:---:
비교 | =, <>, <, <=, >, >=
범위 | BETWEEN
집합 | IN, NOT IN
패턴 | LIKE
NULL | IS NULL, IS NOT NULL
복합 | AND, OR, NOT

> 프로그래머스 <이름이 있는 동물의 아이디>
```SQL
SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME IS NOT NULL;
```


### ORDER BY
>고객 ID를 기준으로 내림차순 검색
```SQL
SELECT *
FROM Customer
ORDER BY ID DESC;
```


### GROUP BY/HAVING
> 프로그래머스 <노선별 평균 역 사이 거리 조회하기>
```SQL
SELECT ROUTE,  
CONCAT(ROUND(SUM(D_BETWEEN_DIST), 1),'km') AS TOTAL_DISTANCE, 
CONCAT(ROUND(AVG(D_BETWEEN_DIST), 2), 'km') AS AVERAGE_DISTANCE
FROM SUBWAY_DISTANCE
GROUP BY ROUTE
ORDER BY ROUND(SUM(D_BETWEEN_DIST), 1) DESC;
```

### 함수
> 문자형 함수

함수명|함수기능|기타
:---:|:---:|:---:
LOWER(대상) | 문자열을 소문자로 | 
UPPER(대상) | 문자열을 대문자로 | 
SUBSTR(대상, m, n) | 문자열 m위치에서 n개의 문자열 추출 | n 생략 시 끝까지 추출<br/> -m은 뒤에서부터 m위치에서 오른쪽으로
