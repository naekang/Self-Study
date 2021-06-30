# Chapter19-4 프로토타입
---

## 19.11 직접 상속

### 19.11.1 Object.create에 의한 직접 상속
- Object.create 메서드는 명시적으로 프로토타입을 지정하여 새로운 객체 생성

```javascript
/**
 * 지정된 프로토타입 및 프로퍼티를 갖는 새로운 객체를 생성하여 반환
 * @param {Object} prototype - 생성할 객체의 프로토타입으로 지정할 객체
 * @param {Object} {propertiesObject} - 생성할 객체의 프로퍼티를 갖는 객체
 * @returns {Object} 지정된 프로토타입 및 프로퍼티를 갖는 새로운 객체
 */
Object.create(prototype[, propertiesObject])
```

- 장점
  - new 연산자 없이도 객체 생성 가능
  - 프로토타입을 지정하면서 객체 생성 가능
  - 객체 리터럴에 의해 생성된 객체도 상속 가능

```javascript
// 프로토타입이 null인 객체를 생성
const obj = Object.create(null);
obj.a = 1;

// console.log(obj.hasOwnProperty('a'));
// TypeError: obj.hasOwnProperty is not a function

// Object.prototype의 빌트인 메서드는 객체로 직접 호출하지 않는다
console.log(Object.prototype.hasOwnProperty.call(obj, 'a')); // true
```

### 19.11.2 객체 리터럴 내부에서 `__proto__`에 의한 직접 상속
- ES6에서는 객체 리터럴 내부에서 `__proto__`접근자 프로퍼티를 사용하여 직접 상속 구현 가능
```javascript
const myPhoto = { x: 10 };

// 객체 리터럴에 의해 객체를 생성하면서 프로토타입을 지정하여 직접 상속받을 수 있음
const obj = {
    y: 20,
    // 객체를 직접 상속받음
    // obj -> myPhoto -> Object.prototype -> null
    __proto__: myPhoto
};

console.log(obj.x, obj.y); // 10 20
console.log(Object.getPrototypeOf(obj) === myPhoto); // true
```

## 19.12 정적 프로퍼티 / 메서드
```javascript
// 생성자 함수
function Person(name) {
    this.name = name;
}

// 프로토타입 메서드
Person.prototype.sayHello = function () {
    console.log(`Hi! My name is ${this.name}`);
};

// 정적 프로퍼티
Person.staticProp = 'static prop';

// 정적 메서드
Person.staticMethod = function () {
    console.log('staticMethod');
};

const me = new Person('Lee');

// 생성자 함수에 추가한 정적 프로퍼티/메서드는 생성자 함수로 참조/호출한다.
Person.staticMethod(); // staticMethod

me.staticMethod(); // TypeError: me.staticMethod is not a function
```

## 19.13 프로퍼티 존재 확인

### 19.13.1 in 연산자
```javascript
/**
 * key: 프로퍼티 키를 나타내는 문자열
 * object: 객체로 평가되는 표현식
 */
key in object
```
- in 연산자 대신 ES6에서 도입된 Reflect.has 메서드 사용 가능

### 19.13.2 Object.prototype.hasOwnProperty 메서드
- `Object.prototype.hasOwnProperty` 메서드를 사용해도 객체에 특정 프로퍼티가 존재하는지 확인 가능