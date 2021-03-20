# [프로그래머스] 같은 숫자는 싫어
---

1. 문제 설명 : 임의의 양의 정수 n에 대해, n이 어떤 양의 정수 x의 제곱인지 아닌지 판단하려 합니다. n이 양의 정수 x의 제곱이라면 x+1의 제곱을 리턴하고, n이 양의 정수 x의 제곱이 아니라면 -1을 리턴

2. 제한사항
    - n은 1이상, 50000000000000 이하인 양의 정수

3. 예시

n|return
--|--
121|144
3|-1

4. 내가 푼 코드
```javascript
function solution(n) {
    var sqrt = Math.sqrt(n); // n의 제곱근
    
    // sqrt의 값이 정수일 경우 +1을 하고 제곱
    // 정수가 아닐 경우 -1 return
    // ES6이후 도입된 ** 연산자
    if (Number.isInteger(sqrt) === true) { 
        return (sqrt+1) ** 2;
    }
    else {
        return -1;
    }
}
```