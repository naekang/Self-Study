# Chapter4 - 변수
---

## 4.1 변수란 무엇인가? 왜 필요한가?
- 어플리케이션은 데이터를 입력(input)받고 처리하여 출력(output)
- 10 + 20 를 이해하기 위해 필요한 개념
    - 10, 20, + 기호(literal, operator)의 의미
    - 10+20 식의 의미 해석(parsing)
- CPU로 연산하고 메모리로 데이터 기억
- 메모리는 데이터 저장이 가능한 메모리 셀의 집합체로 하나당 1byte(8bits)
- 각 셀은 고유한 메모리 주소를 갖게되며 이 주소는 메모리 공간의 위치를 나타내며 정수로 표현
- 10과 20을 더하는 연산까지 마치고 30이라는 결과가 나와 메모리에 저장하였으나 재사용 불가능 <- 메모리에 직접 접근하는것은 치명적인 오류발생 위험이 있기에 허용하지 않음

> 프로그래밍 언어는 기억하고 싶은 값을 메모리에 저장하고 필요할때 마다 재사용하기 위해 변수라는 메커니즘을 이용

- 변수에 여러개 값 저장하기 - 배열이나 객체 사용
    ```javascript
    // 변수는 보통 하나의 값을 저장하기 위해 사용
    var userId = 1;
    var userName = 'Lee';

    // 객체나 배열을 사용하여 여러 값을 저장 가능
    var user = { id: 1, name: 'Lee' };

    var users = [
        { id: 1, name: 'Lee' },
        { id: 2, name: 'Kim' }
    ];
    ```

- 변수 선언 방식
    ```javascript
    var result = 10 + 20;
    ```
- result : 변수명, 30 : 변수 값, 변수에 값을 저장하는 것 : 할당

## 4.2 식별자
- 변수명을 식별자(identifier)라고도 함 -> 식별 가능한 고유한 이름
- 식별자는 값이 아니라 메모리 주소를 기억

## 4.3 변수 선언
- var, let, const 키워드를 사용하여 선언
- var 키워드
    - ES6 이전에 변수 선언 방식으로 함수 레벨 스코프만을 지원하기 때문에 의도치않게 전역 변수를 선언하는 문제 발생
    ```javascript
    var score; // 변수 선언
    ```
    - var 변수 선언은 선언 단계와 초기화 단계가 동시에 진행 (값을 할당하지 않으면 undefined 값을 갖게됨)

## 4.4 변수 선언의 실행 시점과 변수 호이스팅
```javascript
console.log(score);
var score;
```
- 변수 선언이 소스코드가 한줄씩 순차적으로 실행되는 시점(run time)이 아니라 그 이전 단계에서 먼저 실행
- 따라서 위 코드의 결과로 undefined가 출력
- 자바스크립트에서는 순차적인 실행이 아닌 변수 선언을 최우선으로 끌어올려 동작하며 이를 변수 호이스팅(Variable Hoisting)이라고 함

## 4.5 값의 할당
- 할당 연산자 = 사용
```javascript
var score = 80; // 변수 선언 + 값 할당
```
- 변수 선언은 코드가 순차 실행되는 시점인 런타임 이전에 실행이 되고 할당은 런타임에 실행
    ```javascript
    console.log(score); // undefined

    var score; // 변수 선언
    score = 80; // 값 할당

    console.log(score); // 80

    // 이때 undefined가 저장되어있던 메모리 공간을 지우고 80을 저장하는 것이 아니라 새로 메모리 공간을 확보하고 할당 값을 저장함
    ```

## 4.6 값의 재할당
- var 키워드 선언 변수는 값의 재할당 가능
    ```javascript
    var score = 80; // 변수 선언과 값의 할당
    score = 90; // 값의 재할당
    ```
- 이 역시 처음 80이 저장되어있던 메모리 공간이 아닌 새로운 메모리 공간을 확보하여 저장
- 가비지 콜렉터(garbage collector): 할당한 메모리 공간을 주기적으로 검사하여 사용하지 않는 메모리 해제 -> 메모리 누수 방지

- Unmanaged language vs Managed language
    - C언어의 경우 개발자가 메모리를 직접 해체, 할당할 수 있는 malloc(), free() 같은 저수준 제어 기능을 제공하는 Unmanaged language
    - 자바스크립트는 치명적 오류를 동반할 수 있는 직접적인 메모리 제어를 허용하지 않는 Managed language

## 4.7 식별자 네이밍 규칙
- 식별자는 특수문자를 제외한 문자, 숫자, (_), ($)를 포함할 수 있다.
- 단, 식별자는 특수문자를 제외한 문자, (_), ($)로 시작해야한다. 숫자는 허용하지 않는다.
- 예약어는 식별자로 사용할 수 없다. (ex. await, do, in 등등)

- 자바스크립트는 대소문자 구별 / 유니코드를 허용하긴 하지만 권장하지는 않음
- 변수 선언에 주석이 필요하다면 존재 목적을 드러내지 못한것이다!

- 가장 자주 사용하는 네이밍 컨벤션
    ```javascript
    // 카멜 케이스(camelCase)
    var firstName;

    // 스네이크 케이스(snake_case)
    var first_name;

    // 파스칼 케이스(PascalCase)
    var FirstName;

    // 헝가리언 케이스(typeHungarianCase)
    var strFisrtName; // type + identifier
    var $elem = document.getElementById('myId'); // DOM 노드
    var observable$ = fromEvent(document, 'click'); // RxJS 옵저버블
    ```

> 변수나 함수의 이름은 camelCase, 생성자 함수나 클래스 이름에는 PascalCase