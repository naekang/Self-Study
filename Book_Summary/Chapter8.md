# Chapter2.5 - 다른 개발자를 배려하는 주석 쓰기
---

## 코드는 의미를, 주석은 의도를
- 개발자가 의도를 전달하는 이유는 다른 개발자를 위한 것
    ```java
    letsEatSomething() // 내가 배가 고픈 상황
    letsEatSomething() // 네가 배가 고픈 상황
    letsEatSomething() // 내가 심심한 상황
    ```

## 주석의 반복
- 문서를 처음부터 보는 경우는 반복이 필요가 없을 것임
- 특정 부분만 검색해서 확인하고자 할때는 주석이 필요할 것임
- 독자에 따라 작성하는 것이 좋음

## 주석의 발췌와 요약
- 중요한 부분을 뽑으려면 덜 중요한 것을 빼야함
- 예시
    ```java
    // 사용자가 레벨업하려면 로그인을 10회 이상하고 게시물을 5개 이상 작성해야 한다.
    if(user.getLoginCount() >= 10 && user.getOwnArticleCount() >= 5) {
        int level = user.getLevel();
        user.setLevel(level++);
    } 
    ```
    - 승급 조건과 승급의 상위 개념을 사용하여 주석을 간단하게 나타내는 방법도 가능
    - 리팩토링을 통해 주석 없애기
    ```java
    if(user.enoughToLevelUp()) {
        user.levelup();
    }
    ```

## 주석도 코드다
- 급하게 코드를 수정하다보면 주석에 오류가 생기는 경우가 발생할 수 있음
- 주석도 코드라고 생각하며 코드 리뷰시 꼼꼼하게 살피기