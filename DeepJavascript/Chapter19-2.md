# Chapter19-2 프로토타입
---

### 19-4 리터럴 표기법에 의해 생성된 객체의 생성자 함수와 프로토타입
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