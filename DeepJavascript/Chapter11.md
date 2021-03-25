# Chapter11 - 원시 값과 객체의 비교
---
- 원시 타입의 값, 즉 원시 값은 변경 불가능한 값 / 객체 타입의 값, 즉 객체는 변경 가능한 값
- 원시 값을 변수에 할당하면 변수에는 실제 값이 저장 / 객체를 변수에 할당하면 변수에는 참조 값이 저장
- 원시 값을 갖는 변수를 다른 변수에 할당하면 원시 값이 복사되어 전달 = 값에 의한 전달
- 객체를 가리키는 변수를 다른 변수에 할당하면 원본의 참조값이 복사되어 전달 = 참조에 의한 전달


## 11.1 원시 값

### 11.1.1 변경 불가능한 값
- 원시 타입의 값은 변경 불가능
- 원시 값 자체를 변경할 수 없다는 것이지 변수 값을 변경할 수 없다는 것은 아님
```javascript
// const 키워드를 사용해 선언한 변수는 재할당이 금지
const o = {};

// const 키워드를 사용해 선언한 변수에 할당한 원시 값(상수)은 변경 불가능
// 하지만 const 키워드를 사용해 선언한 변수에 할당한 객체는 변경 가능
o.a = 1;
console.log(o); // {a: 1}
```
- 원시 값을 재할당하면 값을 변경하는 것이 아니라 새로운 메모리 공간을 확보하고 재할당한 원시 값 저장 -> 불변성(immutability)

### 11.12 문자열과 불변성
- 원시 값을 저장하려면 먼저 확보해야 하는 메모리 공간의 크기를 결정해야함
- 문자열은 몇 개의 문자로 이루어졌느냐에 따라 필요한 메모리 공간의 크기 결정

```javascript
var str = 'Hello';
str = 'world';
```
- 첫 번째 문이 실행되면 문자열 'Hello'가 생성되고 식별자 str은 'Hello'가 저장된 첫 번째 메모리 셀 주소를 가리킴
- 두 번째 문이 실행되면 새로운 문자열 'world'를 메모리에 생성하고 식별자는 이것을 가리킴

- `유사 배열 객체(array-like object)`
    - 마치 배열처럼 인덱스로 프로퍼티 값에 접근할 수 있고 length 프로퍼티를 갖는 객체
        ```javascript
        var str = 'string';

        // 문자열은 유사 배열이므로 인덱스를 이용해 각 문자에 접근할 수 있음
        console.log(str[0]); // s

        // 원시 값인 문자열이 객체처럼 동작
        console.log(str.length); // 6
        console.log(str.toUpperCase()); // STRING
        ```

### 11.1.3 값에 의한 전달
```javascript
var score = 80;

// copy 변수에는 score 변수의 값 80이 복사되어 할당
var copy = score;

console.log(score, copy); // 80 80
console.log(score === copy); // true

// score 변수와 copy 변수의 값은 다른 메모리 공간에 저장된 별개의 값
// 따라서 score 변수의 값을 변경해도 copy 변수의 값에는 어떠한 영향도 주지 않음
score = 100;

console.log(score, copy); // 100 80
```
- `값에 의한 전달`도 사실은 값을 전달하는 것이 아니라 메모리 주소를 전달한다. 단, 전달된 메모리 주소를 통해 메모리 공간에 접근하면 값을 참조할 수 있다.

## 11.2 객체
- 객체는 프로퍼티의 개수가 정해져 있지 않고 동적으로 추가, 삭제가 가능하기 때문에 원시 값처럼 메모리 공간의 크기를 사전에 정해둘 수 없음
- 자바스크립트 객체의 관리 방식
    - 프로퍼티 키를 인덱스로 사용하는 해시 테이블
    - 클래스 없이 객체를 생성할 수 있으며 동적으로 프로퍼티와 메서드의 추가가 가능함
    - 사용은 편리하나 성능 면에서는 클래스 기반 언어의 객체보다 생성과 프로퍼티 접근에 비용이 더 많이 드는 비효율적인 방식임
    - 따라서, V8자바스크립트 엔진은 동적 탐색 대신 히든 클래스 방식 ㅏㅅ용


### 11.2.1 변경 가능한 값
- 객체 타입의 값, 즉 객체는 변경 가능한 값
- 객체를 할당한 변수가 기억하는 메모리 주소를 통해 메모리 공간에 접근하면 참조 값에 접근 가능
- 재할당 없이 프로퍼티를 동적으로 추가할 수 있고 프로퍼티 값 갱신도 가능하며 프로퍼티 자체를 삭제할 수 있다.
    ```javascript
    var person = {
        name: 'Lee'
    };

    // 프로퍼티 값 갱신
    person.name = 'Kim';

    // 프로퍼티 동적 생성
    person.address = 'Seoul';

    console.log(person); // {name: "Kim", address: "Seoul"}
    ```

- 얕은 복사 vs 깊은 복사
    - 객체를 프로퍼티 값으로 갖는 객체의 경우 얕은 복사는 한 단계까지만 복사하는 것을 말하고 깊은 복사는 객체에 중첩되어 있는 객체까지 모두 복사하는 것
    ```javascript
    const o = { x: { y: 1 } };

    // 얕은 복사
    const c1 = { ...o };
    console.log(c1 === o); // false
    console.log(c1.x === o.x); // true

    // lodash의 cloneDeeop을 사용한 깊은 복사
    // "npm install lodash"로 lodash를 설치한 후, Node.js 환경에서 실행
    const _ = require('lodash');
    // 깊은 복사
    const c2 = _.cloneDeep(o);
    console.log(c2 == o); // false
    console.log(c2.x === o.x); // false
    ```

### 11.2.2 참조에 의한 전달
```javascript
var person = {
    name: 'Lee'
};

// 참조 값을 복사(얕은 복사). copy와 person은 동일한 참조 값을 갖는다.
var copy = person;

// copy와 person은 동일한 객체를 참조
console.log(copy === person); // true

// copy를 통해 객체 변경
copy.name = 'Kim';

// person을 통해 객체 변경
person.address = 'Seoul';
// copy와 person은 동일한 객체를 가리킴
// 따라서 어느 한쪽에서 객체를 변경하면 서로 영향을 주고받음
console.log(person); // {name: "Kim", address: "Seoul"}
console.log(copy); // {name: "Kim", address: "Seoul"}
```
- `값에 의한 전달`과 `참조에 의한 전달`은 식별자가 기억하는 메모리 공간에 저장되어 있는 값을 복사해서 전달한다는 면에 동일함