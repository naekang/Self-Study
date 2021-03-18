# Chapter6 - 데이터 타입
---
> 자바스크립트(ES6 기준)는 7개의 데이터 타입 제공

## 6.1 숫자 타입(number)
- int, long, float 등이 있는 c, java와는 달리 하나의 숫자 타입만 존재
- ECMAScript 사양에 따라 64비트 부동소수점 형식을 따름
- 2진수, 8진수, 16진수 데이터 타입이 없기때문에 모두 10진수 형태로 해석
- 양, 음의 무한대, NaN(not-a-number) 값 표현 가능
    ```javascript
    console.log(10 / 0);
    console.log(10 / -0);
    console.log(1 * 'String');
    ```

## 6.2 문자열 타입(string)
- 작은따옴표(''), 큰따옴표(""), 백틱(``)으로 텍스트를 감쌈
- 키워드, 식별자 같은 토큰과 구분을 위해
- 어떤 형식으로 하든 통일성 있게 진행하는 것이 중요

## 6.3 템플릿 리터럴(template literal)
- 멀티라인 문자열, 표현식 삽입, 태그드 템플릿 등 문자열 처리 기능 제공
- 백틱(``)을 사용하여 표현

### 6.3.1 멀티라인 문자열
- 공백을 표현하기 위해 (\)로 시작하는 escape sequence 사용

Escape sequence|의미
--|--
\0|NULL
\b|백스페이스
\f|Form Feed : 프린터로 출력할 경우 다음 페이지의 시작점으로 이동
\n|Line Feed : 개행, 다음 행으로 이동
\r|Carriage Return : 개행, 커서를 처음으로 이동
\t|탭(수평)
\v|탭(수직)
\uXXXX|유니코드
\'|작은따옴표
\"|큰따옴표
\\|백슬래시

- 개행문자 LF, CR 차이 : LF는 커서를 정지한 상태에서 종이를 한 줄 올리는 것, CR은 종이는 그대로고 커서를 맨 앞줄로 이동하는 것 / 운영체제마다 다른 개행 방식 사용

- 줄바꿈과 들여쓰기가 적용된 HTML 문자열 예시
    ```javascript
    var template = '<ul>\n\t<li><a href="#">Home</a></li>\n</ul>';

    console.log(template);
    ```
    ```html
    <ul>
        <li><a href="#">Home</a></li>
    </ul>
    ```
- 템플릿 리터럴의 경우 줄바꿈과 공백이 그대로 출력
    ```javascript
    var template = `<ul>
        <li><a href="#">Home</a></li>
    </ul>`
    ```
    ```html
    <ul>
        <li><a href="#">Home</a></li>
    </ul>
    ```

### 6.3.2 표현식 삽입
- +를 사용하여 연결 가능
- My name is Jinho Kim.을 출력하는 방법
    ```javascript
    var first = 'Jinho';
    var last = 'Kim';

    // ES5: 문자열 연결
    console.log('My name is ' + first + ' ' + last + '.');

    // ES6: 표현식 삽입
    console.log(`My name is ${first} ${last}.`);
    ```

- 백틱(``)과 작은따옴표('')를 헷갈리지 않게 주의해야 함

## 6.4 불리언 타입
- 논리 참 : true, 논리 거짓 : false
- 조건문에서 자주 사용

## 6.5 undefined 타입
- var 키워드로 선언한 변수는 암묵적으로 undefined로 초기화
- 의도적으로 할당하는 것은 취지에 어긋나기에 권장하지 않음
- 변수에 값이 없음을 명시하기 위해서는 null을 할당
- 선언과 정의 : 대상을 명확히 규정하는 것
    1. 선언(declaration)
        - 변수에 주로 사용
    2. 정의(definition)
        - 함수에 주로 사용

## 6.6 null 타입
- 변수에 값이 없음을 의도적으로 명시
- 함수가 유효한 값을 반환할 수 없는 경우 null을 반환

## 6.7 심벌 타입
- 충돌 위험이 없는 객체의 유일한 프로퍼티 키를 만들기 위해 사용
    ```javascript
    // 심벌 값 생성
    var key = Symbol('key');
    console.log(typeof key); // symbol

    // 객체 생성
    var obj = {};

    // 이름이 충돌할 위험이 없는 유일무이한 값인 심벌을 프로퍼티 키로 사용
    obj[key] = 'value';
    console.log(obj[key]); // value
    ```

## 6.8 객체 타입
- 자바스크립트는 객체 기반의 언어로 자바스크립트를 이루고 있는 거의 모든 것이 객체

## 6.9 데이터 타입의 필요성

### 6.9.1 데이터 타입에 의한 메모리 공간의 확보와 참조
```javascript
var score = 100;
```
- 위 코드가 실행되면 100을 저장하기 위해 메모리 공간 확보 후 100을 2진수로 저장
- 이때 변수에 할당되는 값의 데이터 타입에 따라 확보해야 할 메모리 공간의 크기 결정
- 100을 저장하기 위해서는 8바이트의 메모리 공간 확보 후 2진수 형태로 저장

### 6.9.2 데이터 타입에 의한 값의 해석
- 데이터 타입이 필요한 이유
    1. 값을 저장할 때 확보해야하는 메모리 공간의 크기를 결정하기 위해
    2. 값을 참조할 때 한 번에 읽어 들여야 할 메모리 공간의 크기를 결정하기 위해
    3. 메모리에서 읽어들인 2진수를 어떻게 해석할지 결정하기 위해

## 6.10 동적 타이핑

### 6.10.1 동적 타입 언어와 정적 타입 언어
- 정적 타입 언어 : 변수 선언 시 데이터 타입을 같이 선언해야함
    ```c
    char C;
    int num;
    ```
- typeof 연산자를 이용하여 데이터 타입 조사 가능
    ```javascript
    var foo;
    console.log(typeof foo); // undefined

    foo = 3;
    console.log(typeof foo); // number

    foo = 'Hello';
    console.log(typeof foo); // string

    foo = true;
    console.log(typeof foo); // boolean

    foo = null;
    console.log(typeof foo); // object

    foo = Symbol(); // 심벌
    console.log(typeof foo); // symbol

    foo = {}; // 객체
    console.log(typeof foo); // object

    foo = []; // 객체
    console.log(typeof foo); // object

    foo = function () {}; // 함수
    console.log(typeof foo); // function
    ```

- 동적 타입 언어 : 자바스크립트는 선언이 아닌 할당에 의해 타입이 결정되며 동적인 변화 가능(타입 추론)

### 6.10.2 동적 타입 언어와 변수
- 값의 변경에 따라 타입은 언제든지 변경이 가능하며 자동으로 변환 -> 유연성은 높지만 신뢰성은 떨어짐
- 변수 사용시 주의사항
    1. 변수가 많으면 오류 발생 가능성이 높아지기 때문에 신중하게 제한적으로 선언하기
    2. 변수 유효 범위를 최대한 좁게 만들어 부작용 억제
    3. 전역변수는 의도치 않게 변경될 수 있고 오류 발생 시 원인 특정을 어렵게 만들기 때문에 사용 자제
    4. 변수보다는 상수를 사용해 값의 변경을 억제
    5. 변수 이름은 반드시 목적이나 의미를 파악할 수 있도록!


> **가독성이 좋은 코드가 진정한 좋은 코드!!!!!**