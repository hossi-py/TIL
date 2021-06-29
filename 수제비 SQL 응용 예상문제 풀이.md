1. 트랜잭션에 대해 서술하시오

- 데이터베이스 시스템에서 하나의 논리적 기능이 정상적으로 수행하기 위한 작업의 기본 단위



2.

- 외부
- 개념
- 내부



3. 데이터의 검색을 빠르게 하기 위한 구조



4.

```sql
CREATE INDEX 사번인덱스 ON 사원(사번);
```



5.

```sql
CREATE TABLE 사람
(
	이름 VARCHAR(10), 
    성별 CHAR(1) CHECK(성별 = 'M' or 성별 = 'F')
);
```



6.

```sql
ALTER TABLE 사원 ADD 전화번호 VARCHAR(11);
```



7.

```sql
CREATE VIEW 사원뷰 AS SELECT 사번, 이름 FROM 사원 WHERE 성별 = 'M';
```



8.

```sql
SELECT DISTINCT 전공 FROM 학생;
```



9.

```sql
SELECT 학번 FROM 학생 WHERE 이름 = '이%';
```



10.

```sql
SELECT 주소 FROM 학생 WHERE 주소 IS NOT NULL;
```



11.

```sql
SELECT * FROM 교수 WHERE 전공 IN ('컴퓨터공학', '전자공학');
```



12.

```sql
SELECT 이름 FROM 고객 WHERE 나이 BETWEEN 50 AND 59 AND 성별 = '남자';
```



13.

```sql
SELECT * FROM 성적 ORDER BY 성적 DESC;
```



14.

???



15.

3



16.

```sql
INSERT INTO EMPLOYEE(NAME, AGE, SALARY) VALUES('홍길동', 24, 300);
```



17.

```sql
DELETE FROM EMPLOYEE WHERE SALARY <= 300;
```



18.

```sql
GRANT UPDATE ON 학생 TO 장길산;
```

