# Chapter19-3 프로토타입
---

## 19.7 프로토타입 체인
```javascript
function Person(name) {
    this.name = name;
}

// 프로토타입 메서드
Person.prototype.sayHello = function() {
    console.log(`Hi! My name is ${this.name}`);
};

const me = new Person('Lee');

// hasOwnProperty는 Object.prototype의 메서드
console.log(me.hasOwnProperty('name')); // true
```

- 자바스크립트는 객체의 프로퍼티에 접근하려고 할 떄 해당 객체에 접근하려는 프로퍼티가 없다면 `[[Prototype]]` 내부 슬롯의 참조를 따라 자신의 부모 역할을 하는 프로토타입의 프로퍼티를 순차적으로 검색한다. -> 프로토타입 체인
- 프로토타입 체인은 상속과 프로퍼티 검색을 위한 메커니즘

## 19.8 오버라이딩과 프로퍼티 섀도잉
- `오버라이딩`: 상위 클래스가 가지고 있는 메서드를 하위 클래스가 재정의하여 사용하는 방식
- `오버로딩`: 함수의 이름은 동일하지만 매개변수의 타입 또는 개수가 다른 메서드를 구현하고 매개변수에 의해 메서드를 구별하여 호출하는 방식

```javascript
const Person = (function () {
    // 생성자 함수
    function Person(name) {
        this.name = name;
    }

    // 프로토타입 메서드
    Person.prototype.sayHello = function () {
        console.log(`Hi! My name is ${this.name}`);
    };

    // 생성자 함수를 반환
    return Person;
}());

const me = new Person('Lee');

// 인스턴스 메서드
me.sayHello = function () {
    consol.log(`Hey! My name is ${this.name}`);
};

// 인스턴스 메서드 호출
me.sayHello(); // Hey! My name is Lee
```

## 19.9 프로토타입 교체

### 19.9.1 생성자 함수에 의한 프로토타입의 교체
```javascript
const Person = (function () {
    function Person(name) {
        this.name = name;
    }

    // 생성자 함수의 prototype 프로퍼티를 통해 프로토타입을 교체
    Person.prototype = {
        // constructor 프토퍼티와 생성자 함수 간의 연결을 설정
        constructor: Person,
        sayHello() {
            console.log(`Hi! My name is ${this.name}`);
        }
    };

    return Person;
}());

const me = new Person('Lee');

// constructor 프로퍼티가 생성자 함수를 가리킴
console.log(me.constructor === Person); // true
console.log(me.constructor === Object); // false
```

### 19.9.2 인스턴스에 의한 프로토타입의 교체
- 프로토타입은 생성자 함수의 prototype 프로퍼티 뿐 아니라 인스턴스의 `__proto__` 접근자 프로퍼티를 통해 접근할 수 있기 떄문에 프로토타입 교체 가능


## 19.10 instanceof 연산자
```javascript
객체 instanceof 생성자 함수
```

- 생성자 함수의 prototype에 바인딩된 객체가 프로토타입 체인 상에 존재하는지 확인

```javascript
const Person = (function () {
    function Person(name) {
        this.name = name;
    }

    // 생성자 함수의 prototype 프로퍼티를 통해 프로토타입을 교체
    Person.prototype = {
        sayHello() {
            console.log(`Hi! My name is ${this.name}`);
        }
    };

    return Person;
}());

const me = new Person('Lee');

// constructor 프로퍼티와 생성자 함수 간의 연결이 파괴되어도 instanceof는 아무런 영향을 받지 않음
console.log(me.constructor === Person); // false

// Person.prototype이 me 객체의 프로토타입 체인 상에 존재하므로 true
console.log(me instanceof Person); // true
// Object.prototype이 me 객체의 프로토타입 체인 상에 존재하므로 true
console.log(me instanceof Object); // true
```