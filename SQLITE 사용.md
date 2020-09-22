# SQLITE 사용

## 다운로드 및 등록

sqltie 홈페이지에서 파일 다운로드 받고, C 드라이브에 sqlite 폴더를 생성, 파일을 추가한다.

환경설정-사용자변수에서 path를 설정해준다.

> `C:\sqlite` 입력



bash 창을 열고

```bash
vi ~/.bashrc
```

입력 후 `i` 키를 눌러서 insert 설정

```sqlite
alias sqlite3="winpty sqlite3"
```

를 입력하면 bash창에서 `sqlite3`로 실행시킬 수 있다.

`esc`누르고

insert 위치에 `:wp` 입력해서 저장한다.



새로운 bash 창을 열고,

```bash
source ~/.bashrc
```

입력 한 후, 데이터 불러올 폴더로 들어가서 bash에 sqlite3 입력



`연습`

+++

## 데이터 불러오기

`.mode csv` : output mode csv로 변경

`.import hellodb.csv examples` : import 해오기



+++

### 조회한 데이터 정렬

`.headers on`

`.mode column`



+++

## Table 생성

```sqlite
CREATE TABLE classmates (
	id INTEGER PRIMARY KEY,
    name TEXT
);
```

> `;` : sqlite 에서 종료를 의미

`.tables`  : 만들어진 table 확인



ex) 다음과 같은 스키마를 가진 table을 만들어보자!

| column  | datatype |
| :-----: | :------: |
|  name   |   TEXT   |
|   age   |   INT    |
| address |   TEXT   |

```sqlite
sqlite> CREATE TABLE classmates (
   ...> name TEXT,
   ...> age INT,
   ...> address TEXT
   ...> );

```



### Table 생성 (NOT NULL 옵션 & id 직접 정의)

```sqlite
sqlite> CREATE TABLE classmates(
   ...> id INTEGER PRIMARY KEY,
   ...> name TEXT NOT NULL,
   ...> age INT NOT NULL,
   ...> address TEXT NOT NULL
   ...> );
```



### Table 생성 ( id 빼고 정의)

```sqlite
sqlite> CREATE TABLE classmates (
   ...> name TEXT NOT NULL,
   ...> age INT NOT NULL,
   ...> address TEXT NOT NULL
   ...> );
```



+++

## Table 및 Schema 조회

+ 테이블 목록 조회
  + `.tables`
+ 특정 테이블 스키마 조회
  + `.schema table(테이블 명)`



+++

## Table 삭제(DROP)

+ 특정 table 삭제
  + `DROP TABLE table;`



+++

## Data 추가(INSERT)

+ classmates 테이블에 이름이 홍길동이고 나이가 23인 데이터를 넣어보기!

```sqlite
sqlite> INSERT INTO classmates (name, age)
   ...> VALUES ('홍길동', 23);
```



+ classmates 테이블에 이름이 홍길동이고, 나이가 30이고 주소가 서울인 데이터를 넣어보기!

```sqlite
sqlite> INSERT INTO classmates(name, age, address)
   ...> VALUES ('홍길동', 30, '서울');

sqlite> SELECT * FROM classmates;
name  age  address
----  ---  -------
홍길동   23
홍길동   30   서울

```

혹은

```sqlite
sqlite> INSERT INTO classmates
   ...> VALUES ('홍길동', 30, '서울');
```



### Data 추가 (NOT NULL 설정 후 오류 확인)

```sqlite
sqlite> INSERT INTO classmates
   ...> VALUES ('홍길동', 23, '서울');
Error: table classmates has 4 columns but 3 values were supplied
```

> id 값을 입력하지 않았다. 하지만 id 값을 직접 입력하는 것은 곤란하다.
>
> 따라서 테이블 설정 시 id 설정을 하지 않는 것이 좋다.

+ id 직접 작성하지 않을 때

```sqlite
sqlite> INSERT INTO classmates (name, age, address)
   ...> VALUES ('홍길동', 23, '서울');

```



+ id 직접 작성 할 때

```sqlite
sqlite> INSERT INTO classmates VALUES (2, '홍길동', 30, '대전');

```



+++

## 데이터 조회(SELECT)

`SELECT * FROM examples` : examples 에서 가져오기

> examples : table 명

`SELECT rowid, name FROM tables` : 원하는 column만 가져오기

+ table에서 id, name column 값 하나만 가져오기

  + `SELECT rowid, name FROM classmates LIMIT 1;`

  + LIMIT 와 OFFSET 은 한 세트다.

    > offset : 앞의 <num> 만큼의 값을 제외하고 뒤에서부터 데이터를 가져온다.

  + `SELECT rowid, name FROM classmates LIMIT 1 OFFSET 2;`



+++

### WHERE 문



- 주소가 서울인 사람만 가져오기
  - ```sqlite
    SELECT rowid, name FROM classmates
    WHERE address='서울';
    ```

- age 중복 없이 가져오기

  - ```sqlite
    SELECT DISTINCT age FROM classmates;
    ```



users에서 age가 30 이상인 사람만 가져오기

```sqlite
SELECT * FROM users age >= 30;
```



users에서 age가 30 이상인 사람의 이름만 가져오기

> schema로 column 확인

```sqlite
SELECT first_name FROM users WHERE age >= 30;
```



### COUNT

> 레코드 총 개수

```sqlite
sqlite> SELECT COUNT(*) FROM users;
1000
```



### AVG() / SUM() / MIN() / MAX()

30살 이상인 사람들의 평균 나이는?

```sqlite
sqlite> SELECT AVG(age) FROM users WHERE age >= 30;
35.1763285024155

```



30살 이상인 사람들의 나이 중복 없이 출력

```sqlite
sqlite> SELECT DISTINCT(age) FROM users WHERE age >= 30;
40
36
37
30
33
32
35
34
39
38
31
```



users에서 계좌 잔액(balance)이 가장 높은 사람과 액수

```sqlite
sqlite> SELECT first_name, MAX(balance) FROM users;
"선영",990000
```



### LIKE (wild cards)

`WHERE column LIKE' ';`

|  %   |     `2%`     |               2로 시작하는 값                |
| :--: | :----------: | :------------------------------------------: |
|      |     `%2`     |                2로 끝나는 값                 |
|      |    `%2%`     |               2가 들어가는 값                |
|  _   |    `_2%`     | 아무값이나 들어가고 두번째가 2로 시작하는 값 |
|      |    `1___`    |           1로 시작하고 4자리인 값            |
|      | `2_%_%/2__%` |        2로 시작하고 적어도 3자리인 값        |



user에서 20대인 사람?

```sqlite
sqlite> SELECT * FROM users WHERE age LIKE '2_';
```



user에서 지역번호가 02인 사람

```sqlite
sqlite> SELECT * FROM users WHERE
   ...> phone LIKE '02-%';
```



users에서 이름이 '준'으로 끝나는 사람

```sqlite
sqlite> SELECT * FROM users WHERE
   ...> first_name LIKE '%준';
```



+++

## 정렬 (ORDER)

ASC : 오름차순 (default)

DESC : 내림차순



users 에서 나이 순으로 오름차순 정렬하여 상위 10개 뽑기

```sqlite
sqlite> SELECT * FROM users ORDER BY age ASC LIMIT 10;
```



users에서 나이순 , 성 순으로 오름차순 정렬하여 상위 10개 뽑기

```sqlite
sqlite> SELECT * FROM users ORDER BY age, last_name ASC LIMIT 10;
```



+++

### GROUP BY



users에서 각 성(last_name)씨가 몇 명씩 있는지 조회 하시오

```sqlite
sqlite> SELECT last_name, COUNT(*)
   ...> FROM users
   ...> GROUP BY last_name;
```



+++

### ALTER

> 테이블 명 변경



articles 테이블 생성 한 후 진행



테이블 명 변경

```sqlite
sqlite> ALTER TABLE articles RENAME TO news;
sqlite> .tables
classmates  examples    news        users
```



새로운 컬럼 추가

```sqlite
sqlite> ALTER TABLE news
   ...> ADD COLUMN created_at TEXT NOT NULL;
Error: Cannot add a NOT NULL column with default value NULL
```

> 기존 데이터에 NOT NULL 조건으로 인해 NULL 값으로 새로운 칼럼이 추가될 수 없으므로 에러가 발생한다.
>
> NOT NULL 조건을 빼고 컬럼을 추가하면 정상적으로 추가된다. 혹은 **디폴트 값을 넣어서  추가한다**

```sqlite
sqlite> ALTER TABLE news
   ...> ADD COLUMN subtitle TEXT NOT NULL DEFAULT 1;
sqlite> .schema news
CREATE TABLE IF NOT EXISTS "news" (
title TEXT NOT NULL,
content TEXT NOT NULL
, subtitle TEXT NOT NULL DEFAULT 1);

sqlite> SELECT * FROM news;
"1번 제목","1번 내용",1
```



+++

## Data 삭제(DELETE)

`DELETE FROM table WHERE rowid=?;`

- id 기준으로 삭제

  - ```sqlite
    DELETE FROM classmates WHERE rowid=4;
    ```



+++

## Data 수정(UPDATE)

`UPDATE table SET column=value WHERE condition;`

- 해당 row id 사람의 데이터 수정

```sqlite
sqlite> UPDATE classmates SET name='홍길동', address='제주도'
   ...> WHERE rowid=4;
sqlite> SELECT rowid, *FROM classmates;
rowid  name  age  address
-----  ----  ---  -------
1      홍길동   30   서울
2      김철수   23   대전
3      박나래   23   광주
4      홍길동   45   제주도

```

+++



## 참고

SQLite는 따로 PRIMARY KEY 속성의 컬럼을 작성하지 않으면, 값이 자동으로 증가하는 PK 옵션을 가진 `rowid` 컬럼을 정의한다.

> rowid  : 64bit 정수 타입의 유일한 식별 값
>
> INTEGER PRIMARY KEY 타입으로 컬럼을 만들면 이는 rowid를 대체한다.

+ rowid 확인

```sqlite
sqlite> SELECT rowid, * FROM classmates;
rowid  name  age  address
-----  ----  ---  -------
1      홍길동   23
2      홍길동   30   서울
3      홍길동   30   서울
```



주소가 꼭 필요한 정보라면 공백으로 비워두면 안된다.(NOT NULL)

> 빈 문자열 `' '` 은 가능하다.



특정한 요구사항 (사용 되지 않은 값이나 이전에 삭제 된 행의 값을 재사용하지 못하게 하는)이 없다면

`AUTOINCREMENT` 속성을 사용하지 않아야 한다고 한다.



+ 내부적으로 CPU, 메모리, 디스크 공간을 추가로 불필요하게 사용하기 때문이다.
+ django는 사용?
  + 데이터베이스에서 삭제가 된 데이터에 대해 더 이상 불필요한 데이터라고 처리하는 것을 중요하게 생각하기 때문이다
    + 프레임워크 관점의 차이!!