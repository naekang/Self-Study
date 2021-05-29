# Chapter19-2 프로토타입
---

## 19-4 리터럴 표기법에 의해 생성된 객체의 생성자 함수와 프로토타입
```javascript
// obj 객체를 생성한 생성자 함수는 Object
const obj = new Object();
console.log(obj.constructor === Object); // true

// add 함수 객체를 생성한 생성자 함수는 Function
const add = new Function('a', 'b', 'return a + b');
console.log(add.constructor === Function); // true

// 생성자 함수
function Person(name) {
    this.name = name;
}

// me 객체를 생성한 생성자 함수는 Person
const me = new Person('Lee');
console.log(me.constructor === Person); // true
```

- 명시적으로 new 연산자와 함께 생성자 함수를 호출하여 인스턴스를 생성하지 않는 방법
    ```javascript
    // 객체 리터럴
    const obj = {};

    // 함수 리터럴
    const add = function (a, b) { return a + b; };

    // 배열 리터럴
    const arr = [1, 2, 3];

    // 정규 표현식 리터럴
    const regexp = /is/ig;
    ```

- 프로토타입과 생성자 함수는 단독으로 존재할 수 없고 언제나 쌍으로 존재

리터럴 표기법|생성자 함수|프로토타입
--|--|--
객체 리터럴|Object|Object.prototype
함수 리터럴|Function|Function.prototype
배열 리터럴|Array|Array.prototype
정규 표현식 리터럴|RegExp|RegExp.prototype

## 19.5 프로토타입의 생성 시점
- 생성자 함수가 생성되는 시점에 더불어 생성됨

### 19.5.1 사용자 정의 생성자 함수와 프로토타입 생성 시점
- 생성자 함수로서 호출할 수 있는 함수, 즉 constructor는 함수 정의가 평가되어 함수 객체를 생성하는 시점에 프로토타입도 더불어 생성됨
    ```javascript
    // 함수 정의(constructor)가 평가되어 함수 객체를 생성하는 시점에 프로토타입도 더불어 생성
    console.log(Person.prototype); // {constructor: f}

    // 생성자 함수
    function Person(name) {
        this.name = name;
    }
    ```

    ```javascript
    // 화살표 함수는 non-constructor
    const Person = name => {
        this.name = name;
    };

    // non-constructor는 프로토타입이 생성되지 않음
    console.log(Person.prototype); // undefined
    ```

### 19.5.2 빌트인 생성자 함수와 프로토타입 생성 시점
- 객체가 생성되기 이전에 생성자 함수와 프로토타입은 이미 객체화
- 이후 생성자 함수 또는 리터럴 표기법으로 객체를 생성하면 프로토타입은 생성된 객체의 `[[Prototype]]` 내부 슬롯에 할당


## 19.6 객체 생성 방식과 프로토타입의 결정
- 객체 리터럴
- Object 생성자 함수
- 생성자 함수
- Object.create 메서드
- 클래스(ES6)

### 19.6.1 객체 리터럴에 의해 생성된 객체의 프로토타입
- 객체의 프로토타입은 `Object.prototype`
    ```javascript
    const obj = { x: 1 };
    console.log(obj.constructor === Object); // true
    console.log(obj.hasOwnProperty('x')); // true
    ```

### 19.6.2 Object 생성자 함수에 의해 생성된 객체의 프로토타입
- Object 생성자 함수를 호출하면 추상 연산 `OrdinaryObjectCreate` 호출
    ```javascript
    const obj = new Object();
    obj.x = 1;
    console.log(obj.constructor === Object); // true
    console.log(obj.hasOwnProperty('x')); // true
    ```

### 19.6.3 생성자 함수에 의해 생성된 객체의 프로토타입
- 추상 연산 `OrdinaryObjectCreate` 호출
    ```javascript
    function Person(name) {
        this.name = name;
    }

    // 프로토타입 메서드
    Person.prototype.sayHello = function () {
        console.log(`Hi! My name is ${this.name}`);
    };

    const me = new Person('Lee');
    const you = new Person('Kim');

    me.sayHello(); // Hi! My name is Lee
    you.sayHello(); // Hi! My name is Kim
    ```