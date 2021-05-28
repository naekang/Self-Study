# Chapter2.2 - 변수 이름을 잘 짓는 법
---

## i는 변수 이름이지만 d는 아니다
- 반복문, 조건문 등에서 가장 많이 사용하는 i는 사실 integer의 약자
    ```java
    // Bad Example
    int d;
    int m;
    int y;

    // Good Example 
    int someday;
    int today;
    int thisMonth;
    int finalYear;
    int daysSinceCreated;
    int monthSinceUpdated;
    int yearsSinceRegistered;
    ```

## 긴 이름? 짧은 이름? 검색 잘 되는 이름!
- 변수길이와 오탈자와는 이제 별개
- 검색이 쉽도록!

## 복수형을 나타내는 s를 붙여야 하나
- 변수명은 짧기에 s가 눈에 잘 띄지만 함수명은 길어서 잘 보이지 않음
- `-s`보다 `list of` 같은걸로 대체 하는 것이 좋을 수 있음
    ```java
    checkUserNameArrayUnder2Characters()
    checkListOfUserNameExistsInDB()
    ```

## 약어를 쓰는 것이 좋을까? 안 쓰는 것이 좋을까?
- 용어 정의서에 약어 설명 추가
- 서비스, 패키지, 클래스 이름에 약어 사용
    ```
    Amazon Web Service Simple Storage Service -> AWS S3
    Clova Extensions Kit -> CEK
    Clova Interface Connect -> CIC
    KakaoMessageTemplate -> KMT
    ```
- 보편성을 기준으로 약어 정하기

## 중요한 단어를 앞에 쓴다
- 여러 단어를 조합할 때 중요한 단어를 앞에!
    ```java
    int visitorTotal;
    int registerTotal;
    int vipCount;
    int windowSizeMax;
    ```

## 함수 이름 짓는 순서
1. 문장 간결하게 만들기
2. 문장 조각내기
3. 조각낸 문장을 영어로 변경
4. 정관사나 불필요한 단어 제거 및 of는 앞뒤 바꾸기
5. 띄어쓰기 없애기
6. 두번쨰 단어 첫글자 대문자로 변경
7. 의미상 없어도 되는 단어 없애기
    ```java
    // 사용자 이름을 input태그에서 가져옴
    getUserNameFromField();
    //글자 수가 2글자 이하면 다음과 같이 처리
    checkUserNameUnder2Character();
    ```

