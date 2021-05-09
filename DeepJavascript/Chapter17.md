# Chapter17 - 생성자 함수에 의한 객체 생성
---

## 17.1 Object 생성자 함수
- new 연산자와 함꼐 Object 생성자 함수를 호출하면 빈 객체를 생성하여 반환
    ```javascript
    // 빈 객체의 생성
    const person = new Object();

    // 프로퍼티 추가
    person.name = 'Lee';
    person.sayHello = function () {
        console.log('Hi! My name is ' + this.name);
    };

    console.log(person); // {name: "Lee", sayHello: f}
    person.sayHello(); // Hi! My name is Lee
    ```

- 자바스크립트는 Object 생성자 함수 외에도 String, Number, Boolean, Function 등 빌트인 생성자 함수 제공


## 17.2 생성자 함수

### 17.2.1 객체 리터럴에 의한 객체 생성 방식의 문제점
- 직관적이고 간편하지만 단 하나의 객체만 생성 가능
- 동일한 프로퍼티를 갖는 객체가 여러개 필요할 경우 반복 작성해야하기 떄문에 비효율적
    ```javascript
    const circle1 = {
        radius: 5,
        getDiameter() {
            return 2 * this.radius;
        }
    };

    console.log(circle1.getDiameter()); // 10

    const circle2 = {
        radius: 10,
        getDiameter() {
            return 2 * this.radius;
        }
    };

    console.log(circle2.getDiameter()); // 20

    // radius 프로퍼티의 값은 객체마다 다를 수 있음
    // getDiameter 메서드는 동일
    ```

### 17.2.2 생성자 함수에 의한 객체 생성 방식의 장점
- 객체 생성 템플릿처럼 사용 가능
    ```javascript
    // 생성자 함수
    function Circle(radius) {
        // 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킴
        this.radius = radius;
        this.getDiameter = function () {
            return 2 * this.radius;
        };
    }

    // 인스턴스의 생성
    const circle1 = new Circle(5); // 반지름이 5인 Circle 객체 생성
    const circle2 = new Circle(10); // 반지름이 10인 Circle 객체 생성

    console.log(circle1.getDiameter()); // 10
    console.log(circle2.getDiameter()); // 20
    ```

- new 연산자와 함께 사용하면 생성자 함수로 동작
- new 연산자 없이 사용하면 일반 함수로 동작

### 17.2.3 생성자 함수의 인스턴스 생성 과정
- 인스턴스 생성(필수) 및 생성된 인스턴스 초기화(옵션)
    ```javascript
    // 생성자 함수
    function Circle(radius) {
        // 인스턴스 초기화
        this.radius = radius;
        this.getDiameter = function () {
            return 2 * this.radius;
        };
    }

    // 인스턴스 생성
    const circle1 = new Circle(5); // 반지름이 5인 Circle 객체 생성
    ```


#### 1. 인스턴스 생성과 this 바인딩
- 암묵적으로 빈 객체 생성 = 생성자 함수가 생성한 인스턴스 = this에 바인딩
    ```javascript
    function Circle(radius) {
        // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩
        console.log(this); // Circle {}

        this.radius = radius;
        this.getDiameter = function () {
            return 2 * this.radius;
        };
    }
    ```

#### 2. 인스턴스 초기화
- this에 바인딩되어 있는 인스턴스에 프로퍼티나 메서드를 추가하고 생성자 함수가 인수로 전달받은 초기값을 인스턴스 프로퍼티에 할당하여 초기화하거나 고정값 할당
    ```javascript
    function Circle(radius) {
        // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩

        // 2. this에 바인딩되어 있는 인스턴스 초기화
        this.radius = radius;
        this.getDiameter = function () {
            return 2 * this.radius;
        };
    }
    ```

#### 3. 인스턴스 반환
- 생성자 함수 내부의 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환
    ```javascript
    function Circle(radius) {
        // 1. 암묵적으로 빈 객체가 생성되고 this에 바인딩

        // 2. this에 바인딩되어 있는 인스턴스 초기화
        this.radius = radius;
        this.getDiameter = function () {
            return 2 * this.radius;
        };

        // 3. 완성된 인스턴스가 바인딩된 this가 암묵적으로 변환
    }

    // 인스턴스 생성. Circle 생성자 함수는 암묵적으로 this를 반환
    const circle = new Circle(1);
    console.log(circle); // Circle {radius: 1, getDiameter: f}
    ```

### 17.2.4 내부 메서드 [[Call]]과 [[Construct]]
- 일반 객체는 호출할 수 없지만 함수는 호출 가능
- 일반 함수 호출: [[Call]] 호출, 생성자 함수 호출: [[Construct]] 호출
    ```javascript
    function foo() {}
    // 일반적인 함수로서 호출: [[Call]] 호출
    foo();

    // 생성자 함수로서 호출: [[Construct]] 호출
    new foo();
    ```


### 17.2.5 constructor와 non-constructor의 구분
- constructor: 함수 선언문, 함수 표현식, 클래스
- non-constructor: 메서드, 화살표 함수

```javascript
// 일반 함수 정의: 함수 선언문, 함수 표현식
function foo() {}
const bar = function () {};
// 프로퍼티 x의 값으로 할당된 것은 일반 함수로 정의된 함수
const baz = {
    x: function () {}
};

// 일반 함수로 정의된 함수만이 constructor
new foo(); // foo {}
new bar(); // bar {}
new bar.x(); // x{}

// 화살표 함수 정의
const arrow = () => {};

new arrow(); // TypeError: Arrow is not a constructor

// 메서드 정의: ES6의 메서드 축약 표현만 메서드로 인정
const obj = {
    x() {}
};

new obj.x(); // TypeError: obj.x is not a constructor
```

```javascript
function foo() {}

// 일반 함수로서 호출
// [[call]] 호출. 모든 함수 객체는 [[call]]이 구현되어 있음
foo();

// 생성자 함수로서 호출
// [[Construct]] 호출. 이때 [[Construct]]를 갖지 않으면 에러 발생
new foo();
```


### 17.2.6 new 연산자
- new 연산자와 함께 함수를 호출하면 생성자 함수로 동작. 즉, [[Construct]] 호출
    ```javascript
    // 생성자 함수로서 정의하지 않은 일반 함수
    function add(x, y) {
        return x + y;
    }

    // 생성자 함수로서 정의하지 않은 일반 함수를 new 연산자와 함께 호출
    let inst = new add();

    // 함수가 객체를 반환하지 않았으므로 반환문이 무시됨. 따라서, 빈 객체가 생성되어 반환
    console.log(inst); // {}

    // 객체를 반환하는 일반 함수
    function createUser(name, role) {
        return { name, role }; 
    }

    // 일반 함수를 new 연산자와 함께 호출
    inst = new createUser('Lee', 'admin');
    // 함수가 생성한 객체를 반환
    console.log(inst); // {name: "Lee", role: "admin"}
    ```

- new 연산자가 없이 함수를 호출하면 일반 함수로 호출. 즉, [[call]] 호출
    ```javascript
    // 생성자 함수
    function Circle(radius) {
        this.radius = radius;
        this.getDiameter = function () {
            return 2 * this.radius;
        };
    }

    // new 연산자 없이 생성자 함수를 호출하면 일반 함수로서 호출
    const circle = Circle(5);
    console.log(circle); // undefined
    
    // 일반 함수 내부의 this는 전역 객체 window를 가리킴
    console.log(radius); // 5
    console.log(getDiameter()); // 10

    circle.getDiameter();
    // TypeError: Cannot read property 'getDiameter' of undefined
    ```


### 17.2.7 new.target
- this와 유사하게 constructor인 모든 함수 내부에서 암묵적인 지역변수와 함께 생성
- new 연산자와 함께 생성자 함수로서 호출되면 함수 내부의 new.target은 함수 자신을 가리킴. new 연산자 없이 일반 함수로서 호출된 함수 내부의 new.target은 undefined

- Object와 Function 생성자 함수는 new 연산자 없어도 동일하게 동작
- String, Number, Boolean 생성자 함수는 new가 있으면 객체 생성 반환 없으면 그대로 반환
