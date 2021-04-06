# Chapter15 - let, const 키워드와 블록 레벨 스코프
---

## 15.1 var 키워드로 선언한 변수의 문제점
- ES5까지 변수 선언의 유일한 방법은 var 키워드 이용

### 15.1 변수 중복 선언 허용
```javascript
var x = 1;
var y = 1;

// var 키워드는 중복 선언 허용
// 초기화문이 있는 변수 선언문은 var 키워드가 없는 것처럼 동작
var x = 100;
var y;

console.log(x); // 100
console.log(y); // 1
```

### 15.1.2 함수 레벨 스코프
- 오직 코드 블록만 지역 스코프로 인정
- 특히 for문에서 중복 선언 조심
    ```javascript
    var i = 10;

    for (var i = 0; i < 5; i++) {
        console.log(i) // 0 1 2 3 4
    }

    console.log(i); // 5
    ```

### 15.1.3 변수 호이스팅
- 할당문 이전에 변수 참조하면 undefined 반환


## 15.2 let 키워드
- ES6 이후 var 키워드의 단점을 보완하기 위해 도입

### 15.2.1 변수 중복 선언 금지
```javascript
var foo = 123;
// var 키워드로 선언된 변수는 중복 선언 허용
var foo = 456;

let bar = 123;
// let이나 const 키워드는 중복 선언 비허용
let bar = 456; // SyntaxError
```

### 15.2.2 블록 레벨 스코프
- 모든 코드 블록을 지역 스코프로 인정하는 블록 레벨 스코프를 따름
    ```javascript
    let foo = 1; // 전역 변수
    {
        let foo = 2; // 지역 변수
        let bar = 3; // 지역 변수
    }
    console.log(foo); // 1
    console.log(bar); // ReferenceError: bar is not defined
    ```

### 15.2.3 변수 호이스팅
- 변수 호이스팅이 발생하지 않는 것처럼 동작
- let 키워드의 경우 var 와 달리 선언과 초기화가 분리되어 진행 -> 일시적 사각지대(TDZ) 생성

### 15.2.4 전역 객체와 let
```javascript
// 브라우저 환경에서 실행

// 전역 변수
var x = 1;
// 암묵적 전역
y = 2;
// 전역 함수
function foo() {
    // var 키워드로 선언한 전역 변수는 전역 객체 window의 프로퍼티
    console.log(window.x); // 1
    // 전역 객체 window의 프로퍼티는 전역 변수처럼 사용
    console.log(x); // 1

    // 암묵적 전역은 전역 객체 window의 프로퍼티
    console.log(window.y); // 2
    console.log(y); // 2

    // 함수 선언문으로 정의한 전역 함수는 전역 객체 window의 프로퍼티
    console.log(window.foo); // f foo() {}
    // 전역 객체 window의 프로퍼티는 전역 변수처럼 사용
    console.log(foo); // f foo() {}
}
```

## 15.3 const 키워드
- 상수 선언을 위해 사용

### 15.3.1 선언과 초기화
- const 키워드로 선언한 변수는 반드시 선언과 동시에 초기화 해야함

### 15.3.2 재할당 금지
- var, let과 달리 재할당 금지

### 15.3.3 상수
- 상태 유지와 가독성, 유지보수의 편의성을 위해 적극적인 사용 권장
    ```javascript
    // 변수이름을 대문자로 선언하여 상수임을 명확히
    const TAX_RATE = 0.1;

    // 세전 가격
    let preTaxPrice = 100;

    let afterTaxPrice = preTaxPrice + (preTaxPrice * TAX_RATE);

    console.log(afterTaxPrice); // 10
    ```

### 15.3.4 const 키워드와 객체
- const 키워드로 선언된 변수에 객체를 할당한 경우 값 변경 가능
    ```javascript
    const person = {
        name: 'Lee'
    };

    // 객체는 변경 가능, 재할당 없이 변경 가능
    person.name = 'Kim';

    console.log(person); // {name: "Kim"}
    ```