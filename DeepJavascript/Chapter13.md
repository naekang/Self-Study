# Chapter13 - 스코프
---

## 13.1 스코프란?
- 모든 식별자는 자신이 선언된 위치에 의해 다른 코드가 식별자 자신을 참조할 수 있는 유효범위 결정
- 즉, 식별자가 유효한 범위
- 식별자 결정 시 사용하는 규칙으로 할 수 있음
    ```javascript
    var x = 'global';

    function foo() {
        // foo 함수 내부에서만 참조 가능
        var x = 'local';
        console.log(x); // local
    }

    foo();

    console.log(x); // global
    ```

- var 키워드로 선언한 변수는 중복 선언 허용 -> 재할당으로 인한 부작용 발생 가능성이 있음
- let, const 키워드 변수는 중복 선언 허용하지 않음

## 13.2 스코프의 종류

구분|설명|스코프|변수
--|--|--|--
전역|코드의 가장 바깥 영역|전역 스코프|전역 변수
지역|함수 몸체 내부|지역 스코프|지역 변수

### 13.2.1 전역과 전역 스코프
```javascript
var x = "global x";
var y = "global y";

function outer() {
    var z = "outer's local z";

    console.log(x); // global x
    console.log(y); // global y
    console.log(z); // outer's local z
    
    function inner() {
        var x = "inner's local x";

        console.log(x); // inner's local x
        console.log(y); // global y
        console.log(z); // outer's local z
    }

    inner();
}
outer();

console.log(x); // global x
console.log(y); // ReferenceError : z is not defined
```
- 전역변수는 어디서든지 참조 가능

### 13.2.2 지역과 지역 스코프
- 지역 변수는 자신의 지역 스코프와 하위 지역 스코프에서 유효

## 13.3 스코프 체인
- 스코프는 함수의 중첩에 의해 계층적 구조를 갖게 될수도 있음
    1. 전역스코프
        변수|값
        --|--
        x|"global x"
        y|"global y"
        outer|&#60;function object&#62;
        ⬆︎
    2. outer 지역 스코프
        변수|값
        --|--
        z|"outer's local z"
        inner|&#60;function object&#62;
        ⬆︎
    3. inner 지역 스코프
    
        변수|값
        --|--
        x|"inner's local x"

- 변수를 참조할 때 자바스크립트 엔진은 스코프 체인을 통해 변수를 참조하는 코드의 스코프에서 시작하여 상위 스코프로 이동하며 변수 검색
- Lexical Environment를 물리적으로 생성

### 13.3.1 스코프 체인에 의한 변수 검색
- 상위 스코프는 하위 스코프를 자유롭게 참조 가능
- 하위 스코프는 상위 스코프 참조 불가능

### 13.3.2 스코프 체인에 의한 함수 검색
```javascript
// 전역 함수
function foo() {
    console.log("global function foo");
}

function bar() {
    // 중첩 함수
    function foo() {
        console.log("local function foo");
    }

    foo(); // foo 함수를 호출하면 함수를 가리키는 식별자 foo 검색
}

bar();
```

## 13.4 함수 레벨 스코프
- 코드 블록이 아닌 함수에 의해 지역 스코프 생성 = block level scope

## 13.5 렉시컬 스코프
1. 동적 스코프: 함수를 어디서 호출했는지를 기준
2. 렉시컬 스코프(정적 스코프): 함수를 어디서 정의했는지를 기준

- 자바스크립트는 렉시컬 스코프를 따름
    ```javascript
    var x = 1;

    function foo() {
        var x = 10;
        bar();
    }

    function bar() {
        console.log(x);
    }

    foo(); // 1
    bar(); // bar 함수는 전역코드가 실행되기 전 먼저 평가되므로 1 출력
    ```