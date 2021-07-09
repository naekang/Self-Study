# Chapter20 - strict mode
---

## 20.1 strict mode란?
- 암묵적 전역(Implicit global)은 오류를 발생시킬 수 있는 원인이 될 수 있으므로 반드시 `var`, `const`, `let`으로 변수 선언한 뒤 사용해야함
- 이러한 암묵적 전역을 예방하기 위해 `strict mode`가 도입
- 꿀Tip! : `ESLint` 사용하기

## 20.2 strict mode의 적용
- 전역의 선두 또는 함수의 몸체에 `'use strict';` 추가하기

## 20.3 전역에 strict mode를 적용하는 것은 피하자
- 전역에 적용한 strict mode는 스크립트 단위로 적용
- 전역에 사용하면 non-strict mode 서드파티 라이브러리와 충돌을 일으킬 수 있음

## 20.4 함수 단위로 strict mode를 적용하는 것도 피하자
- 번거로운 일이며 적용된 함수가 참조할 외부 함수의 컨텍스트에도 일일히 찾아서 걸어야 함

> strict mode는 즉시 실행 함수로 감싼 스크립트 단위로 적용하는 것이 바람직함

## 20.5 strict mode가 발생시키는 에러

### 20.5.1 암묵적 전역
- 선연하지 않은 변수를 참조하면 ReferenceError
    ```javascript
    (function () {
        'use stict';

        x = 1;
        console.log(x); // ReferenceError: x is not defined
    }());
    ```

### 20.5.2 변수, 함수, 매개변수의 삭제
- delete 연산자로 변수, 함수, 매개변수 삭제하면 SyntaxError
    ```javascript
    (function () {
        'use strict';

        var x = 1;
        delete x; // SyntaxError: Delete of an unqualified identifier in strict mode.

        function foo(a) {
            delete a; // SyntaxError: Delete of an unqualified identifier in strict mode.
        }
        delete foo; // SyntaxError: Delete of an unqualified identifier in strict mode.
    }());
    ```

### 20.5.3 매개변수 이름의 중복
- 중복된 매개변수 이름을 사용하면 SyntaxError
    ```javascript
    (function () {
        'use strict';

        // SyntaxError: Duplicate parameter name not allowed in this context
        function foo(x, x) {
            return x + x;
        }
        console.log(foo(1,2));
    })
    ```

### 20.5.4 with 문의 사용
```javascript
(function () {
    'use strict';

    with({ x: 1 }) {
        console.log(x);
    }
}());
```


## 20.6 strict mode 적용에 의한 변화

### 20.6.1 일반 함수의 this
- `use strict`에서 함수를 일반 함수로서 호출하면 this에 undefined가 바인딩

### 20.6.2 arguments 객체
- 매개변수에 전달된 인수를 재할당하여 변경해도 arguments 객체에 반영되지 않음