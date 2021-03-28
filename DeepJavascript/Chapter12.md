# Chapter12 - 함수
---

## 12.1 함수란?
- 일련의 과정을 문(statement)로 구현하고 코드 블록으로 감싸 하나의 실행 단위로 정의한 것
- 매개변수(parameter): 함수 내부로 입력을 전달받는 변수
- 인수(argument): 입력, 반환값(return value): 출력
- 함수는 함수 정의(function definition)을 통해 생성
- 생성 후 함수 호출(function call/invoke)을 통해 반환

## 12.2 함수를 사용하는 이유
- 필요할 떄 여러번 호출할 수 있음 -> 재사용 가능이란 측면에서 매우 유리
- 같은 코드가 여러번 중복될 경우 함수화하여 유지보수 편의성을 높이고 코드의 신뢰성을 높임
- 함수는 객체 타입의 값으로 이름을 붙일 수 있어 코드의 가독성이 좋아짐

## 12.3 함수 리터럴
- 함수 리터럴은 function 키워드, 함수 이름, 매개변수 목록, 함수 몸체로 구성

## 12.4 함수 정의
- 함수 선언문
    ```javascript
    function add(x,y) {
        return x + y;
    }
    ```
- 함수 표현식
    ```javascript
    var add = function (x, y) {
        return x + y;
    };
    ```
- Function 생성자 함수
    ```javascript
    var add = new Function('x', 'y', 'return x + y');
    ```
- 화살표 함수(ES6)
    ```javascript
    var add = (x, y) => x + y;
    ```

### 12.4.1 함수 선언문
- 함수 리터럴과 형태는 동일하지만 함수 이름 생략 불가능
    ```javascript
    // 함수 선언문
    function add(x, y) {
        return x + y;
    }

    // 함수 참조
    // console.dir은 console.log와 달리 함수 객체의 프로퍼티까지 출력
    // 단, Node.js 환경에서는 console.log와 같은 결과 출력
    console.dir(add); // f add(x, y)

    // 함수 호출
    console.log(add(2, 5)); // 7
    ```

- 자바스크립트 엔진은 생성된 함수를 호출하기 위해 함수 이름과 동일한 이름의 식별자를 암묵적으로 생성하고, 거기에 함수 객체 할당
- 함수는 함수 이름으로 호출하는 것이 아니라 함수 객체를 가리키는 식별자로 호출


### 12.4.2 함수 표현식
- 자바스크립트 함수는 일급 객체로 함수를 값처럼 자유롭게 사용가능
    ```javascript
    var add = function foo (x, y) {
        return x + y;
    };

    // 함수 객체를 가리키는 식별자로 호출
    console.log(add(2, 5)); // 7

    // 함수 이름으로 호출하면 ReferenceError 발생
    console.log(foo(2, 5)); // ReferenceError: foo is not defined
    ```