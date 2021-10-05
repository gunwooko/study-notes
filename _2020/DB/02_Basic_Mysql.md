# SQL (Structured Query Language)

SQL은 구조화된 Query 언어이다. 데이터베이스용 프로그래밍 언어로, 데이터베이스에 query를 보내 원하는 데이터만을 뽑아올 수 있다.

## Query란?

- 직역하면 "질의문"
- 예시로는 검색창에 적는 검색어도 Query의 일종
- 저장된 정보를 필터하기 위한 질문

## 데이터베이스는 왜 필요한가?

- **In-memory**: 서버 혹은 클라이언트에서 저장이 가능하고, 보통은 클라이언트에서 저장한다. 우선 끄면 데이터가 사라진다. (in-memory상이라는 의미는 보통, 서버가 켜있을 동안만 변수에 할당된 값을 통해 저장하는 것을 의미한다)
- **File I/O**: node.js 의 fs 모듈, 그중에서도 readFile이나 writeFile method 등을 이용해 자료를 파일로 저장하기도 할 수도 있다. 저장은 할 수 있지만, 원하는 데이터만 가져올 수 없고 항상 모든 데이터를 가져온 뒤 서버에서 필터링이 필요하다. (ex) for문, filter) 그래서 서버에 부화가 많이 걸리다.

위의 모든 문제점을 해결하는 것이 **데이터베이스**이다. 필터링 외에도 File I/O고 구현이 힘든 관리를 위한 여러 기능을 가지고 있는 데이터에 특화된 서버라고 볼 수 있다.

### Persistance (영속성)

데이터를 생성한 프로그램이 종료되더라도 사라지지 않는 데이터의 특성을 말한다. 영속성을 갖지 않는 데이터는 단지 메모리에서만 존재하기에 프로그램을 종료하면 데이터는 삭제된다. (In-memory 형식)
또 다르게 표현하면, 서버가 재시작해도 저장된 데이터가 지워지지 않는 것을 의미하며, 대부분의 어플리케이션에서 요구되는 기능이다.

## 데이터베이스란?

데이터베이스와 엑셀(스프레드시트)과 많이 닮았다. 여러 부분이 비슷하다고 말할 수 있는데 (테이블-시트 / column(열)-row(행: 각 데이터) / 필터 기능), 다른 점은 스프레드시트는 인터페이스를 통해 필터링 된 정보를 볼 수 있지만, 데이터베이스는 서버와 교류하기 때문에 그 형태가 쿼리(Query)이다.

```
// Query 문 예제)
SELECT*
FROM student
WHERE gender='M';

// 위 Query 문 해석
*(모든 열을) 선택해라
student에서
gender = 'M'인 데이터들을
```

예를 들어 클라이언트에서 "남자 학생들 목록을 보여줘"라고 한다면, 서버에서는 이 요청을 처리하기 위해서 데이터베이스에 위의 쿼리문을 보내고, 데이터베이스는 이 쿼리문을 가지고서 필터링을 하고서 결과값을 서버에 전달해 준다. (다양한 방법이 있다: JSON, XML, etc) 결과값을 전달받은 서버는 따로 가동할 필요 없이 이것을 가지고 클라이언트에 전해줄 수 있다.

## SQL Tutorial

> [w3s를 참고했다](https://www.w3schools.com/sql/default.asp)

### Select

데이터베이스로부터 데이터를 선택하기 위해 사용한다. 반환된 데이터는 result-set(결과 집합)이라는 result table에 저장된다.

```
SELECT column1, column2, ...
FROM table_name
```

`SELECT *`은 모든 열을 선택한다.
`FROM`은 데이터가 저장되어있는 데이블과 같다.

### Where

Records를 필터링하는 데 사용된다. Where 절은 지정된 조건을 충족하는 records만 추출하는 데 사용된다.

```
SELECT column1, column2, ...  //또한 UPDATE, DELETE 문에서도 사용된다.
FROM table_name
WHERE condition;
```

```
// 예제
SELECT * FROM Customers
WHERE Country='Mexico'; // 텍스트값에는 따옴표가 필요하다.

SELECT * FROM Customers
WHERE CustomerID=1; // 숫자는 따옴표로 묶지 않는다.
```

### And, Or, Not

Where 절은 AND, OR, NOT 연산자와 결합할 수 있다.

```
// 예제
SELECT * FROM Customers
WHERE Country='Germany' AND City='Berlin';

SELECT * FROM Customers
WHERE Country='Germany' OR Country='Spain';

SELECT * FROM Customers
WHERE NOT Country='Germany' AND NOT Country='USA';
```

### Order By

Order By 키워드는 result-set을 오름차순 또는 내림차순으로 정렬하는데 사용된다.
기본적으로 records를 오름차순으로 정렬한다. 만일 내림차순으로 정렬하고 싶으면, `DESC` 키워드를 사용하면 된다.

```
// 고객 테이블에서 국가 열을 기준으로 정렬하여 모든 고객을 선택
SELECT * FROM Customers
ORDER BY Country;

// descending으로 정렬
SELECT * FROM Customers
ORDER BY Country DESC;

// 국가별로 정렬하지만, 동일한 국가가 있으면 성함으로 정렬한다.
SELECT * FROM Customers
ORDER BY Country, CustomerName;

SELECT * FROM Customers
ORDER BY Country ASC, CustomerName DESC;
```

### Insert Into

테이블에 새 레코드를 삽입하는 데 사용된다. INSERT INTO 문을 두 가지 방법으로 작성할 수 있다.

1. 열 이름과 삽입할 값을 모두 지정하기

```
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);

// 만일 테이블의 모든 열에 값을 추가하는 경우, 열 이름을 지정할 필요가 없다.
// 그러나 값의 순서가 테이블의 열과 동일한 순서인지 확인해야 한다.
INSERT INTO table_name
VALUES (value1, value2, value3, ...);

// 예시
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway');

// CustomerID 열은 자동 증분 필드이며, 새 레코드가 테이블에 삽입될 때 자동 생성된다.
```

- [SQL 자동 증분 필드이란](https://www.w3schools.com/sql/sql_autoincrement.asp)

2. 특정 열에만 데이터를 삽입하기

```
// 새 레코드를 삽입하지만 "CustomerName", "City"및 "Country"열에 만 데이터를 삽입한다. (CustomerID는 자동으로 업데이트됨).

INSERT INTO Customers (CustomerName, City, Country)
VALUES ('Cardinal', 'Stavanger', 'Norway');
```

이후 Customers 테이블에서 선택한 내용을 확인해 보면, Cardinal이란 이름의 정보에서 삽입하지 않은 값은 `null`로 표시됨을 볼 수 있다.

### Null Values

값이 없는 필드를 가리킨다. `NULL` 값은 0 값 또는 공백이 포함된 필드와 다르다. `NULL` 값을 가진 필드는 레코드 작성 중에 비워진 필드이다.

#### Null 값을 테스트하는 방법

- `IS NULL` 구문

```
// 다음은 주소 필드에 NULL 값을 가진 모든 고객을 나열한다.
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NULL;
```

항상 `IS NULL`을 사용해서 `null`값을 찾자.

- `IS NOT NULL` 구문

```
// 다음은 주소 필드에 값이 있는 모든 고객을 나열한다.
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NOT NULL;
```

### Update

테이블의 기존 레코드를 수정하는 데 사용된다.
**한 가지 주의할 점은**, 항상 업데이트 문을 사용할 때 where 절을 확인해야 한다. where 절에서 업데이트할 레코드를 지정하기에, where 절을 생략하게 되면 테이블의 모든 레코드가 업데이트된다.

```
// 구문
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;

// 예시: 첫 번째 고객(CustomerID = 1)을 새로운 담당자 및 새로운 도시로 업데이트한다.
UPDATE Customers
SET ContactName = 'Alfred Schmidt', City= 'Frankfurt'
WHERE CustomerID = 1;

// 예시2: 국가가 멕시코인 모든 레코드의 연락처 이름을 Juan으로 업데이트 한다.
UPDATE Customers
SET ContactName='Juan'
WHERE Country='Mexico';
```

### Delete

테이블에서 기존 레코드를 삭제하는데 사용된다.
**한 가지 주의할 점은**, where 절을 반드시 확인해야한다. where절은 삭제할 레코드를 지정하기 때문이다. where 절을 생략하면 테이블의 모든 레코드가 삭제된다.

```
// 삭제 구문
DELETE FROM table_name WHERE condition;

// 예시: 고객 테이블에서 고객 Alfreds Futterkiste를 삭제한다.
DELETE FROM Customers WHERE CustomerName='Alfreds Futterkiste';
```

#### 모든 레코드 삭제

```
// 구문: 테이블을 삭제하지 않고 테이블의 모든 행을 삭제하고 싶을 때
// 이는 테이블 구조, 속성 및 인덱스가 그래도 유지됨을 의미한다.
DELETE FROM table_name;

// 예시: 테이블을 삭제하지 않고, 고객 테이블의 모든 행을 삭제할 때
DELETE FROM Customers;
```

### Count

`COUNT()` 함수는 지정된 기준과 일치하는 행 수를 반환한다. 참고로 `null`값은 계산되지 않는다.

```
// 구문
SELECT COUNT(column_name)
FROM table_name
WHERE condition;
```

### Like

LIKE 연산자는 where절에서 열에서 지정된 패턴을 검색하는데 사용된다.
LIKE 연산자와 함께 자주 사용되는 두 가지 와일드카드가 있다.

- `%` 백분율 기호는 0, 1 또는 여러 문자를 나타낸다.
- `_` 밑줄은 단일 문자를 나타낸다.
  AND, OR, NOT 연산자를 사용하여 여러 조건을 결합 할 수도 있다.

```
// 예제
SELECT * FROM Customers
WHERE CustomerName LIKE 'a%'; // a로 시작하는 CustomerName

WHERE CustomerName LIKE '%a'; // a로 끝나는 ...

WHERE ContactName LIKE 'a%o'; // a로 시작, 0로 끝나는 ...

WHERE CustomerName LIKE '%or%'; // 임의의 위치에 or 이 있는 ...

WHERE CustomerName LIKE '_r%'; // 두 번째 위치에 r이 있는 ...

WHERE CustomerName LIKE 'a__%'; // a로 시작하고 길이가 3자 이상인 ...

WHERE CustomerName NOT LIKE 'a%'; // a로 시작하지 않는 ...
```

### Wildcards

와일드카드 문자는 문자열에서 하나 이상의 문자를 대체하는데 사용된다. 그리고 LIKE 연산자와 함께 사용된다.

- `%` 와일드 카드
- `_` 와일드 카드
- `[charlist]` 와일드 카드

```
// 예제
SELECT * FROM Customers
WHERE City LIKE '[bsp]%'; // 도시가 b, s 또는 p로 시작하는 모든 고객을 선택

WHERE City LIKE '[a-c]%'; // 도시가 a,b 또는 c로 시작하는 ...
```

- `[!charlist]` 와일드 카드

```
// 예제
SELECT * FROM Customers
WHERE City LIKE '[!bsp]%'; // b, s, 또는 p로 시작하지 않는 도시의 ...

WHERE City NOT LIKE '[bsp]%'; // 이렇게도 사용할 수 있다.
```

### Aliases

테이블 또는 테이블의 열에 임시 이름을 제공하는 데 사용된다. Aliases는 종종 열 이름을 더 읽기 쉽게 만드는 데 사용되는데, 쿼리하는 동안만 존재한다.

```
// Aliases 열 구문
SELECT column_name AS alias_name
FROM table_name;

// 예제: CustomerID는 ID로 CustomerName은 Customer이란 별칭을 만든다.
// 참고로 Aliases에 공백이 있으면 큰 따옴표 또는 대괄호로 묶어서 사용한다.
SELECT CustomerID AS ID, CustomerName AS Customer
FROM Customers;

// 예제2 "Address" that combine four columns (Address, PostalCode, City and Country):
SELECT CustomerName, Address + ', ' + PostalCode + ' ' + City + ', ' + Country AS Address
FROM Customers;

// Aliases 테이블 구문
SELECT column_name(s)
FROM table_name AS alias_name;
```

쿼리에 관련된 테이블이 두 개 이상있다거나, 쿼리에 함수가 사용된다거나, 열 이름이 크거나 읽을 수 없는 경우, 둘 이상의 열이 결합된 경우 Aliases를 사용하는 것이 유용할 수 있다.

### Joins

둘 사이의 관련 열을 기반으로 둘 이상의 테이블의 행을 결합하는데 사용된다.

- [Understanding 21 SQL Joins](https://blazarblogs.wordpress.com/2019/08/27/understanding-21-sql-joins/)
- [MySQL JOIN Types Poster](http://stevestedman.com/2015/03/mysql-join-types-poster/?cli_action=1595552580.258)

### Inner Join

두 테이블에서 일치하는 값을 가진 레코드를 반환한다.

```
// 두 테이블 모두에서 값이 일치하는 레코드를 선택한다
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;
```

### Left Join (Outer Join)

왼쪽 테이블의 모든 레코드와 오른쪽 테이블의 일치하는 레코드를 반환한다. 일치하는 것이 없으면 결과는 오른쪽에서 `NULL`이다. 그리고 오른쪽 테이블에 일치하는 항목이 없더라도 왼쪽 테이블의 모든 레코드를 반환한다.

```
SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name = table2.column_name;
```

- [생활코딩 - SQL JOIN - 4. LEFT JOIN ](https://www.youtube.com/watch?v=pJqBR2TNe24)

### Right Join (Outer Join)

오른쪽 테이블의 모든 레코드와 왼쪽 테이블의 일치하는 레코드를 반환한다. 일치하는 것이 없으면 결과는 왼쪽에서 `NULL`이다. 그리고 왼쪽 테이블에 일치하는 항목이 없더라도 오른쪽 테이블의 모든 레코드를 반환한다.

```
SELECT column_name(s)
FROM table1
RIGHT JOIN table2
ON table1.column_name = table2.column_name;
```

### Group By

같은 값을 가진 행을 요약 행으로 그룹화한다.
GROUP BY 문은 종종 집계 함수 (COUNT, MAX, MIN, SUM, AVG)와 함께 사용되어 result-set(결과 집합)을 하나 이상의 열로 그룹화한다.

```
// 구문
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
ORDER BY column_name(s);

// 예시1: 각 국가의 고객 수를 나타낸다
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country;

// 예시2: 각 국가의 고객 수를 높은 순서에서 낮은 수서로 나열한다
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
ORDER BY COUNT(CustomerID) DESC;
```

[[SQL 10] 그룹 함수, GROUP BY 절, HAVING 절](https://keep-cool.tistory.com/37)
[GROUP BY절](http://www.gurubee.net/lecture/1032)

## SQL Database

### SQL Create DB

새 SQL 데이터베이스를 작성하는데 사용된다.

```
CREATE DATABASE databasename;
```

데이터베이스를 작성하기 전에 관리자 권한이 있는지 확인해야한다. 데이터베이스가 작성되면 다음 SQL 명령을 사용하여 데이터베이스 목록에서 데이터베이스를 확인할 수 있다. `SHOW DATABASES;`

### SQL Drop DB

기존 SQL 데이터베이스를 삭제하는데 사용된다.

```
DROP DATABASE databasename;
```

데이터베이스를 삭제하면 데이터베이스에 저장된 정보가 손실된다.
데이터베이스를 삭제하기 전에 관리자 권한이 있는지 확인해야한다. 데이터베이스가 삭제되면 다음 SQL 명령을 사용하여 데이터베이스 목록에서 데이터베이스를 확인할 수 있다. `SHOW DATABASES;`

### SQL Create Table

데이터베이스에서 새 테이블을 작성하는 데 사용된다.

```
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
   ....
);
```

[w3s - SQL Create Table](https://www.w3schools.com/sql/sql_create_table.asp)

### SQL Drop Table

데이터베이스에서 기존 테이블을 삭제하는 데 사용된다.

```
DROP TABLE table_name;
```

### SQL TRUNCATE Table

테이블 자체가 아닌 테이블 내부의 데이터를 삭제하는 데 사용된다.

```
TRUNCATE TABLE table_name;
```

### SQL Alter Table

기존 테이블의 열을 추가, 삭제 또는 수정하는 데 사용된다. 또한 기존 테이블에서 다양한 제한 조건을 추가 및 삭제하는 데 사용된다.

- 테이블에 열을 추가하고 싶을 때
- 테이블에서 열을 삭제하고 싶을 때
- 테이블에서 열의 데이터 유형을 변경하고 싶을 때
  [w3s - SQL Alter Table](https://www.w3schools.com/sql/sql_alter.asp)

### SQL Not Null

기본적으로 열은 `NULL`값을 보유할 수 있다. NOT NULL 제약조건(constraint)은 열이 NOT NULL 값을 수락하도록 한다. 이렇게하면 필드에 항상 값이 포함되므로 이 필드에 값을 추가하지 않고 새 레코드를 삽입하거나 레코드를 업데이트 할 수 없다.

- CREATE TABLE에서 SQL NOT NULL
- ALTER TABLE의 SQL NOT NULL
  [w3s - SQL Not Null](https://www.w3schools.com/sql/sql_notnull.asp)

### SQL Unique

열의 모든 값이 다른지 확인한다.
[w3s - SQL Unique](https://www.w3schools.com/sql/sql_unique.asp)

### SQL Primary Key

테이블의 각 레코드를 고유하게 식별한다.
[w3s - SQL Primary Key](https://www.w3schools.com/sql/sql_primarykey.asp)

### SQL Foreign Key

두 테이블을 서로 연결하는 데 사용되는 키이다. FOREIGN KEY는 한 테이블에서 다른 테이블의 PRIMARY KEY를 참조하는 필드(또는 필드 모음)이다.
[w3s - SQL Foreign Key](https://www.w3schools.com/sql/sql_foreignkey.asp)

### SQL Default

열의 기본값을 제공하는 데 사용된다. 다른 값을 지정하지 않으면 기본값이 모든 새 레코드에 추가된다.
[w3s - SQL Default](https://www.w3schools.com/sql/sql_default.asp)

### SQL Auto Increment

새 레코드가 테이블에 삽입 될 때 고유 번호가 자동으로 생성되도록한다. 종종 새로운 레코드가 삽입 될 때마다 자동으로 생성되는 기본 키 필드이다.
[w3s - SQL Auto Increment](https://www.w3schools.com/sql/sql_autoincrement.asp)

### SQL Dates

날짜를 사용할 때 가장 어려운 부분은 삽입하려는 날짜 형식이 데이터베이스의 날짜 열 형식과 일치하는지 확인하는 것이다. 데이터에 날짜 부분 만 포함되어 있으면 쿼리가 예상대로 작동한다. 그러나 시간 부분이 관련되면 더 복잡해진다.
[w3s - SQL Dates](https://www.w3schools.com/sql/sql_dates.asp)

# SQL with MySQL

대표적인 관계형 데이터베이스(RDBMS)의 하나인 MySQL은 Schema를 설계하고 SQL을 사용하여 데이터를 영속성있게(persistently) 저장해준다.

## MySQL 설치 및 서비스 시작

Ubuntu Linux 사용자는 `apt-get` 패키지 매니저를 이용해서 mysql를 설치할 수 있다. 참고: [Ubuntu MySQL 설치](https://support.rackspace.com/how-to/install-mysql-server-on-the-ubuntu-operating-system/)

```
$ sudo apt-get update
$ sudo apt-get install mysql-server
```

MacOS 사용자는 [Homebrew](https://brew.sh/)라는 패키지 매니저를 이용해 설치할 수 있다. 참고: [macOS MySQL 설치](https://gist.github.com/nrollr/3f57fc15ded7dddddcc4e82fe137b58e)

```
$ brew install mysql
$ brew info mysql
```

설치 후에 MySQL 서비스를 실행해야 MySQL을 사용할 수 있다.(참고로 나는 Ubuntu를 사용한다.)

```
$ sudo systemctl start mysql
```

## MySQL 접속

다음 명령어로 MySQL에 접속할 수 있다. 오류가 발생하거나, 존재하지 않는 명령어라는 결과가 나온다면, 설치에 문제가 있거나, 혹은 MySQL이 실행되지 않은 상태이다.

```
// mysql -u(계정 접근) [계정명] -p(비밀번호 입력)

$ mysql -u root -p
```

MySQL에 접속한 이후에 데이터베이스를 생성하고, 테이블 생성 및 데이터 조회를 해볼 수 있겠다.

## MySQL 이슈

- [MySQL 비밀번호 변경 방법](https://inma.tistory.com/98)

## MySQL official Docs: 공식 지원하는 Syntax를 확인하기

- [MySQL CREATE TABLE reference docs](https://dev.mysql.com/doc/refman/8.0/en/create-table.html)
- [MySQL SELECT reference docs](https://dev.mysql.com/doc/refman/8.0/en/select.html)
- [MySQL INSERT reference docs](https://dev.mysql.com/doc/refman/8.0/en/insert.html)
- [Executing SQL statements from a file](https://dev.mysql.com/doc/refman/8.0/en/batch-mode.html)

## node.js에서의 mysql 모듈: README.md를 읽고, 사용법 알아보기

- [Node mysql module docs](https://github.com/mysqljs/mysql)

# SQL GUI Support Tool

데이터베이스에 접속하는 것을 터미널 환경(CLI)이 아닌 이를 보조해주는 툴(GUI)를 이용해서 데이터베이스에 접속할 수 있다.

- [MySQL Workbench](https://www.mysql.com/products/workbench/)
- Sequel Pro (OSX 전용)
- Table Plus
- DBeaver
- DataGrip

# Schema & Query Design

## Schema란?

스키마(schema)는 데이터베이스에서 데이터가 구성되는 방식과 서로 다른 엔티티 간의 관계에 대한 설명이다. 즉, 데이터베이스의 청사진과 같다. 데이터를 정의하는 방법, 데이터 간의 관계를 구성하는 방법을 하기 위해 필요한 것이 스키마이다.

- **엔티티**란 고유한 정보의 단위이다. 엔티티는 데이터베이스에서 테이블로 표시할 수 있다.
- 각 엔티티에는 해당 엔티티의 특성을 설명하는 **필드(Field)**가 있다. 행렬이라면(테이블로 표현하자면) 열(column)에 해당하겠다. 가장 상단에 헤더로 있는 줄이다.
- **레코드(record)**는 테이블에 저장된 항목이다. 행렬에서의 행(row)이라고 볼 수 있다.

## 1:N의 관계

상황: 보통 학교에서 각 선생님이 여려 가지의 수업을 진행할 수 있다. 이러한 형태의 관계를 1:N(one to many, 일대 다)라고 표현한다.
1대 다수의 관계를 표현하기에는 1의 ID를 N 테이블에 저장하는 것이다.

## N:N의 관계

상황: 각 수업은 여러 명의 학생으로 구성되어 있고, 각 학생 또한 여러 개의 수업을 듣고 있다. 이러한 형태의 관계를 N:N(many to many, 다대 다)이라고 표현할 수 있다.
하나의 열(column)에 여러 값을 저장할 수 없다는 것을 배웠다. 즉, 수업 테이블에 여러 개의 학생ID들을 저장할 수 없다. 그 이유는 수업당 최대 학생 수를 늘리면 문제가 발생하기 때문이다. 반대로도 해결되지 않는다.
그렇다면 두 엔티티의(수업과 학생) 관계를 어떻게 하면 정확히 보여줄 수 있을까?
다른 형태로 데이터를 표현해 볼 수 있다: 수업ID와 학생ID로 이루어진 좌표계 테이블과 같은 형태. 이런 테이블을 Foreign키로 이루어진 Join 테이블로 만들어서, 일대 다가 두 번 이루어지는 형태로 나눠서 만들 수 있다.

## Schema 설계하기

![](https://images.velog.io/images/gunwooko/post/c55fef09-b2dc-4ebc-85a6-3e06422dcc57/f0pf6_xNm-1594972163489.png)
(출처: 코드스테이츠)

#### user 테이블

| Field | Type         | Null | Key | Default | Extra          |
| ----- | ------------ | ---- | --- | ------- | -------------- |
| id    | int          | No   | PK  | null    | auto_increment |
| name  | varchar(255) | No   |     | null    |                |
| email | varchar(255) | No   |     | null    |                |

#### content 테이블

| Field      | Type         | Null | Key | Default           | Extra             |
| ---------- | ------------ | ---- | --- | ----------------- | ----------------- |
| id         | int          | No   | PK  | null              | auto_increment    |
| title      | varchar(255) | No   |     | null              |                   |
| body       | varchar(255) | No   |     | null              |                   |
| created_at | timestamp    | No   |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED |
| userId     | int          | Yes  | FK  | null              |                   |

```MySQL
CREATE TABLE user(
    id int NOT NULL AUTO_INCREMENT,
    name varchar(255) NOT NULL,
    email varchar(255) NOT NULL,
    PRIMARY KEY(id),
    );

CREATE TABLE content(
    id int NOT NULL AUTO_INCREMENT,
    title varchar(255) NOT NULL,
    body varchar(255) NOT NULL,
    created_at timestamp Default CURRENT_TIMESTAMP NOT NULL,
    userId int,
    PRIMARY KEY(id),
    FOREIGN KEY(userId) REFERENCES user(id)
    );
```

## Schema Visualizer

스키마를 디자인하기 위해 다양한 외부 도구를 사용할 수 있다.

- 연필과 펜을 이용한 A4용지 및 화이트 보드
- [DBdiagram](https://dbdiagram.io/d)
  [How dbdiagram.io makes your life better](https://hackernoon.com/dbdiagram-io-a-database-diagram-designer-built-for-developers-and-analysts-975f310d4f13)
- [WWW SQL Designer](https://ondras.zarovi.cz/sql/demo/?keyword=default)
- [MySQL Workbench](https://www.mysql.com/products/workbench/)

# Server with Database

## CRUD API

클라이언트의 http 요청에 따라 CRUD API를 구현할 수 있다. (CRUD: Create, Read, Update, Delete)

# 이슈

- [MySQL Import Database Schema](https://stackoverflow.com/questions/26015521/mysql-import-database-schema)
- [npm - dotenv](https://www.npmjs.com/package/dotenv)
- [Node.js 기반에서 환경변수 사용하기 블로그 1](https://velog.io/@public_danuel/process-env-on-node-js)
- 매개 변수화 된 쿼리
- 다중쿼리 처리 방법
  [[Node.js 8-2강] 다중쿼리 처리 방법, sql에 파라미터 매핑하는 다양한 방법](https://junspapa-itdev.tistory.com/10)
- ORM

# 참고

- [w3schools - sql](https://www.w3schools.com/sql/default.asp)
- [MySQL - GitHub](https://github.com/mysqljs/mysql)
- [w3schools - Node.js MySQL](https://www.w3schools.com/nodejs/nodejs_mysql.asp)
- [생활코딩 - 데이터베이스 MySQL](https://opentutorials.org/course/3161/19535)
- [What is Database? What is SQL?](https://www.guru99.com/introduction-to-database-sql.html)
