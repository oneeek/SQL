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
* ALL:중복 허용 / DISTINCT:중복 허용 X
* ASC:오름차순(기본) / DESC:내림차순
