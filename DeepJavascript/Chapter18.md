# Chapter18 - 함수와 일급 객체
---

## 18.1 일급 객체
- 무명의 리터럴로 생성 가능. 즉, 런타임에 생성 가능
- 변수나 자료구조에 저장 가능
- 함수의 매개변수에 전달 가능
- 함수의 반환값으로 사용 가능
```javascript
// 1. 함수는 무명의 리터털로 생성할 수 있음
// 2. 함수는 변수에 저장할 수 있음
// 런타임에 함수 리터럴이 평가되어 함수 객체가 생성되고 변수에 할당됨
const increase = function (num) {
    return ++num;
};

const decrease = function (num) {
    return --num;
};

// 2. 함수는 객체에 저장 가능
const predicates = { increase, decrease };

// 3. 함수의 매개 변수에 전달 가능
// 4. 험수의 반환값으로 사용 가능
function makeCounter(predicate) {
    let num = 0;
    
    return function () {
        num = predicate(num);
        return num;
    };
}

// 3. 함수는 매개변수에게 함수 전달 가능
const increaser = makeCounter(predicates.increase);
console.log(increaser()); // 1
console.log(increaser()); // 2

const decreaser = makeCounter(prediates.decrease);
console.log(decreaser()); // -1
console.log(decreaser()); // -2
```


## 18.2 함수 객체의 프로퍼티
```javascript
function square(number) {
    return number * number;
}

console.log(square);
```
- 브라우저 콘솔에서 `console.dir` 메서드를 사용하여 함수 객체 내부 확인
- square 함수의 모든 프로퍼티 어트리뷰트를 `Object.getOwnPropertyDescriptors` 메서드로 확인 가능

### 18.2.1 arguments 프로퍼티
- 함수 객체의 arguments 프로퍼티 값은 arguments 객체
- arguments 객체는 인수를 프로퍼티 값으로 소유하며 프로퍼티 키는 인수의 순서를 나타냄
- arguments 객체는 매개변수 개수를 확정할 수 있는 __가변 인자 함수__ 를 구현할 떄 유용함
    ```javascript
    function sum() {
        let res = 0;

        for (let i = 0; i < arguments.length; i++) {
            res += arguments[i];
        }

        return res;
    }

    console.log(sum()); // 0
    console.log(sum(1, 2)); // 3
    console.log(sum(1, 2, 3)); // 6
    ```

- arguments 객체는 유사 배열 객체
- 배열 객체를 사용하기 위해서는 `Function.prototype.call`, `Function.prototype.apply`를 사용해 간접 호출
- ES6에서는 번거로움을 해결하기 위해 Rest 파라미터 도입
    ```javascript
    // ES6 Rest parameter
    function sum(...args) {
        return args.reduce((pre, cur) => pre + cur, 0);
    }

    console.log(sum(1, 2)); // 3
    console.log(sum(1, 2, 3, 4, 5)); // 15
    ```


### 18.2.2 caller 프로퍼티
- ECMAScript 사양에 포함되지 않은 비표준 프로퍼티
- 자기 자신을 호출한 함수를 가리킴
    ```javascript
    function foo(func) {
        return func();
    }

    function bar() {
        return 'caller : ' + bar.caller;
    }

    // 브라우저에서의 실행한 결과
    console.log(foo(bar)); // caller : function foo(func) { ... }
    console.log(bar()); // caller : null
    ```

### 18.2.3 length 프로퍼티
- 함수를 정의할 떄 선언한 매개변수의 개수를 가리킴
    ```javascript
    function foo() {}
    console.log(foo.length); // 0

    function bar() {
        return x;
    }

    console.log(bar.length); // 1

    function baz(x, y) {
        return x * y;
    }

    console.log(baz.length); // 2
    ```

### 18.2.4 name 프로퍼티
- ES6에서 정식 표준으로 자리잡음
- 함수 객체를 가리키는 식별자를 값으로 갖음
    ```javascript
    // 기명 함수 표현식
    var namedFunc = function foo() {};
    console.log(namedFunc.name); // foo

    // 익명 함수 표현식
    var anonymousFunc = function() {};
    console.log(anonymous.name); // anonymousFunc

    // 함수 선언문
    function bar() {}
    console.log(bar.name); // bar
    ```

### 18.2.5 __proto__ 접근자 프로퍼티
- 모든 객체는 [[Prototype]] 내부 슬롯을 가짐

### 18.2.6 prototype 프로퍼티
- constructor만이 소유하는 프로퍼티
    ```javascript
    // 함수 객체는 prototype 프로퍼티 소유
    (function () {}).hasOwnProperty('prototype'); // -> true

    // 일반 객체는 prototype 프로퍼티를 소유하지 않음
    ({}).hasOwnProperty('prototype'); // -> false
    ```