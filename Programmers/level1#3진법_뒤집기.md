# [프로그래머스] 3진법 뒤집기
---

1. 문제 설명 : 자연수 n이 매개변수로 주어집니다. n을 3진법 상에서 앞뒤로 뒤집은 후, 이를 다시 10진법으로 표현한 수를 return 하도록 solution 함수를 완성해주세요.

2. 제한사항
    - n은 1이상 100,000,000 이하인 자연수

3. 예시

    n|result
    --|--
    45|7
    125|229

4. 내가 푼 코드
- 자바스크립트의 배열 중복 제거 방법 중 한가지인 Set 객체를 이용하는 방법을 사용하였다.
- 최대 결과값인 N/2를 지정해두고 비교하여 결과값을 출력한다.
```javascript
function solution(n) {
    // 10진법 -> 3진법 변환
    var tetra = n.toString(3);
    // 띄어쓰기 없이 역으로 재배열한 후 
    var tetraReverse = tetra.split("").reverse().join("");
    
    // 문자열을 정수로 변환하여 return
    return parseInt(tetraReverse, 3);
}
```