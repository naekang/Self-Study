# MySQL 기본 문법 정리

> 1. 일반적인 구문 뒤에는 ;을 붙이기
> 2. 키워드와 구문은 대,소문자를 구분하지 않지만 테이블명과 필드는 대,소문자를 구분하기 때문에 일관되게 주의해서 사용하기

## DATABASE 생성
```sql
CREATE DATABASE 데이터베이스 이름

ex) CREATE DATABASE opentutorials;
```

## DATABASE 선택
```sql
USE 데이터베이스 이름

ex) USE opentutorials;
```

## TABLE 생성
```sql
CREATE TABLE topic
(
    id INT(11) NOT NULL AUTO_INCREMENT,
    -- NOT NULL 제약조건 : 해당필드에 NULL값을 저장할 수 없음(무조건 데이터를 가져야 함)
    -- AUTO_INCREMENT : 기본 값 1에서 새로운 record에 대해 1씩 증가
    title VARCHAR(100) NOT NULL,
    description TEXT NULL,
    -- NULL : 필드값이 없는것을 허용함
    created DATETIME NOT NULL,
    author VARCHAR(30) NULL,
    profile VARCHAR(100) NULL,
    PRIMARY KEY(id)
    -- PRIMARY KEY : TABLE에서 유일한 값으로 테이블당 하나의 필드에만 설정 가능
);
```

## SHOW 명령어
- 데이터베이스 또는 테이블 목록을 보기 위해 사용

1. 데이터베이스 목록 보기
```sql
SHOW DATABASES; -- 복수형으로 사용해야함
```
2. 데이터베이스 안의 테이블 목록 보기
```sql
SHOW TABLES;
```
3. 현재 데이터베이스에서 조건에 맞는 테이블 목록 보기
```sql
SHOW TABLES LIKE '키워드%';
```
4. 특정 데이터베이스에 있는 테이블 목록 보기
```sql
SHOW TABLES FROM 데이터베이스 이름;
```
5. 특정 데이터베이스에서 조건에 맞는 테이블 목록 보기
```sql
SHOW TABLES FROM 데이터베이스 이름 LIKE '키워드%';
```
6. 특정 테이블에 있는 인덱스 보기
```sql
SHOW INDEX FROM 테이블 이름;
```
7. 특정 테이블에 있는 컬럼 보기
```sql
SHOW COLUMNS FROM 테이블 이름;
```
8. 특정 데이터베이스에 모든 테이블 정보 보기
```sql
SHOW TABLES STATUS FROM 데이터베이스 이름;
```

## 테이블에 대한 설명 알아보기
```sql
DESC topic;
-- 내부 데이터를 표 형식으로 제공
```

## INSERT INTO로 레코드 추가
```sql
INSERT INTO topic(title,description,created,author, profile)
VALUES('MySQL','MySQL is ...',NOW(),jinhoKim,'student');
```

## SELECT문
- 테이블의 레코드 선택
```sql
SELECT * FROM 테이블 이름;
-- 해당 테이블의 모든 필드 선택

SELECT * FROM 테이블 이름 WHERE 필드 이름 = '필드값';
-- 특정 조건에 맞는 레코드 선택

SELECT DISTINCT 필드 이름 FROM 테이블 이름;
-- 특정 테이블에서 특정 필드 선택 단, 중복 값은 한번만 선택

SELECT * FROM 테이블 이름 ORDER BY 필드 이름;
-- 특정 테이블의 모든 레코드를 특정 필드의 오름차순으로 정렬 

SELECT * FROM 테이블 이름 ORDER BY 필드 이름 DESC;
-- 특정 테이블의 모든 레코드를 특정 필드의 내림차순으로 정렬
```

## UPDATE
```sql
UPDATE 테이블 이름 
SET 필드 이름 = '변경할 필드값' 
WHERE 필드 이름 = '필드값';
```

## DELETE
- 잘못 사용하면 인생 고달파짐
```sql
DELETE FROM 테이블 이름
WHERE 필드 이름 = '필드값';
```
