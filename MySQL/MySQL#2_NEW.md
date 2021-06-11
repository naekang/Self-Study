# Chapter 2 - MySQL 전체 운영 실습
---

## 3.1 요구사항 분석과 시스템 설계 그리고 모델링

### 3.1.1 정보시스템 구축 절차 요약
1. __분석__: 현재 우리가 무엇(What)을 할 것인지
2. __설계__: 시스템을 어떻게 할 것인지
3. __구현__
4. __시험__
5. __유지보수__

### 3.1.2 데이터베이스 모델링과 필수 용어
- 데이터베이스 모델링: 현실 세계에서 사용되는 데이터를 MySQL로 어떻게 옮겨 놓을지 결정하는 과정
- 데이터: 하나하나의 단편적인 정보, 체계화되지 않은 정보들
- 테이블: 데이터를 입력하기 위해 표현된 표
- 데이터베이스(DB): 테이블이 저장되는 저장소
- DBMS(Database Management System): 데이터베이스를 관리하는 시스템 및 소프트웨어
- 열(Column): 각 테이블은 열로 구성
- 열 이름: 각 열을 구분하기 위한 이름
- 데이터 형식: 열의 데이터 형식
- 행(Row): 실질적인 데이터
- 기본키(Primary Key) 열: 각 행을 구분하는 유일한 열
- 외래키(Foreign Key) 필드: 두 테이블의 관계를 맺어주는 키
- SQL: 사람과 DBMS가 소통하기 위한 언어


## 3.2 MySQL을 이용한 데이터베이스 구축 절차
- 여기서는 Workbench를 이용하여 실습

### 3.2.1 데이터베이스 생성
- 쇼핑몰 데이터베이스 생성 실습
- Workbench를 이용하여 `Create Schema`를 통해 `shopdb` 데이터베이스 추가

### 3.2.2 테이블 생성
- memberTBL
    열 이름(한글)|영문 이름|데이터 형식|길이|NULL 허용
    --|--|--|--|--
    아이디|memberID|문자(CHAR)|8글자(영문)|X
    회원 이름|memberName|문자(CHAR)|5글자(한글)|X
    주소|memberAddress|문자(CHAR)|20글자(한글)|O

- productTBL
    열 이름(한글)|영문 이름|데이터 형식|길이|NULL 허용
    --|--|--|--|--
    제품 이름|productName|문자(CHAR)|4글자(한글)|X
    가격|cost|숫자(INT)|정수|X
    제조일자|makeDate|날짜(DATE)|날짜형|O
    제조회사|company|문자(CHAR)|5글자(한글)|O
    남은 수량|amount|숫자(INT)|정수|X

- Workbench에서 테이블을 선택한 후 오른쪽 마우스를 누르고 `Create Table`

### 3.2.3 데이터 입력
- [SCHEMAS] -> [ShopDB] -> [Tables] -> [memebertbl] -> [Select Rows - Limits 1000]
- Result Grid에서 직접 입력 가능

### 3.2.4 데이터 활용
- `SELECT문`의 활용
- 제품 테이블의 모든 데이터 조회하기
    ```sql
    SELECT * FROM productTBL;
    ```

- 회원 테이블 중에 이름과 주소만 출력
    ```sql
    SELECT memberName, memberAddress FROM memberTBL;
    ```

- 새로운 테이블 생성 방법
    ```sql
    CREATE TABLE `my TestTBL` (id INT);
    ```


## 3.3 테이블 외의 데이터베이스 개체의 활용

### 3.3.1 인덱스
- 색인과 같은 개념
- 시스템 성능을 결정하는 중요한 요인
- 인덱스가 없다면 테이블 전체를 검색해야 함

### 3.3.2 뷰
- 가상의 테이블로 실제는 없는 진짜 테이블에 Link된 개념

### 3.3.3 스토어드 프로시저
- SQL문을 하나로 묶어 편리하게 사용하는 기능
- 매번 같은 긴 SQL 문장들을 쓸 경우 불편함 해소
    ```sql
    DELIMITER //
    CREATE PROCEDURE myProc()
    BEGIN
        SELECT * FROM memberTBL WHERE memberName = '당탕이';
        SELECT * FROM productTBL WHERE productName = '냉장고';
    END //
    DELIMITER ;
    ```

### 3.3.4 트리거
- 테이블에 부착되어 테이블에 INSERT나 UPDATE 또는 DELETE 작업이 발생되면 실행되는 코드
- 특정 조건이 만족하면 저절로 실행되는 장치 ex) 삭제 데이터 -> 백업 테이블


## 3.4 데이터베이스 백업 및 관리

### 3.4.1 백업과 복원
- 백업: 데이터베이스를 다른 매체에 보관하는 작업
- 복원: 데이터베이스에 문제가 발생했을 때 다른 매체에 백업된 데이터를 이용해 원상태로 복구하는 작업
- [Navigator] -> [Administration] -> [Data Export]