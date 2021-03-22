# Chapter9 - 타입 변환과 단축 평가
---

## 9.1 타입 변환이란?
- 의도적으로 타입을 변환하는 것을 명시적 타입 변환(explicit coercion) 또는 타입 캐스팅(type casting)이라고 함
    ```javascript
    var x = 10;

    // 명시적 타입 변환
    // 숫자를 문자열로 타입 캐스팅
    var str = x.toString();
    console.log(typeof str, str); // string 10

    // x 변수의 값이 변경된 것은 아님
    console.log(typeof x, x); // number 10
    ```

- 자바스크립트 엔진에 의해 암묵적으로 변환되기도 하는데 이것을 암묵적 타입 변환(implicit coercion) 또는 타입 강제 변환(type coercion)이라 함
    ```javascript
    var x = 10;

    // 암묵적 타입 변환
    // 문자열 연결 연산자는 숫자 타입 x의 값을 바탕으로 새로운 문자열을 생성
    var str = x + '';
    console.log(typeof str, str); // string 10

    // x변수의 값이 변경된 것은 아님
    console.log(typeof x, x); // number 10
    ```

- 암묵적 타입 변환은 기존 변수 값을 재할당이 아니라 새로운 타입의 값을 만들어 한번 사용하고 버림
- 자신이 작성한 코드에서  어떤 값으로 변환되는지 어떻게 평가될 것인지 예측 가능해야함 -> 협업을 통한 프로젝트에 필수적!!!

## 9.2 암묵적 타입 변환
- 개발자의 의도와 상관없이 문맥을 고려해 암묵적 타입 변환을 할 때가 있음
    ```javascript
    // 피연산자가 모두 문자열 타입이어야 하는 문맥
    '10' + 2 // '102'

    // 피연산자가 모두 숫자 타입이어야 하는 문맥
    5 * '10' // 50

    // 피연산자 또는 표현식이 불리언 타입이어야 하는 문맥
    !0 // true
    if (1) { } 
    ```

### 9.2.1 문자열 타입으로 변환
- 문자열 값을 만드는 것
- ES6에서 도입된 템플릿 리터럴의 표현식 삽입은 표현식의 평가 결과를 문자열 타입으로 암묵적 타입 변환
    ```javascript
    `1 + 1 = ${1 + 1}` // "1 + 1 = 2"
    ```
    ```javascript
    // 숫자 타입
    0 + '' // "0"
    -0 + '' // "0"
    1 + '' // "1"
    -1 + '' // "-1"
    NaN + '' // "NaN"
    Infinity + '' // "Infinity"
    -Infinity + '' // "-Infinity"

    // 불리언 타입
    true + '' // "true"
    false + '' // "false"

    // null 타입
    null + '' // "null"

    // undefined 타입
    undefined + '' // "undefined"

    // 심벌 타입
    (Symbol()) + '' // TypeError: Cannot convert a Symbol value to a string

    // 객체 타입
    ({}) + '' // "[object Object]"
    Math + '' // "[object Math]"
    [] + '' // ""
    [10, 20] + '' // "10, 20"
    (function(){}) + '' // "function(){}"
    Array + '' // "function Array() { [native code] }"
    ```

### 9.2.2 숫자 타입으로 변환
- 숫자 값을 만드는 것
    ```javascript
    // 문자열 타입
    +'' // 0
    +'0' // 0
    +'1' // 1
    +'string' // NaN

    // 불리언 타입
    +true // 1
    +false // 0

    // null 타입
    +null // 0

    // undefined 타입
    +undefined // NaN

    // 심벌 타입
    +Symbol() // TypeError: Cannot convert a Symbol value to a number

    // 객체 타입
    +{} // NaN
    +[] // 0
    +[10, 20] // NaN
    +(function(){}) // NaN
    ```

### 9.2.3 불리언 타입으로 변환
- 자바스크립트 엔진은 불리언 타입이 아닌 값을 Truthy 값(참으로 평가되는 값) 또는 Falsy 값(거짓으로 평가되는 값)으로 구분
- Truthy/Falsy 값을 판별하는 함수
    ```javascript
    // 전달받은 인수가 Falsy 값이면 true, Truthy 값이면 false 반환
    function isFlasy(v) {
        return !v;
    }

    // 전달받은 인수가 Truthy 값이면 true, Falsy 값이면 false 반환
    function isTruthy(v) {
        return !!v;
    }

    // 모두 true 반환
    isFalsy(false);
    isFalsy(undefined);
    isFalsy(null);
    isFalsy(0);
    isFalsy(NaN);
    isFalsy('');

    // 모두 true 반환
    isTruthy(true);
    isTruthy('0');
    isTruthy({});
    isTruthy([]);
    ```

## 9.3 명시적 타입 변환
- 표준 빌트인 생성자 함수(String, Number, Boolean)를 new 연산자 없이 호출하는 방법
- 빌트인 메서드를 사용하는 방법
- 암묵적 타입 변환을 이용하는 방법

### 9.3.1 문자열 타입으로 변환
```javascript
// 1. String 생성자 함수를 new 연산자 없이 호출하는 방법
// 숫자 타입 => 문자열 타입
String(1); // "1"
String(NaN); // "NaN"
String(Infinity); // "Infinity"
// 불리언 타입 => 문자열 타입
String(true); // "true"
String(false); // "false"

// 2. Object.prototype.toString 메서드를 사용하는 방법
// 숫자 타입 => 문자열 타입
(1).toString(); // "1"
(NaN).toString(); // "NaN"
(Infinity).toString(); // "Infinity"
// 불리언 타입 => 문자열 타입
(true).toString(); // "true"
(false).toString(); // "false"

// 3. 문자열 연결 연산자를 이용하는 방법
// 숫자 타입 => 문자열 타입
1 + ''; // "1"
NaN + ''; // "NaN"
Infinity + ''; // "Infinity"
// 불리언 타입 => 문자열 타입
true + ''; // "true"
false + ''; // "false"
```

### 9.3.2 숫자 타입으로 변환
```javascript
// 1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
// 문자열 타입 => 숫자 타입
Number('0'); // 0
Number('-1'); // -1
Number('10.53'); // 10.53
// 불리언 타입 => 숫자 타입
Number(true); // 1
Number(false); // 0

// 2. parseInt, parseFloat 함수를 사용하는 방법(문자열만 가능)
parseInt('0'); // 0
parseInt('-1'); // -1
parseInt('10.53'); // 10.53

// 3. + 단항 산술 연산자를 이용하는 방법
// 문자열 타입 => 숫자 타입
+'0'; // 0
+'-1' // -1
+'10.53' // 10.53
// 불리언 타입 => 숫자 타입
+true; // 1
+false; // 0

// 4. * 산술 연산자를 이용하는 방법
// 문자열 타입 => 숫자 타입
'0' * 1; // 0
'-1' * 1; // -1
'10.53' * 1; // 10.53
// 불리언 타입 => 숫자 타입
true * 1; // 1
false * 1; // 0
```

### 9.3.3 불리언 타입으로 변환
1. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
2. ! 부정 논리 연산자를 두 번 사용하는 방법


## 9.4 단축 평가

### 9.4.1 논리 연산자를 사용한 단축 평가
- 논리합 또는 논리곱 연산자 표현식의 평가 결과는 불리언 값이 아닐 수 있음
- 논리 연산의 결과를 결정하는 피연산자를 타입 변환하지 않고 그대로 반환 -> 단축 평가(short-circuit evaluation)
    단축 평가 표션식|평가 결과
    --|--
    true &#124;&#124; anything|true
    false &#124;&#124; anything|anything
    true && anything|anything
    false && anything|false

#### 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때
- 객체는 키와 값으로 구성된 프로퍼티의 집합
- 객체를 가리키기를 기대하는 변수의 값이 객체가 아니라 null 또는 undefined인 경우 객체의 프로퍼티를 참조하면 타입 에러 발생
    ```javascript
    var elem = null;
    var value = elem.value; // TypeError

    var elem = null;
    var value = elem && elem.value; // null
    ```

#### 함수 매개변수에 기본값을 설정할 때
- 함수를 호출할 떄 인수를 전달하지 않으면 매개변수에는 undefined 할당
- 이떄 단축평가를 사용해 기본값을 설정하면 에러 방지 가능
    ```javascript
    // 단축 평가를 사용한 매개변수의 기본값 설정
    function getStringLength(str) {
        str = str || '';
        return str.length;
    }
    
    getStringLength(); // 0
    getStringLength('hi'); // 2

    // ES6 매개변수의 기본값 설정
    function getStringLength(str = '') {
        return str.length;
    }

    getStringLength(); // 0
    getStringLength('hi'); // 2
    ```

### 9.4.2 옵셔널 체이닝 연산자
- ES11에서 도입된 옵셔널 체이닝 연산자 ?.는 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어감
    ```javascript
    var elem = null;

    var value = elem?.value;
    console.log(value); // undefined
    ```
- 옵셔널 체이닝 연산자 ?.는 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 떄 유용
- 논리 연산자 &&는 false로 평가되는 Falsy 값이면 좌항 피연산자를 그대로 반환
    ```javascript
    var str = '';

    var length = str && str.length;

    console.log(length); // ''
    ```
    ```javascript
    var str = '';

    var length = str?.length;
    
    console.log(length); // 0
    ```

### 9.4.3 null 병합 연산자
- ES11에서 도입된 null 병합 연산자 ??는 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 반환
- 변수에 기본값을 설정할 때 유용
    ```javascript
    var foo = '' || 'default string';
    console.log(foo); // "default string"
    ```
    ```javascript
    var foo = '' ?? 'defalut string';
    console.log(foo); // ""
    ```