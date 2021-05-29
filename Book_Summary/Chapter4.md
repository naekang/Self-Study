# Chapter2.1 - 네이밍 컨벤션, 이유를 알고 쓰자
---

## 개발자의 가장 큰 고민은 이름 짓기
- 개발자는 이름 짓는데 가장 많은 시간을 소요한다.
- 주석 없이도 코드를 이해하도록 하기 위함
- 변수, 함수 이름을 짓기 위해서는 한번에 무슨 뜻인지, 기능은 무엇인지 알아야하고 간결해야 함

## 이름 짓기는 창조가 아니라 조합
- [오픈소스의 네이밍 특징들](https://brunch.co.kr/@goodvc78/12)
- 자바 네이밍 컨벤션 철저히 준수
  - 클래스는 UpperCamelCase
  - 함수와 변수는 lowerCamelCase
  - 상수는 UPPER_DELIMITER_CASE

- 네이밍은 보통 16글자, 3단어 조합
  - 클래스: 3.18 단어
  - 함수: 3.36 단어
  - 변수: 2.57 단어

- 품사는 주로 명사, 동사, 형용사 조합
  - 명사 + 명사 + 명사
  - 동사 + 명사 + 명사
  - 형용사 + 명사 + 명사

## 코드의 네이밍 컨벤션은 영어 표기법을 상속받았다
- 고유 명사는 문장 어느 위치에 있든 대문자
    `I went to Tokyo.`
- 이름 앞 직함은 첫 글자 대문자
    `Doctor Mr.Micheal`
- 책, 신문, 잡지 등 제목 첫 단어와 마지막 단어, 관사는 대문자
    `Marvel's The Avengers`
- 명사 다음 숫자가 올 때 명사 첫 글자는 대문자
    `Section 2`
- 요일명, 휴일명, 달, 역사적 사건, 역사적 기간은 첫 글자 모두 대문자
    `World War 2`
- 천체의 이름은 첫 글자 대문자
    `It is the Mars`

## 파스칼 표기법으로 클래스 이름 짓기
- 모든 단어에서 첫 글자를 대문자로
    ```java
    interface Menu
    class CoffeeMenu implements Menu
    ```

## 카멜 표기법으로 함수, 변수 이름 짓기
- 첫 단어 빼고 나머지 대문자
    ```java
    int totalCount = 0;
    void orderCoffee();
    ```

## 상수는 모두 대문자로 작성
```java
static final int COFFEE_MAX = 10;
```

## 패키지와 모듈은 모두 소문자로 씀
- 패키지와 모듈은 단지 클래스나 함수를 모아둔 통에 불과함
    ```java
    kr.co.wikibook.android.developerwriting
    import developerwriting
    ```

## BEM 표기법
- 대상의 요소나 부분을 의미할 때는 `__`(언더바 2개)
- 대상이나 요소의 상태나 속성을 의미할 때는 `--`(하이픈 2개)
    ```css
    .form {}
    .form__button {}
    .form__button--disabled {}
    ```

## 가독성과 소통이 먼저다
- 프로그램 개발하기 전 관련 개발자들끼리 기본적인 컨벤션 규칙을 정하는 것이 우선