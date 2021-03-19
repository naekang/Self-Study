# [프로그래머스] 서울에서 김서방 찾기
---

1. 문제 설명 : String형 배열 seoul의 element중 "Kim"의 위치 x를 찾아, "김서방은 x에 있다"는 String을 반환하는 함수
    - seoul에 "Kim"은 오직 한번 나타남

2. 제한 사항
    - seoul은 길이 1이상, 1000 이하인 배열
    - seoul의 원소는 길이 1이상, 20 이하인 문자열
    - "Kim"은 반드시 seoul안에 포함

3. 예시

seoul|return
--|--
["Jane", "Kim"]|"김서방은 1에 있다"

4. 내가 푼 코드
- 처음에는 배열의 원소들과 "Kim"을 반복문을 통해 하나씩 비교하는 방법으로 생각했다.
```javascript
function solution(seoul) {
    for(var i=0; i < seoul.length; i++) {
        if (seoul[i] === "Kim") {
            return "김서방은 " + i +"에 있다"; 
        }
    }
}
```
- 간단한 자바스크립트 함수를 써서 작성해보기
- indexOf함수 : 문자열에서 특정 문자열을 찾고 가장 먼저 발견하는 위치 index return
```javascript
function solution(seoul) {
    var index = seoul.indexOf('Kim');
    return `김서방은 ${index}에 있다`; // ES6이후 도입된 방법
}
```