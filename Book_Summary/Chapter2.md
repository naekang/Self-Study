# Chapter1.2 - 쉽게 쓰는 띄어쓰기와 문장 부호
---

## 가장 쉬운 띄어쓰기 원칙
- 조사, 순서, 숫자, 하다, 기호만 붙이고 나머지는 띄어쓰기!
- 쉼표는 앞 낱말에 붙이기
    ```javascript
    var obj = {
        arg1 = 1,
        arg2 = 2,
        arg3 = 3
    };
    ```
- 한글 숫자가 순서나 단계를 나타낼 때는 붙이기
- 숫자는 모두 뒤 낱말과 붙이기
- `장애가 발생한 지 3시간이 지나 버려서 일단계 대책이 무의미하다.(v.1.1.0).` 

- 함수 선언 시 괄호 안에 인수는 붙여쓴다.
    ```javascript
    wordSpacing(arg1, arg2)
    ```

- 맞춤법이 너무 어려울 경우 [부산대 맞춤법 사이트](https://speller.cs.pusan.ac.kr/) 이용하기

## 오해하기 쉬운 문장 부호(큰따옴표, 작은따옴표)
- 개발 언어에 따라 차이가 존재
- C언어의 경우 `" "`는 문자열, `' '`는 단일 문자
    ```c
    char str[] = "Hello World!";
    str[0] = 'A';
    ```

- SQL은 쿼리문 안에서 모두 `' '`사용
- Javascript는 주로 `' '`사용
- 큰따옴표는 글에서 직접 대화 또는 인용구 표현시
- 작은따옴표는 인용한 말 안에 인용한 말 또는 마음속으로 한 말

- 비즈니스 문서에서는 책 제목, 신문 이름에 사용하는 <> 대신 큰따옴표 사용
    ```
    이번에 출간된 "개발자의 글쓰기"를 참고했음.
    이 건은 "00신문"의 기사를 토대로 작성했음.
    ```

- 소제목이나 예술작품의 제목, 상호, 법률, 규정 등을 나타낼 떄 사용하는 홑낫표와 홑화살괄호 대신 작은 따옴표
    ```
    이번 프로젝트의 이름은 '안드로이드'로 정했음.
    이번 릴리스는 '개인정보 보호법'을 준수함.
    ```

- 강조하거나 비교할 떄도 작은따옴표
    ```
    1단계로 '원인 분석'을 철저히 한 다음 2단계를 추진해야 함.
    이 시점에서 중요한 것은 '창의'가 아니라 '열정'임.
    ```


참고문헌: [개발자의 글쓰기](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9791158391744&orderClick=LAG&Kc=#N)