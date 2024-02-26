## JOIN

두 개의 테이블을 엮어야 원하는 결과가 나오는 경우 → JOIN 사용

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/16642d63-61d8-4e34-93b3-97e1df82f22d)


- INNER JOIN

⇒ 두 테이블의 교집합

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/81e171b9-cea2-441b-9baf-451c1b15b3ed)

- FULL OUTER JOIN

⇒ 두 테이블의 합집합

- LEFT OUTER JOIN

⇒ 왼쪽 테이블의 모든 값이 출력되는 조인

- RIGHT OUTER JOIN

⇒ 오른쪽 테이블의 모든 값이 출력되는 조인

<br></br>
## UNION

- 두 개의 SQL 실행 결과를 결합하는데 사용
- `UNION`은 테이블 사이에 관계성이 없어도 사용할 수 있음
- UNION은 결과에 중복된 데이터가 있을 경우 제거

```sql
[SQL 1]
UNION
[SQL 2];

EX)
SELECT name, age FROM students WHERE age < 30
UNION
SELECT name, age FROM students WHERE age < 32;
```

UNION으로 결합하기 위한 조건

- SQL 1과 SQL 2의 열 개수가 같아야 한다.
- SQL 1과 SQL 2의 열 이름이 같아야 한다.
- SQL 1과 SQL 2의 각 열의 데이터 타입이 동일해야한다.

`UNION ALL` 

- 중복 제거 없이 모두 보여줌

<br></br>
## 서브 쿼리

- 하나의 SQL문 안에 포함되어 있는 또 다른 SQL문
- 최종 결과를 출력하는 쿼리 ⇒ 메인 쿼리, 메인 쿼리의 보조 역할 ⇒ 서브 쿼리

[서브 쿼리]

1. SELECT 절에서 사용하는 서브 쿼리
    
    

```sql
SELECT
	name,
	age,
	(SELECT AVG(age) FROM students) AS avg_age
FROM students
WHERE age < 30
```

1. FROM 절에서 사용하는 서브쿼리
    
    서브쿼리의 결과를 마치 가상의 테이블처럼 사용할 수 있음
    

```sql
SELECT *
FROM
	(
		SELECT name, class_name
		FROM classes
		WHERE class_name IN ('데이터베이스', '알고리즘')
	)
```

1. WHERE 절에서 사용하는 서브 쿼리
    
    students 테이블에서 서브 쿼리에서 조회한 이름만 필터링하여 결과로 보여줌
    

```sql
SELECT name, age, address
FROM students
WHERE name IN (
	SELECT name
	FROM classes
	WHERE class_name IN ('데이터베이스', '알고리즘')
)
```

<br></br>
## DDL

- 데이터 정의 언어
- `테이블을 정의할 때 쓰는 명령어`
- DML은 데이터 조회, 삽입, 수정, 삭제

| CREATE | 새로운 테이블을 생성 |
| --- | --- |
| ALTER | 기존 테이블 구조 변경 |
| DROP | 테이블 삭제 |
| RENAME | 기존 테이블 이름 변경 |
| TRUNCATE | 기존 테이블 초기화 |

## CREATE

- 데이터베이스 생성
    
    ```sql
    CREATE DATABASE [데이터베이스명]
    ```
    

- 테이블 생성
    
    ```sql
    CREATE TABLE [데이터베이스이름].[테이블이름] (
    	[열] [데이터타입] [제약조건],
    	...
    )
    
    CREATE TABLE test_db.students (
      name VARCHAR(255) NOT NULL,
      age INT NOT NULL,
      address VARCHAR(255) NOT NULL
    )
    ```
    
- 테이블 제약조건
    
    테이블 생성 시점에 규칙을 정해놓는 것 → Constraint
    
    | 옵션 | 설명 |
    | --- | --- |
    | NOT NULL | 해당 열에 NULL 값을 허용하지 않는다는 의미입니다. |
    | DEFAULT | 데이터를 입력 시 해당 열에 아무런 값도 입력되지 않은 경우 기본으로 사용할 값 지정합니다. |
    | UNIQUE | 해당 테이블 내에서 유일한 속성을 갖는다는 의미로, UNIQUE로 설정된 열에는 중복된 값을 저장할 수 없습니다.
    데이터 무결성을 유지하는데 도움, 예를 들어 사용자 ID나 주문번호 등이 이에 해당 |
    | PRIMARY KEY | 하나의 테이블에 있는 데이터들을 식별하기 위한 기준 값
    하나의 테이블 안에 단 하나만 생성 가능 ⇒ UNIQUE +  NOT NULL 제약조건의 속성을 지님 |
    | FOREIGN KEY(외래키) | 테이블간에 관계를 나타낼 때 사용하는 Key로, 다른 테이블의 기본키를 참조해 외래키로 사용합니다.  |
    
    DEFAULT 사용 예시
    
    ```sql
    CREATE TABLE profile (
    	id VARCHAR(255) NOT NULL,
    	create_date DATE DEFAULT now()  //현재 날자 기준으로 등록됨
    )
    ```
    

FOREIGN KEY (외래키)

- 한 테이블의 외래키는 연결되어 있는 다른 테이블의 기본키 중 하나
- FK의 Column이 여러 개 일 수 있음
