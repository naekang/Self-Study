# Chapter14 - 전역 변수의 문제점
---

## 14.1 변수의 생명 주기

### 14.1.1 지역변수의 생명 주기
- 지역 변수의 생명 주기는 함수의 생명 주기와 일치
    ```javascript
    var x = "global";

    function foo() {
        console.log(x); // undefined
        var x = "local";
    }

    foo();
    console.log(x); // global
    ```
- 호이스팅은 스코프 단위로 동작

### 14.1.2 전역 변수의 생명 주기
- 전역 코드에는 반환문을 사용할 수 없으므로 마지막 문이 실행되어 더 이상 실행할 문이 없을 때 종료
- var 키워드로 선언한 전역 변수의 생명 주기는 전역 객체의 생명 주기와 일치


## 14.2 전역 변수의 문제점
1. 암묵적 결합
2. 긴 생명 주기
   - 메모리 리소스 오래 소비
3. 스코프 체인 상에서 종점에 존재
   - 전역변수의 검색 속도가 가장 느림
4. 네임스페이스 오염
   - 다른 파일 내에서 동일한 이름으로 명명된 전역변수나 전역 함수가 같은 스코프 내에 존재할 경우 예상치 못한 결과를 가져올 수 있음

## 14.3 전역 변수의 사용을 억제하는 방법
- 반드시 사용해야 할 이유가 없다면 지역 변수를 사용해야함

### 14.3.1 즉시 실행 함수
- 모든 코드를 즉시 실행 함수로 감싸면 모든 변수는 즉시 실행 함수의 지역 변수가 됨
    ```javascript
    (function () {
        var foo = 10; // 즉시 실행 함수의 지역 변수
        // ...
    }());

    console.log(foo); // ReferenceError: foo is not defined
    ```

### 14.3.2 네임스페이스 객체
- 전역에 네임스페이스 역할을 담당할 객체를 생성하고 전역 변수처럼 사용하고 싶은 변수를 프로퍼티로 추가하는 방법
    ```javascript
    var MYAPP = {}; // 전역 네임스페이스 객체

    MYAPP.person = {
        name: "Lee",
        address: "Seoul"
    };

    console.log(MYAPP.person.name); // Lee
    ```

### 14.3.3 모듈 패턴
```javascript
var Counter = (function () {
    // private 변수
    var num = 0;

    // 외부로 공개할 데이터나 메서드를 프로퍼티로 추가한 객체를 반환
    return {
        increase() {
            return ++num;
        },
        decrease() {
            return --num;
        }
    };
}());

// private 변수는 외부로 노출되지 않음
console.log(Counter.num); // undefined

console.log(Counter.increase()); // 1
console.log(Counter.increase()); // 2
console.log(Counter.decrease()); // 1
console.log(Counter.decrease()); // 0
```

### 14.3.4 ES6 모듈
- ES6 모듈 사용 시 전역 변수 사용 불가능
- 파일 자체의 독자적인 모듈 스코프 제공
    ```javascript
    <script type="module" src="lib.mjs"></script>
    <script type="module" src="app.mjs"></script>
    ```