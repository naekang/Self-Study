# Chapter10 - 객체 리터럴
---

## 10.1 객체란?
- 원시 타입의 값, 즉 원시 값은 변경 불가능한 값이지만 객체 타입의 값, 즉 객체는 변경 가능한 값임
- 객체는 0개 이상의 프로퍼티로 구성된 집합이며 프로퍼티는 키(key)와 값(value)으로 구성
    ```javascript
    var person = {
        name: 'Lee', // 프로퍼티
        age: 20 // 프로퍼티 키: age, 프로퍼티 값: 20
    }
    ```
- 프로퍼티 값이 함수일 경우 일반 함수와 구분하기 위해 메서드(method)라함
    ```javascript
    var counter = {
        num: 0, // 프로퍼티
        // 메서드
        increase: function () {
            this.num++;
        }
    }
    ```

- 객체와 함수는 밀접한 관계를 가짐

## 10.2 객체 리터럴에 의한 객체 생성
- C++이나 Java 같은 클래스 기반 객체지향언어는 클래스를 사전에 정의하고 필요한 시점에 new 연산자와 함께 생성자(constructor)를 호출하여 인스턴스 생성
- 인스턴스(instance): 클래스에 의해 생성되어 메모리에 저장된 실체
- 자바스크립트는 `프로토타입 기반 객체지향 언어`로 다양한 객체 생성 방법 지원
    1. 객체 리터럴 - 가장 간단한 방법
    2. Object 생성자 함수
    3. 생성자 함수
    4. Object.create 메서드
    5. 클래스(ES6)

- 객체 리터럴은 중괄호 내에 0개 이상의 프로퍼티 정의, 정의하지 않으면 빈 객체 생성
    ```javascript
    var person = {
        name: 'Lee',
        sayHello: function () {
            console.log(`Hello! My name is ${this.name}.`);
        }
    };

    console.log(typeof person); // object
    console.log(person); // {name: "Lee", sayHello: f}
    ```

## 10.3 프로퍼티
- 프로퍼티를 나열할 때는 쉼표(,)로 구분
- 프로퍼티 키: 빈 문자열을 포함하는 모든 문자열 또는 심벌 값
- 프로퍼티 값: 자바스크립트에서 사용할 수 있는 모든 값
- 식별자 네이밍을 준수하는 경우는 따옴표 생략이 가능하지만 아닌 경우는 따옴표를 사용해야만 한다.
- 프로퍼티 키에 문자열이나 심벌 이외의 값을 사용하면 암묵적인 타입 변환을 통해 문자열이 됨
- 중복 선언 시 덮어쓰기가 됨

## 10.4 메서드
- 프로퍼티 값이 함수일 경우 일반 함수와 구분하기 위해 메서드(method)라고 부름
    ```javascript
    var circle = {
        radius: 5, // 프로퍼티

        // 원의 지름
        getDiameter: function () {
            return 2 * this.radius; // this는 circle을 가리킴
        }
    }
    ```

## 10.5 프로퍼티 접근
- 마침표 프로퍼티 접근 연산자(.)를 사용하는 마침표 표기법(dot notation)
- 대괄호 프로퍼티 접근 연산자([ ... ])를 사용하는 대괄호 표기법(bracket notation)
    ```javascript
    var person = {
        name: 'Lee';
    };

    console.log(person.name); // Lee
    console.log(person['name']); // Lee
    ```

```javascript
var person = {
    'last-name': 'Lee',
    1: 10
};

person.'last-name';
person.last-name; // 브라우저 환경: NaN, Node.js 환경: ReferenceError
person.[last-name]; // ReferenceError
person.['last-name']; // Lee

person.1; // SyntaxError
person.'1'; // SyntaxError
person[1]; // 10 : person[1] -> person['1']
person['1']; // 10
```
- 브라우저 환경과 node.js 환경에서의 결과가 다른 이유
    - 자바스크립트 엔진은 먼저 person.last를 평가되므로 undefined - name과 같음
    - Node.js 환경에서는 name이라는 식별자 선언이 없기때문에 참조에러 발생

## 10.6 프로퍼티 값 갱신
```javascript
var person = {
    name: 'Lee';
};

// person 객체에 name 프로퍼티가 존재하므로 값이 갱신됨
person.name = 'Kim';

console.log(person); // {name : "Kim"}
```

## 10.7 프로퍼티 동적 생성
```javascript
var person = {
    name: 'Lee'
};

person.age = 20;

console.log(person); // {name : "Lee", age : 20}
```

## 10.8 프로퍼티 삭제
- delete 연산자를 이용하여 삭제
```javascript
var person = {
    name: 'Lee'
};

// 프로퍼티 동적 생성
person.age = 20;

delete person.age;

// person객체에 address 프로퍼티가 없지만 에러 발생하지 않음
delete person.address;

console.log(person); // {name: "Lee"}
```

## 10.9 ES6에서 추가된 객체 리터럴의 확장 기능

### 10.9.1 프로퍼티 축약 표현
```javascript
// ES5
var x = 1, y = 2;

var obj = {
    x: x,
    y: y
};

console.log(obj); // {x: 1, y: 2}
```
```javascript
// ES6
let x = 1, y = 2;

// 프로퍼티 축약 표현
const obj = { x, y };

console.log(obj); // {x: 1, y: 2}
```

### 10.9.2 계산된 프로퍼티 이름
```javascript
// ES5
var prefix = 'prop';
var i = 0;

var obj = {};

obj[prefix + '-' + ++i] = i;
obj[prefix + '-' + ++i] = i;
obj[prefix + '-' + ++i] = i;

console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}
```
```javascript
// ES6
const prefix = 'prop';
let i = 0;

// 객체 리터럴 내부에서 계산된 프로퍼티 이름으로 프로퍼티 키를 동적 생성
const obj = {
    [`${prefix}-${++i}`]: i,
    [`${prefix}-${++i}`]: i,
    [`${prefix}-${++i}`]: i
};

console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}
```

### 10.9.3 메서드 축약 표현
```javascript
// ES5
var obj = {
    name: 'Lee',
    sayHi: function() {
        console.log('Hi! ' + this.name);
    }
};

obj.sayHi(); // Hi! Lee
```
```javascript
// ES6
const obj = {
    name: 'Lee',
    // 메서드 축약 표현
    sayHi() {
        console.log('Hi! ' + this.name);
    }
};

obj.sayHi(); // Hi! Lee
```