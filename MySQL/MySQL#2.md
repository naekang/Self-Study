# MySQL 기본 문법 정리
---

## MySQL Numeric types
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