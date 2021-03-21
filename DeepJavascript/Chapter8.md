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

### 8.2.2 switch 문