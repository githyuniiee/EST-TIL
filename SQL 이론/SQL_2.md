## DML

DML은 Data Manipulation Language의 약자로 데이터베이스에서 데이터를 조작하는데 사용

| SELECT | 데이터 조회에 사용 |
| --- | --- |
| INSERT | 데이터 삽입에 사용 |
| UPDATE | 데이터 수정에 사용 |
| DELETE | 데이터 삭제에 사용 |

## 조회

| SELECT | 조회할 열을 지정 |
| --- | --- |
| FROM | 조회할 테이블을 지정 |
| WHERE | 조회할 데이터를 필터링 |

```sql
//모든 열 조회
SELECT *
FROM students;

//별칭을 사용하여 열 이름 변경
SELECT name AS col1, age AS col2
FROM students;

//중복된 행 제거 
SELECT DISTINCT address
FROM students;
```

## 삽입

`INSERT INTO`

테이블에 새로운 행(row)을 삽입할 때 `INSERT INTO` 문을 사용

```sql
INSERT INTO students (name, age, address)
VALUES ('학생1', 20, '경기도'), ('학생2', 22, '경기도'), ('학생3', 23, '경기도');
```

## 수정

테이블에 새로운 행을 수정할 때 사용

| UPDATE | 수정할 테이블을 지정 |
| --- | --- |
| SET | 데이터 수정 |
| WHERE | 수정할 데이터를 필터링 |

```sql
UPDATE students
SET age = 10,
		address = '서울특별시'
WHERE name = '정약용';
```

## 삭제

테이블의 행을 삭제할 때 사용

| DELETE FROM | 삭제할 테이블을 지정 |
| --- | --- |
| WHERE | 삭제할 데이터를 필터링 |

```sql
//모든 행 삭제
DELETE
FROM students;

//특정 행 삭제
DELETE
FROM students
WHERE name = '이황'; 
```

## 내장 함수

함수 

- 입력 값을 받아 계산을 수행하고 결과를 반환하는 구조

내장 함수

- DBMS에서 기본적으로 제공하는 함수
- 내장함수는 DBMS마다 약간의 차이가 있을 수 있음

자주 사용하는 내장 함수들

`SUM, AVG, MIN, MAX, COUNT, CONCAT, LENGHT, REPLACE, NOW`

```sql
SELECT SUM(age) FROM students;

SELECT AVG(age) FROM students;

SELECT MAX(age) FROM students;

SELECT MIN(age) FROM students;

SELECT COUNT(DISTINCT address) FROM students; //address에서 중복을 제거한 값이 몇 개인지 구함

SELECT CONCAT(name, address) FROM students; //name, address 연결

SELECT address, LENGTH(address) FROM students; //주소가 몇 글자인지

SELECT REPLACE(address, '도', '레') FROM students; //address column의 도 -> 레 로 변경
```

## 그룹화

그룹화 : 같은 값을 가진 행끼리 하나의 그룹으로 뭉치는 기능

`GROUP BY` 구문을 사용하여 실행

`HAVING`은 GROUP BY 절에 의해 생성된 그룹 중에서 원하는 조건에 부합하는 그룹 만을 선택하는 구문

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0a234637-d92b-4147-a174-fc090facc651/d996ca12-8007-403a-9bf7-c4ca3671081d/Untitled.png)

```sql
SELECT 열, 집계함수
FROM 테이블
[WHERE 필터 조건]
GROUP BY 열
HAVING 그룹 필터 조건
```

실행 순서 : WHERE → GROUP BY → HAVING

## ORDER BY

특정 기준에 따라 정렬하는 구문

`WHERE → GROUP BY → HAVING → ORDER BY`

ASC ⇒ 오름차순, DESC ⇒ 내림차순

```sql
SELECT 열, 집계함수
FROM 테이블
[WHERE 필터 조건]
GROUP BY 열
HAVING 그룹 필터 조건
ORDER BY 열 [ASC | DESC]
```
