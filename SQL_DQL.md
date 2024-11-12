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
FROM CUSTOMER
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
:---|:---|:---
LOWER(대상) | 문자열을 소문자로 | 
UPPER(대상) | 문자열을 대문자로 | 
SUBSTR(대상, m, n) | 문자열 m위치에서 n개의 문자열 추출 | n 생략 : 끝까지 추출<br/> -m : 뒤에서부터 m위치에서 오른쪽으로
INSTR(대상, 찾을 문자열, m, n) | 대상에서 찾을 문자열 위치 반환 <br/> m위치에서 시작, n번째 발견된 문자열 위치 | m, n 생략 : 1로 해석 <br/> -m : 뒤에서부터 m위치에서 왼쪽으로
LTRIM(대상, 삭제 문자열) | 문자열 중 특정 문자열을 왼쪽에서 삭제 | 삭제 문자열 생략 : 공백 삭제
RTRIM(대상, 삭제 문자열) | 문자열 중 특정 문자열을 오른쪽에서 삭제 | 삭제 문자열 생략 : 공백 삭제
TRIM(대상) | 문자열 중 특정 문자열을 쪽에서 삭제 | ORACLE : 공백만 삭제 가능
LPAD(대상, n, 문자열) | 대상 왼쪽에 문자열을 추가하여 총 n의 길이로 | 
RPAD(대상, n, 문자열) | 대상 오른쪽에 문자열을 추가하여 총 n의 길이로 |
CONCAT(대상1, 대상2) | 대상 문자열 결합 | 두 개의 인수만 전달 가능
LENGTH(대상) | 대상 문자열 길이 | 
REPLACE(대상, 찾을 문자열, 바꿀 문자열) | 일치하는 문자열 치환 및 삭제 | 바꿀 문자열 생략, 빈 문자열 전달 : 찾을 문자열 제거
TRANSLATE(대상, 찾을 문자열, 바꿀 문자열) | 문자열 1:1 치환 | 바꿀 문자열 생략 불가 <br/> 빈 문자열 전달 : 전체 NULL

- SQL Server <br/>
SUBSTR > SUBSTRING <br/>
LENGTH > LEN <br/>
INSTR > CHARINDEX <br/>


> 숫자형 함수

함수명|함수기능|기타
:---|:---|:---
ABS(숫자) | 절대값 | 
ROUND(숫자, 자리수) | 반올림 | 자리수로 반올림 <br/> 자리수 -2 : 정수 십의 자리에서 반올림
TRUNC(숫자, 자리수) | 버림 | 자리수로 버림
SIGN(숫자) | 양수면1, 음수면-1, 0이면0 | 
FLOOR(숫자) | 작거나 같은 최대 정수(버림) | 
CEIL(숫자) | 크거나 같은 최소 정수(올림) | 
MOD(숫자1, 숫자2) | 숫자1을 숫자2로 나눈 나머지 | 
POWER(m, n) | m의 n 거듭제곱 | 
SQRT(숫자) | 루트값 | 


> 날짜형 함수

함수명|함수기능|기타
:---|:---|:---
SYSDATE | 현재 날짜와 시간 | 
CURRENT_DATE | 현재 날짜 | 
CURRENT_TIMESTAMP | 현재 타임스탬프 | 
ADD_MONTHS(날짜, n) | 날짜에서 n개월 후 날짜 | -n : n개월 이전 날짜
MONTHS_BETWEEN(날짜1, 날짜2) | 날짜1과 날짜2의 개월 수 차이 | 날짜1<날짜2 : 음수
LAST_DAY(날짜) | 주어진 월의 마지막 날짜 | 
NEXT_DAY(날짜, n) | 주어진 날짜 이후 지정된 요일의 첫 날짜 | 1: 일요일 ~ 7: 토요일
ROUND(날짜, 자리수) | 날짜 반올림 | 자리수 'MONTH' 입력: 월 이전자리에서 반올림 (16일부터 올림) 
TRUNC(날짜, 자리수) | 날짜 버림 | 자리수 'MONTH' 입력: 월 이전자리에서 버림

- SQL Server <br/>
SYSDATE > GETDATE <br/>
ADD_MONTHS > DATEADD(모든 단위 날짜 연산 가능) <br/>
MONTHS_BETWEEN > DATEDIFF(두 날짜 사이의 년, 월, 일) <br/>


> 변환함수

함수명|함수기능|기타
:---|:---|:---
TO_NUMBER(문자) | 숫자 타입으로 변경 | 
TO_CHAR(대상, 포맷) | 대상을 포맷 형식으로 변경 | 포맷 'MM/DD-YYYY' 입력 : 날짜 형식, 문자 타입 <br/> 포맷 '9,999' 입력 : 천단위 구분기호, 문자 타입 <br/> 포맷 '09999' 입력 : 총 5자리로, 앞 자리수 0
TO_DATE(문자, 포맷) | 문자를 포맷 형식에 맞게 읽어 날짜 데이터로 변경 | 
FORMAT(날짜, 포맷) | 날짜의 포맷 형식 변경 | 포맷 'YYYY' 입력 : 문자 타입 '2024' 반환
CAST(대상 AS 데이터 타입) | 대상을 주어진 데이터 타입으로 변환 | 

- SQL Server <br/>
TO_NUMBER, TO_DATE, TO_CHAR > CONVERT(포맷 전달) <br/>
단순 변환은 주로 CAST 사용 <br/>


> 그룹함수

함수명|함수기능|기타
:---|:---|:---
COUNT(대상) | 행의 수 | NULL 무시 연산 <br/> 전체 NULL : 0 반환
SUM(대상) | 총 합 | NULL 무시 연산 <br/> 전체 NULL : 공집합 반환
AVG(대상) | 평균 | NULL 무시 연산 <br/> 전체 NULL : 공집합 반환
MIN(대상) | 최솟값 | NULL 무시 연산 <br/> 전체 NULL : 공집합 반환
MAX(대상) | 최댓값 | NULL 무시 연산 <br/> 전체 NULL : 공집합 반환
VARIANCE(대상) | 분산 | NULL 무시 연산 <br/> 전체 NULL : 공집합 반환
STDDEV(대상) | 표준편차 | NULL 무시 연산 <br/> 전체 NULL : 공집합 반환

- SQL Server <br/>
VARIANCE > VAR <br/>
STDDEV > STDEV <br/>


> 일반함수

함수명|함수기능|기타
:---|:---|:---
DECODE(대상, 값1, 리턴1, 값2, 리턴2, ~, 그외리턴) | 대상이 값1이면 리턴1, 값2이면 리턴2, ~, 그외에는 그외리턴값 | 그외리턴 생략 : NULL 반환
NVL(대상, 치환값) | 대상이 NULL이면 치환값 반환R > SUBSTRING <br/>
LENGTH > LEN <br/>
INSTR > CHARINDEX <br/>


> 숫자형 함수

함수명|함수기능|기타
:---|:---|:---
ABS(숫자) | 절대값 | 
ROUND(숫자, 자리수) | 반올림 | 자리수로 반올림 <br/> 자리수 -2 : 정수 십의 자리에서 반올림
TRUNC(숫자, 자리수) | 버림 | 자리수로 버림
SIGN(숫자) | 양수면1, 음수면-1, 0이면0 | 
FLOOR(숫자) | 작거나 같은 최대 정수(버림) | 
CEIL(숫자) | 크거나 같은 최소 정수(올림) | 
MOD(숫자1, 숫자2) | 숫자1을 숫자2로 나눈 나머지 | 
POWER(m, n) | m의 n 거듭제곱 | 
SQRT(숫자) | 루트값 | 


> 날짜형 함수

함수명|함수기능|기타
:---|:---|:---
SYSDATE | 현재 날짜와 시간 | 
CURRENT_DATE | 현재 날짜 | 
CURRENT_TIMESTAMP | 현재 타임스탬프 | 
ADD_MONTHS(날짜, n) | 날짜에서 n개월 후 날짜 | -n : n개월 이전 날짜
MONTHS_BETWEEN(날짜1, 날짜2) | 날짜1과 날짜2의 개월 수 차이 | 날짜1<날짜2 : 음수
LAST_DAY(날짜) | 주어진 월의 마지막 날짜 | 
NEXT_DAY(날짜, n) | 주어진 날짜 이후 지정된 요일의 첫 날짜 | 1: 일요일 ~ 7: 토요일
ROUND(날짜, 자리수) | 날짜 반올림 | 자리수 'MONTH' 입력: 월 이전자리에서 반올림 (16일부터 올림) 
TRUNC(날짜, 자리수) | 날짜 버림 | 자리수 'MONTH' 입력: 월 이전자리에서 버림

- SQL Server <br/>
SYSDATE > GETDATE <br/>
ADD_MONTHS > DATEADD(모든 단위 날짜 연산 가능) <br/>
MONTHS_BETWEEN > DATEDIFF(두 날짜 사이의 년, 월, 일) <br/>


> 변환함수

함수명|함수기능|기타
:---|:---|:---
TO_NUMBER(문자) | 숫자 타입으로 변경 | 
TO_CHAR(대상, 포맷) | 대상을 포맷 형식으로 변경 | 포맷 'MM/DD-YYYY' 입력 : 날짜 형식, 문자 타입 <br/> 포맷 '9,999' 입력 : 천단위 구분기호, 문자 타입 <br/> 포맷 '09999' 입력 : 총 5자리로, 앞 자리수 0
TO_DATE(문자, 포맷) | 문자를 포맷 형식에 맞게 읽어 날짜 데이터로 변경 | 
FORMAT(날짜, 포맷) | 날짜의 포맷 형식 변경 | 포맷 'YYYY' 입력 : 문자 타입 '2024' 반환
CAST(대상 AS 데이터 타입) | 대상을 주어진 데이터 타입으로 변환 | 

- SQL Server <br/>
TO_NUMBER, TO_DATE, TO_CHAR > CONVERT(포맷 전달) <br/>
단순 변환은 주로 CAST 사용 <br/>


> 그룹함수

함수명|함수기능|기타
:---|:---|:---
COUNT(대상) | 행의 수 | NULL 무시 연산 <br/> 전체 NULL : 0 반환
SUM(대상) | 총 합 | NULL 무시 연산 <br/> 전체 NULL : 공집합 반환
AVG(대상) | 평균 | NULL 무시 연산 <br/> 전체 NULL : 공집합 반환
MIN(대상) | 최솟값 | NULL 무시 연산 <br/> 전체 NULL : 공집합 반환
MAX(대상) | 최댓값 | NULL 무시 연산 <br/> 전체 NULL : 공집합 반환
VARIANCE(대상) | 분산 | NULL 무시 연산 <br/> 전체 NULL : 공집합 반환
STDDEV(대상) | 표준편차 | NULL 무시 연산 <br/> 전체 NULL : 공집합 반환

- SQL Server <br/>
VARIANCE > VAR <br/>
STDDEV > STDEV <br/>


> 일반함수

함수명|함수기능|기타
:---|:---|:---
DECODE(대상, 값1, 리턴1, 값2, 리턴2, ~, 그외리턴) | 대상이 값1이면 리턴1, 값2이면 리턴2, ~, 그외에는 그외리턴값 | 그외리턴값 생략 : NULL 반환 <br/> 대소비교 불가
NVL(대상, 치환값) | 대상이 NULL이면 치환값 반환 | 
NVL2(대상, 치환값1, 치환값2) | 대상이 NULL이면 치환값2 반환, NULL아니면 치환값1 반환 | 
COALESCE(대상1, 대상2, ~, 그외리턴) | 대상 중 첫번째부터 NULL이 아닌값 반환, 모두가 NULL이면 그외리턴값 반환 | 그외리턴값 생략 : NULL 반환 
ISNULL(대상, 치환값) | 대상이 NULL이면 치환값 반환 | SQL SERVER 함수 
NULLIF(대상1, 대상2) | 대상이 같으면 NULL 반환, 다르면 대상1 반환 | 
CASE문 | 조건별 치환 및 연산 수행 | 


>CASE문 예제
```SQL
SELECT SALE,
       CASE WHEN SALE = 200 THEN 'A'
            WHEN SALE = 300 THEN 'B'
                            ELSE 'C'
       END AS GRADE
FROM TRANSACTION;
```

*같은 대상에 대해 일치하는 조건일 때
```SQL
SELECT SALE,
       CASE SALE WHEN 200 THEN 'A'
                 WHEN 300 THEN 'B'
                          ELSE 'C'
       END AS GRADE
FROM TRANSACTION;
```

























