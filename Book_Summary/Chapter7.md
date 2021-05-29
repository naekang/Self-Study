# Chapter2.4 - 좋은 코드에는 주석이 없다?
---

## 이름을 잘 지으면 주석을 줄일 수 있다
- 이름이 주석을 대신할 수 있도록
    ```java
    // bad example
    // 스크린 최대 높이를 480으로 지정
    int h = 480;
    // 사용자 유형을 분류해서 등급 값을 리턴
    levelUser();

    // good example
    int screenHeightMax = 480;
    classifyUserAndReturnClass();
    ```

## 처음부터 주석 없이 코딩하는 연습을 하자
- JSON에는 주석을 달 수 없었음
    ```
    // 요청에 대한 성공/실패 여부 구분
    "isRequestSucess": true,
    // 잘못된 이메일 주소 형식, 추가하지 않음
    "noCreatedBecauseWrongEmail": [
    ]
    ```

## 주석이 필요한 때도 많다
- `updatedInformationExceptEmail`은 '이메일을 빼고 나머지 정보가 업데이트됨' or except를 몰라서 해석을 못함
- 영어를 잘 못하면 주석 달기
- 이럴 경우 주석이 코드의 정확성을 높이고 버그를 줄이는 계기가 됨