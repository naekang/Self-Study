# Chapter19-5 프로토타입
---

## 19.14

### 19.14.1 for...in 문
- 객체의 모든 프로퍼티를 순회하면서 열거할 경우

```javascript
for (변수선언문 in 객체) {...}
```

- for ... in 문은 객체의 프로토타입 체인 상에 존재하는 모든 프로토타입의 프로퍼티 중에서 프로퍼티 어트리뷰트 `[[Enumerable]]`의 값이 true인 프로퍼티를 순회하면서 열거함

```javascript
const person = {
    name: 'Lee',
    address: 'Seoul'
    __proto__: { age: 20 }
};

for (const key in person) {
    console.log(key + ':' + person[key]);
}
// name: Lee
// address: Seoul
// age: 20
```

```javascript
const sym = Symbol();
const obj = {
    a: 1,
    [sym]: 10
};

for (const key in obj) {
    console.log(key + ':' + obj[key]);
};
// a: 1
```

- 배열에는 일반적인 for문이나 for ... of 문 또는 Array.prototype.forEach 메서드 사용 권장

### 19.14.2 Object.keys/values/entries
- `Object.prototype.hasOwnProperty` 메서드를 사용하여 객체 자신의 프로퍼티인지 확인하는 추가 처리 필요
- ES8에서 도입된 Object.values 메서드는 객체 자신의 열거 가능한 프로퍼티 값을 배열로 반환

```javascript
console.log(Object.entries(person)); //[["name", "Lee"], ["address", "Seoul"]]

Object.entries(person).forEach(([key, value]) => console.log(key, value));
/*
name Lee
address Seoul
*/
```
