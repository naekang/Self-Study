# Chapter8 - 제어문
---
- 일반적으로 코드는 순차적으로 진행되지만 제어문을 통해 제어 가능

## 8.1 블록문(Block Statement)
- 0개 이상의 문을 중괄호로 묶은 것
- 코드 블록
- 블록문의 끝에는 세미콜론을 붙이지 않음

## 8.2 조건문(Conditional Statement)
- if...else문과 switch문 두 가지

### 8.2.1 if ... else 문
```
if (조건식) {
    // 조건식이 참일 경우 이 코드 블록 실행
} else {
    // 조건식이 거짓일 경우 이 코드 블록 실행
}
```
```
if (조건식1) {
    // 조건식1이 참이면 이 코드 블록 실행
} else if (조건식2) {
    // 조건식2가 참이면 이 코드 블록 실행
} else {
    // 조건식1과 조건식2가 모두 거짓이면 이 코드 블록 실행
}
```
- 코드 블록 내 문장이 하나라면 중괄호 생략 가능
- 대부분 삼항 조건 연산자로 변환 가능
- x가 짝수이면 '짝수' 출력, 홀수이면 '홀수' 출력
```javascript
var x = 2;
var result;

// 0은 암묵적 형태 변환에 의해 false로 변환됨
if (x % 2) {
    result = '홀수';
} else {
    result = '짝수';
}

console.log(result);
```
```javascript
var x = 2;

var result = x % 2 ? '홀수' : '짝수';
console.log(result);
```

- 단순한 조건문일 경우는 삼항 연산자를 사용해도 되지만 복잡할 경우는 if ... else문을 사용하도록

### 8.2.2 switch 
```
switch (표현식) {
    case 표현식1 :
        switch 문의 표현식과 표현식1이 일치하면 실행될 문;
        break;
    case 표현식2 :
        switch 문의 표현식과 표현식2가 일치하면 실행될 문;
        break;
    default :
        switch 문의 표현식과 일치하는 case문이 없을 떄 실행될 문;
}
```
- break문을 사용하지 않을 경우 마지막 default까지 실행됨 -> 폴스루(fall through)
- default 문에서는 break문을 생략하는 것이 일반적임
- if ... else문을 사용할 수 있으면 사용하는 것이 좋음

## 8.3 반복문(Loop Statement)
- for 문, while 문, do ... while 문
- 반복문을 대체하기 위한 메서드들도 존재
    - forEach 메서드, for ... in 문, for ... of 문

### 8.3.1 for 문
```
for (변수 선언문 또는 할당문; 조건식; 증감식) {
    조건식이 참일 경우 반복 실행될 문;
}
```
- for 문을 중첩해서 사용가능

### 8.3.2 while 문
- 주어진 조건식의 결과가 참이면 반복실행

```javascript
var count = 0;

while (true) {
    console.log(count);
    count++;
    // count값이 3이면 탈출
    if (count === 3)
        break;
}
```

### 8.3.3 do ... while 문
- 코드블록 먼저 실행 후 조건식 평가
```javascript
var count = 0;

do {
    console.log(count);
    count++;
} while (count < 3);
```

## 8.4 break문
- 코드 블록 탈출
- 반복문 이외에서 break문을 쓰면 문법 에러 발생
- 문자열에서 특정 문자의 인덱스 검색 예시
    ```javascript
    var string = 'Hello World';
    var search = 'l';
    var index;

    for (var i = 0; i < string.length; i++) {
        if (string[i] === search) {
            index = i;
            break;
        }
    }
    console.log(index); // 2
    console.log(string.indexOf(search)); // 2
    ```

## 8.5 continue 문
- 반복문의 코드블록을 현 지점에서 중단하고 증감식으로 이동시킴
- if문 내에서 실행해야 할 코드가 길면 continue를 사용하는 편이 가독성에 좋음
```javascript
// continue 문을 사용하지 않으면 if문 내에 코드를 작성해야함
for (var i = 0; i < string.length; i++) {
    // 'l'이면 카운트 증가
    if (string[i] === search) {
        count++;
        // code
        // code
    }
}

// continue문을 사용하면 if문 밖에 코드 작성 가능
for (var i = 0; i < string.length; i++) {
    // 'l'이면 카운트 증가
    if (string[i] === search) continue;
    
    count++;
    // code
    // code

}
```