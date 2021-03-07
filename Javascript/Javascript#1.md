# Javascript 기본 문법 정리
---
## 자바스크립트 변수형
- var, const, let 등으로 선언(var i = 1;)
- 동적언어이기 때문에 자료형을 선언하지 않음
- 기본 자료형
  |기본 자료형|설명|
  |--|--|--|
  |Boolean|논리적인 요소(True or False)|
  |NULL|값이 존재하지 않음|
  |Undefined|값을 할당하지 않음|
  |Number|숫자형|
  |String|문자형|
  |Symbol|ES6에서 추가|

## 자바스크립트의 배열
- var a = ['javascript', 'node.js', 55, 'hello']
  |0|1|2|3|
  |--|--|--|--|
  |javascript|node.js|55|hello|
  |a[0]|a[1]|a[2]|a[3]|
- a.length = 4 -> 배열의 길이
- a.indexOf('node.js') = 2 -> 몇번째 배열인지

## 자바스크립트의 반복문
1. for문
```javascript
for (var i=0; i<5; i++) {
    console.log(i);
    documnet.write('화면에 찍기');
}
// 0 1 2 3 4
```
2. while문
```javascript
var i = 0;
while (i<5) {
    documnet.write('화면에 찍기');
}
```
3. do-whil문
```javascript
var i = 0;
do {
    documnet.write('화면에 찍기');
} while (i<4)
```

ex) 구구단 만들기
```javascript
for (var i=2; i<=9; i++) {
    for (var j=1; j<=9; j++) {
        document.write(i + '*' + j + '=' + i*j);
        document.write('<br>');
    }
    document.write('<br>');
}
```

## 자바스크립트의 함수
```javascript
function Car(a, b, c) {
    this.name = a;
    this.color = b;
    var move = c; // private 변수
}

var a = new Car("현대", "노란", "전진")
console.log(a.name);
console.log(a.color);
console.log(a.move); // 오류 출력
var b = new Car("기아", "파란", "전진")
```

## 자바스크립트 프로토타입
- class개념이 없는 대신 프로토타입이 존재
```javascript
// function Car(a, b) {
//     this.name = a;
//     this.color = b;
// }

// Car.prototype.move = function() {
//     console.log(this.name + "차이고 " + this.color + "색입니다.);
// }

// var a = new Car("현대", "노란")
// a.move()
// var b = new Car("기아", "파란")
// b.move()

var a =[1,2,3,4,10];
Array.prototype.print = function() {
    for (var i=0; i<this.length; i++) {
        console.log(i);
    }
}
a.print();

```

## 자바스크립트 리터럴객체
- Object 객체를 생성하기 위해 { ... } 을 이용하는 코드
```javascript
var a = {
    'a' : 110,
    'b' : 'hello',
    'c' : function() {
        console.log('gggg');
    }
}
Object.prototype.sum = function() {
    console.log(this.a + 20);
}

a.sum(); // 130
```

## 자바스크립트에서의 this
1. 단독 this
   - window
2. 함수 안에서의 this
   - window의 객체 / 함수의 주인에게 바인딩
3. 메서드 안에서의 this
   - 해당 메서드를 호출한 객체로 바인딩

## 자바스크립트의 조건문
1. if문
```javascript
var a = 10;
if (a < 10) {
    console.log('10보다 작습니다.');
} else if (a < 15 && a >= 10) {
    console.log('10보다 크거나 같고 15보다 작습니다.');
}
```
2. switch문