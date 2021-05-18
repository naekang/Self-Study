# Chapter19-1 프로토타입
---

- 자바스크립트는 명령형, 함수형, 프로토타입 기반 객체지향 프로그래밍을 지원하는 멀티 패러다임 프로그래밍 언어
- 자바스크립트를 이후는 거의 모든 것이 `객체`

## 19.1 객체지향 프로그래밍
- '이름'과 '주소'의 속성을 갖는 person 객체
    ```javascript
    // 이름과 주소 속성을 갖는 객체
    const person = {
            name: 'Lee',
            address: 'Seoul'
    };

    console.log(person); // {name: "Lee", address: "Seoul"}
    ```

- 원의 상태를 나타내는 데이터
    ```javascript
    const circle = {
        // 반지름
        radius: 5, 

        //원의 지름: 2r
        getDiameter() {
            return 2 * this.radius;
        },

        // 원의 둘레: 2πr
        getPerimeter() {
            return 2 * Math.PI * this.radius;
        },

        // 원의 넓이: πrr
        getArea() {
            return Math.PI * this.radius ** 2;
        },
    };

    console.log(circle);
    // {radius: 5, getDiameter: f, getPerimeter: f, getArea: f}

    console.log(circle.getDiameter()); // 10
    console.log(circle.getPremeter()); // 31.4159...
    console.log(circle.getArea()); // 78.5398...
    ```
> 객체는 상태 데이터와 동작을 하나의 논리적인 단위로 묶은 복합적인 자료구조


## 19.2 상속과 프로토타입
- 코드 재사용을 줄이기 위한 방법
    ```javascript
    // 생성자 함수
    function Circle(radius) {
        this.radius = radius;
        this.getArea = function () {
            return Math.PI * this.radius ** 2;
        };
    }

    // 반지름이 1인 인스턴스 생성
    const circle1 = new Circle(1);
    // 반지름이 2인 인스턴스 생성
    const circle2 = new Circle(2);

    //  Circle 생성자 함수는 인스턴스를 생성할 때마다 동일한 동작을 하는
    // getArea 메서드를 중복 생성하고 모든 인스턴스가 중복 소유
    // getArea 메서드는 하나만 생성하여 모든 인스턴스가 공유하는 것이 바람직
    console.log(circle1.getArea === circle2.getArea); // false
    console.log(circle1.getArea()); // 3.141592...
    console.log(circle2.getArea()); // 12.56637...
    ```

- 이러한 문제를 줄이기 위해 prototype 기반으로 상속 구현
    ```javascript
    // 생성자 함수
    function Circle(radius) {
        this.radius = radius;
    }

    // 모든 인스턴스가 getArea 메서드를 공유할 수 있도록 프로토 타입에 추가
    Circle.prototype.getArea = function () {
        return Math.PI * this.raidus ** 2;
    };

    const circle1 = new Circle(1);
    const circle2 = new Circle(2);

    console.log(circle1.getArea === circle2.getArea); // true
    console.log(circle1.getArea()); // 3.141592...
    console.log(circle2.getArea()); // 12.56637...
    ```

## 19.3 프로토타입 객체
- 객체 간 상속을 구현하기 위해 사용

### 19.3.1 __proto__ 접근자 프로퍼티
- 모든 객체는 `__proto__` 접근자 프로퍼티를 통해 `[[prototype]]` 내부 슬롯에 간접적으로 접근 가능

#### `__proto__`는 접근자 프로퍼티
- getter, setter 함수를 통해 `[[prototype]]` 내부 슬롯 값 취득, 할당
    ```javascript
    const obj = {};
    const parent = { x: 1 };

    // getter 함수인 get __proto__가 호출되어 obj 객체의 프로토타입 취득
    obj.__proto__;

    // setter 함수인 set __proto__가 호출되어 obj 객체의 프로토타입 교체
    obj.__proto__ = parent;

    console.log(obj.x); // 1
    ```

#### `__proto__` 접근자 프로퍼티는 상속을 통해 사용
- 모든 객체는 상속을 통해 `Object.prototype.__proto__` 접근자 프로퍼티 사용 가능

#### `__proto__` 접근자 프로퍼티를 통해 프로토타입에 접근하는 이유
- 상호 참조에 의해 프로토타입 체인이 생성되는 것을 방지하기 위해
- 프로토타입 체인은 단방향 연결 리스트로 구현되어야 함

#### `__proto__` 접근자 프로퍼티를 코드 내에서 직접 사용하는 것은 지양
- 프로토타입의 참조를 취득, 교체하고자 하는 경우 `Object.setPrototypeOf` 메서드 사용 권장

### 19.3.2 함수 객체의 prototype 프로퍼티
- 함수 객체만이 소유하는 prototype 프로퍼티는 생성자 함수가 생성할 인스턴스의 프로토타입을 가리킴
- 모든 객체가 가지고 있는 `__proto__` 접근자 프로퍼티와 함수 객체만이 가지고 있는 prototype 프로퍼티는 결국 동일한 프로퍼티를 가리킴

### 19.3.3 프로토타입의 constructor 프로퍼티와 생성자 함수
```javascript
// 생성자 함수
function Person(name) {
    this.name = name;
}

const me = new Person('Lee');

// me 객체의 생성자 함수는 Person
console.log(me.constructor === Person); // true
```