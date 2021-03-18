# [프로그래머스] 124 나라의 숫자
---

1. 문제설명 : 10진법이 아닌 규칙으로 숫자 표현
    - 자연수만 존재
    - 모든 수를 표현할 떄 1,2,4만 사용

10진법|124나라|10진법|124나라
--|--|--|--
1|1|6|14
2|2|7|21
3|4|8|22
4|11|9|24
5|12|10|41

2. 제한사항
   - n은 500,000,000이하의 자연수


3. 내가 푼 코드
    - 3개 단위로 앞자리 숫자가 바뀌는 것을 통해 3으로 나눈다는 생각을 먼저해봄
    - 소인수 분해할때 사용하는 나눗셈 방식을 이용하여 규칙 확인
```javascript
function solution(n) {
    var answer = [];
    
    while(n > 0) {
        switch (n % 3) {
            case 0:
                answer.push('4'); // 규칙성을 통해 나머지값에 따른 치환 문자 확인
                n = Math.floor(n/3) - 1; // 나머지가 0일 경우 몫에서 -1을 하고 반복문을 돌면 원하는 값이 나오는 것을 확인
                break;
            case 1:
                answer.push('1');
                n = Math.floor(n/3); // 몫을 정수로 표현
                break;
            case 2:
                answer.push('2');
                n = Math.floor(n/3); // 몫을 정수로 표현
                break;
        }
    }
    answer = answer.reverse(); // answer배열 안의 요소들을 거꾸로 뒤집음
    return answer.join(''); // answer배열을 문자열로 변환
}
```