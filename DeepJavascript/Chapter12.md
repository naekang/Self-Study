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

### 12.4.3 함수 생성 시점과 함수 호이스팅
```javascript
// 함수 참조
console.dir(add); // f add(x, y)
console.dir(sub); // undefined

// 함수 호출
console.log(add(2, 5)); // 7
console.log(sub(2, 5)); // TypeError: sub is not a function

// 함수 선언문
function add(x, y) {
    return x + y;
}

// 함수 표현식
var sub = function (x, y) {
    return x - y;
};
```
- 함수 선언문으로 정의한 함수는 함수 선언문 이전에 호출할 수 있으나 함수 표현식으로 정의한 함수는 함수 표현식 이전에 호출할 수 없음
- 함수 선언문으로 정의한 함수와 함수 표현식으로 정의한 함수 생성 시점이 다르기 때문

- 함수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 함수 호이스팅(function hoisting)이라함

- 변수 할당문의 값은 할당문이 실행되는 시점, 즉 런타임에 평가되므로 함수 표현식의 함수 리터럴도 할당문이 실행되는 시점에 평가되어 함수 객체가 됨
> 함수 표현식으로 함수를 정의하면 함수 호이스팅이 발생하는 것이 아닌 변수 호이스팅 발생

### 12.4.4 Function 생성자 함수
- 생성자 함수 : 객체를 생성하는 함수
```javascript
var add1 = (function () {
    var a = 10;
    return function (x, y) {
        return x + y + a;
    };
}());

console.log(add1(1, 2)); // 13

var add2 = (function () {
    var a = 10;
    return new Function('x', 'y', 'return x + y + a;');
}());

console.log(add2(1, 2)); // ReferenceError: a is not defined
```

### 12.4.5 화살표 함수
- function 키워드 대신 화살표(=>)를 사용해 간략하게 선언
    ```javascript
    // 화살표 함수
    const add = (x ,y) => x + y;
    console.log(add(3, 5)) // 8
    ```

## 12.5 함수 호출

### 12.5.1 매개변수와 인수
```javascript
// 함수 선언문
function add(x, y) {
    return x + y;
}

// 함수호출
// 인수 1과 2가 매개변수 x와 y에 순서대로 할당되고 함수 몸체의 문들이 실행
var result = add(1, 2);
```
- 매개변수의 스코프(유효 범위)는 함수 내부
- 인수가 부족해서 할당되지 않은 매개변수 값은 undefined
- 매개 변수가 인수보다 많은 경우 초과된 인수는 무시

### 12.5.2 인수 확인
- 자바스크립트 함수는 매개변수와 인수의 개수가 일치하는지 확인하지 않음
- 자바스크립트는 동적 타입 언어로 매개변수 타입을 사전에 지정할 수 없음
- 따라서 자바스크립트의 경우 함수를 정의할 때 적절한 인수가 전달되었는지 확인해야함
    ```javascript
    function add(x, y) {
        if (typeof x !== 'number' || typeof y !== 'number') {
            throw new TypeError('인수는 모두 숫자 값 이어야 합니다.');
        }
        return x + y;
    }

    console.log(add(2)); // TypeError: 인수는 모두 숫자 값 이어야 합니다.
    console.log(add('a','b')); // TypeError: 인수는 모두 숫자 값 이어야 합니다.
    ```

- 인수가 전달되지 않은 경우 단축 평가를 사용하여 매개변수에 기본값을 할당하는 방법도 있음
    ```javascript
    function add(a = 0, b = 0, c = 0) {
        return a + b + c;
    }

    console.log(add(1, 2, 3)); // 6
    console.log(add(1, 2)); // 3
    console.log(add(1)); // 1
    console.log(add()); // 0
    ```

### 12.5.3 매개변수의 최대 개수
- 이상적인 함수는 한 가지 일만 해야하며 가급적 작게 만들어야 함 (3개 이상 넘지 않는 것을 권장)

### 12.5.4 반환문
- 반환문의 역할
    1. 함수의 실행을 중단하고 몸체를 빠져나감
    2. return 키워드 뒤에 오는 표현식을 평가해 반환


## 12.6 참조에 의한 전달과 외부 상태의 변경
```javascript
// 매개변수 primitive는 원시 값을 전달받고, 매개변수 obj는 객체를 전달받음
function changeVal(primitive, obj) {
    primitive += 100;
    obj.name = 'Kim';
}

// 외부 상태
var num = 100;
var person = { name: 'Lee' };

console.log(num); // 100
console.log(person) // {name: "Lee"}

// 원시 값은 값 자체가 복사되어 전달
// 객체는 참조 값이 복사되어 전달
changeVal(num, person);

// 원시값은 훼손되지 않음
console.log(num); // 100

// 객체는 원본이 훼손
console.log(person); // {name: "Kim"}
```

## 12.7 다양한 함수의 형태

### 12.7.1 즉시 실행 함수(Immediately Invoked Function Expression)
- 정의와 동시에 실행되는 함수
- 단 한번만 호출되며 다시 호출할 수 없음
    ```javascript
    // 기명 즉시 실행 함수
    (function foo() {
        var a = 3;
        var b = 5;
        return a * b;
    }());

    foo(); // ReferenceError: foo is not defined
    ```
- 즉시 실행 함수는 반드시 그룹 연산자 (...)로 감싸야 함
- 즉시 실행 함수도 일반 함수처럼 값을 반환할 수 있고 인수 전달 가능
    ```javascript
    // 즉시 실행 함수도 일반 함수처럼 값을 반환할 수 있음
    var res = (function () {
        var a = 3;
        var b = 5;
        return a * b;
    }());
    console.log(res); // 15

    // 즉시 실행 함수에도 일반 함수처럼 인수 전달 가능
    res = (function (a, b) {
        return a * b;
    }(3, 5));
    console.log(res); // 15
    ```

### 12.7.2 재귀 함수
- 함수가 자기 자신을 호출하는 것을 재귀 호출이라 함
- 10부터 0까지 출력하는 함수 -> 반복문 없이 구현 가능
    ```javascript
    function countdown(n) {
        if (n < 0) return;
        console.log(n);
        countdown(n - 1); // 재귀 호출
    }
    countdown(10);
    ```
- 팩토리얼의 구현
    ```javascript
    function factorial(n) {
        // n이 1 이하일 떄 탈출
        if (n <= 1) return 1;
        // 재귀 호출
        return n * factorial(n - 1);
    }

    console.log(factorial(0)); // 1
    console.log(factorial(5)); // 5! = 5 * 4 * 3 * 2 * 1 = 120
    ```
- 재귀 함수는 자신을 무한 재귀 호출하기 때문에 반드시 탈출 조건을 만들어야 한다.

### 12.7.3 중첩 함수
- 함수 내부에 정의된 함수를 중첩 함수(nested function) 또는 내부 함수(inner function)이라함
- 일반적으로 helper function의 역할 수행
    ```javascript
    function outer() {
        var x = 1;
        // 중첩 함수
        function inner() {
            var y = 2;
            console.log(x + y); // 3
        }
        inner();
    }
    outer();
    ```

### 12.7.4 콜백 함수
- 반복적인 일은 같으나 함수의 기능이 다를 경우 매번 새롭게 정의해야함
- 이는 함수의 합성으로 해결 가능
    ```javascript
    // 외부에서 전달받은 f를 n만큼 반복 호출
    function repeat(n, f) {
        for (var i = 0; i < n; i++) {
            f(i); // i를 전달하면서 f를 호출
        }
    }

    var logAll = function (i) {
        console.log(i);
    }

    // 반복 호출할 함수를 인수로 전달
    repeat(5, logAll); // 0 1 2 3 4

    var logOdds = function (i) {
        if (i % 2)
            console.log(i);
    };

    // 반복 호출할 함수를 인수로 전달
    repeat(5, logOdds); // 1 3
    ```
- 함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수 => 콜백 함수
- 매개 변수를 통해 함수의 외부에서 콜백 함수를 전달받은 함수 => 고차 함수
- 고차 함수는 콜백 함수를 자신의 일부분으로 합성

### 12.7.5 순수 함수와 비순수 함수
- 순수 함수 : 어떤 외부 상태에 의존하지도 않고 변경하지도 않는 함수 (반대 : 비순수 함수)
- 함수형 프로그래밍은 결국 순수 함수를 통해 프로그램의 안정성을 높이려는 노력의 일환