# [프로그래머스] 소수 만들기
---

1. 문제 설명 : 주어진 숫자 중 3개의 수를 더했을 떄 소수가 되는 경우의 개수를 구하려고 합니다. 숫자들이 들어가 있는 배열 nums가 매개변수로 주어질 때, nums에 있는 숫자들 중 서로 다른 3개를 골라 더했을 때 소수가 되는 경우의 개수를 return

2. 제한사항
    - nums에 들어있는 숫자의 개수는 3개 이상 50개 이하
    - nums의 각 원소는 1 이상 1,000 이하의 자연수이며, 중복된 숫자가 들어있지 않습니다.

3. 예시

    nums|result
    --|--
    [1,2,3,4]|1
    [1,2,7,6,4]|4

4. 내가 푼 코드
- 3중 for문을 통해 3개 숫자의 합을 구하고 isPrime이라는 함수를 하나 더 만들어서 검사
- isPrime함수의 경우 1과 자기 자신 외의 수로 나누어 지는지 확인하고 나누어 지지 않는 경우만 true로 반환
```javascript
function solution(nums) {
    var answer = 0;
    
    // 3개의 숫자들을 골라 합을 구하는 과정
    for (var i = 0; i < nums.length; i++) {
        for (var j = i + 1; j < nums.length; j++) {
            for (var k = j + 1; k < nums.length; k++) {
                var sum = nums[i] + nums[j] + nums[k];
                // isPrime 함수의 검사를 통해 소수일 경우 0으로 초기화 된 answer의 값을 1씩 증가
                if (isPrime(sum) === true) {
                    answer++;
                }
            }
        }
    }
    
    // 주어진 값이 소수인지 아닌지 검사하기 위한 함수
    function isPrime(n) {
        // 소수란 1과 자기자신 이외의 다른 자연수로는 나눠질 수 없는 수
        // for문을 통해 1과 자기자신 이외의 다른 자연수로 나누어 떨어지는 경우가 있는지 확인하여 나누어 떨어지는 경우 false return 
        // 위의 경우를 제외한 나머지 경우는 true값 반환
        for (var i = 2; i < n; i++) {
            if (n % i === 0) {
                return false;
            } 
        }
        return true;
    }
    
    return answer;
}
```