# MySQL 타입
---

## MySQL 숫자 타입
1. 정수 타입(Integer types)
    type|저장공간
    --|--
    TINYINT|1byte
    SMALLINT|2byte
    MEDIUMINT|3byte
    INT|4byte
    BIGINT|8byte

2. 고정 소수점 타입(fixed-point types)
- 소수부의 자릿수를 미리 정해두고 고정된 자릿수로만 소수 부분을 표현하는 방식
    ```sql
    DECIMAL(M,D)
    -- D는 소수부분의 자릿수
    -- M은 소수부분 포함 실수의 총 자릿수
    ```

3. 부동 소수점 타입(floating-point types)
- FLOAT와 DOUBLE은 실수 값을 대략적으로 표현하기 위해 사용
    ```sql
    FLOAT(M,D)
    DOUBLE(M,D)
    ```

4. 비트값 타입(bit-value type)
- 0,1의 binary값 저장
- M의 범위는 1부터 64까지
    ```sql
    BIT(M)
    ```

## MySQL 문자열 타입
1. CHAR과 VARCHAR
- CHAR는 고정 길이 문자열
- VARCHAR는 가변 길이 문자열
    ```sql
    CHAR(M)
    VARCHAR(M)
    -- M은 저장할 수 있는 문자열의 최대 길이
    ```

2. BINARY와 VARBINARY
- 문자열이 아닌 binary데이터 저장

3. BLOB과 TEXT
- BLOB은 다양한 크기의 binary데이터 저장
- TEXT는 문자열의 대소문자 구별

4. ENUM
- 미리 정의한 집합안의 요소중 하나만 저장
    ```sql
    ENUM('데이터값1','데이터값2',...)
    ```

5. SET
- 미리 정의한 집합 요소 중 여러개를 동시 저장
    ```sql
    SET('데이터값1','데이터값2',...)
    ```

## MySQL 날짜와 시간 타입
1. DATE, DATETIME, TIMESTAMP
- DATE: 날짜 저장, YYYY-MM-DD
- DATETIME: 날짜 + 시간, YYYY-MM-DD HH:MM:SS
- TIMESTAMP: 최종 변경 시각 저장

2. TIME
- 시간 저장, HH:MM:SS

3. YEAR
- 연도 저장