## SQLD
> - [x] 시험시간 : 90분
> 
> [1과목] **데이터 모델링의 이해** : 10문항 20점
> - 데이터 모델링의 이해
> - 데이터 모델과 SQL
>
> [2과목] **SQL 기본 및 활용** : 40문항 80점
> - SQL 기본
> - SQL 활용
> - 관리 구문


개정판 강의 : 
[홍쌤의 데이터랩](https://www.youtube.com/@hdatalab)


**`2024.11.06.`**
홍쌤의 데이터랩 [SQLD 1과목 완벽 정리] 수강완.

**`2024.11.11.`**
홍쌤의 데이터랩 [SQLD 2과목 PART1. SQL 기본] 수강완.

**`2024.11.13.`**
홍쌤의 데이터랩 [SQLD 2과목 PART2. SQL 활용] 수강완.

**`2024.11.14.`**
홍쌤의 데이터랩 [SQLD 2과목 PART3. 관리 구문] 수강완.

**`2024.11.15.`**
홍쌤의 데이터랩 [SQLD 기출문제 풀이 1회차] 수강완.





## 🤔

### SQL 명령어 종류

- **DDL** : CREATE, ALTER, DROP, TRUNCATE
- **DML** : INSERT, DELETE, UPDATE, MERGE
- **DCL** : GRANT, REVOKE
- **TCL** : COMMIT, ROLLBACK
- **DQL** : SELECT


### 정규화

- 제 1정규형 : **1NF** (First Normal Form) <br/>
테이블의 컬럼이 원자값(Atomic Value, 하나의 값)을 갖도록 테이블을 분해하는 것 <br/>


- 제 2정규형 : **2NF** (Second Normal Form) <br/>
제1 정규화를 진행한 테이블에 대해 완전 함수 종속을 만족하도록 테이블을 분해하는 것 <br/>
완전 함수 종속 = 기본 키의 부분집합이 결정자가 되어서는 안 됨 <br/>


- 제 3정규형 : **3NF** (Third Normal Form) <br/>
제2 정규화를 진행한 테이블에 대해 이행적 종속을 없애도록 테이블을 분해하는 것 <br/>
이행적 종속 = A→B, B→C가 성립할 때, A→C가 성립되는 것









