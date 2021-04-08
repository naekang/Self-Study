# Chpater16 - 프로퍼티 어트리뷰트
---

## 16.1 내부 슬롯과 내부 메서드
- 자바스크립트 엔진의 구현 알고리즘을 설명하기 위해 사용하는 의사 프로퍼티와 의사 메서드
- 자바스크립트 엔진의 내부 로직이므로 직접적으로 접근이나 호출 방법을 제공하지 않음


## 16.2 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체
- 프로퍼티 생성 시 상태를 나타내는 프로퍼티 어트리뷰트를 기본값으로 자동 정의
- 직접 접근은 불가능하지만 Object.getOwnPropertyDescriptor 메서드를 이용해 간접적으로 확인가능
    ```javascript
    const person = {
        name: 'Lee'
    };

    // 프로퍼티 동적 생성
    person.age = 20;

    // 모든 프로퍼티의 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체 반환
    console.log(Object.getOwnPropertyDescriptor(person));
    /*
    {
        name: {value: "Lee", writable: true, enumerable: true, configurable: true},
        age: {value: 20, writable: true, enumerable: true, configurable: true}
    }
    */
    ```


## 16.3 데이터 프로퍼티와 접근자 프로퍼티
- 데이터 프로퍼티(Data Property): 키와 값으로 구성
- 접근자 프로퍼티(Accessor Property): 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 접근자 함수로 구성

### 16.3.1 데이터 프로퍼티
1. [[value]] / value
    - 프로퍼티 값에 접근하면 반환되는 값
2. [[Enumerable]] / enumerable
3. [[Configuration]] / configuration

```javascript
const person = {
    // 데이터 프로퍼티
    firstName: 'Ungmo',
    lastName: 'Lee',

    // fullName은 접근자 함수로 구성된 접근자 프로퍼티
    // getter 함수
    get fullName() {
        return `${this.firstName} ${this.lastName}`;
    },
    // setter 함수
    set fullName(name) {
        // 배열 디스트럭처링 할당
        [this.firstName, this.lastName] = name.split(' ');
    }
};

// 데이터 프로퍼티를 통함 프로퍼티 값 참조
console.log(person.firstName + ' ' + person.lastName); // Ungmo Lee

// 접근자 프로퍼티를 통한 프로퍼티 값 저장
// 접근자 프로퍼티 fullName에 값을 저장하면 setter 함수 호출
person.fullName = 'Heegun Lee';
console.log(person); // {firstName: "Heegun", lastName: "Lee"}

// 접근자 프로퍼티를 통한 프로퍼티 값 참조
console.log(person.fullName); // Heegun Lee

// firstName은 데이터 프로퍼티
// 프로퍼티 어트리뷰트를 갖음
let descriptor = Object.getOwnPropertyDescriptor(person, 'firstNmae');
console.log(descriptor);
// {value: "Heegun", writable: true, enumerable: true, configuration: true}

// fullName은 접근자 프로퍼티
descriptor = Object.getOwnPropertyDescriptor(person, 'fullName');
console.log(decriptor);
// {get: f, set: f, enumerable: true, configuration: true}
```

## 16.4 프로퍼티 정의
- Object.defineProperties 메서드를 사용하여 여러 개의 프로퍼티 정의 가능

## 16.5 객체 변경 방지

구분|메서드|프로퍼티 추가|프로퍼티 삭제|프로퍼티 값 읽기|프로퍼티 값 쓰기|프로퍼티 어트리뷰트 재정의
--|--|--|--|--|--|--
객체확장금지|Object.preventExtensions|X|O|O|O|O
객체 밀봉|Object.seal|X|X|O|O|X
객체 동결|Object.freeze|X|X|O|X|X