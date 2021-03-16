# [프로그래머스] 같은 숫자는 싫어
---
1. 문제 설명 : 배열 arr가 주어지고 각 원소는 0부터 9로 이루어져있다. 연속적으로 같은숫자가 나타나면 하나만 남기고 전부 제외한다. 예를 들면 
    - arr = [1,1,3,3,0,1,1] 이면 [1,3,0,1]을 return

2. 제한사항
    - 배열 arr 크기 : 1,000,000이하의 자연수
    - 배열 arr의 원소의 크기 : 0보다 크거나 같고 9보다 작거나 같은 정수

3. 내가 푼 코드
```javascript
function solution(arr)
{
    var answer = []; // 배열 return 에정
    var pointer = arr[0]; // 배열의 각 원소들을 나타내기 위한 포인터
    answer.push(pointer);

    // 반복문을 통해 배열의 처음부터 끝까지 한번씩 돌면서 겹치는 부분이 있는지 확인
    // pointer와 arr[i]의 값을 비교하며 같지 않을 경우 그 값을 answer 배열에 push
    // push 후 pointer의 값을 변경하고 같은 행위를 반복하여 겹치지 않는 숫자만 answer 배열에 넣는다.
    for(var i=0; i<arr.length; i++) {
        if(pointer !== arr[i]) {
            pointer = arr[i];
            answer.push(pointer);
        }
    }
    return answer;
}
```