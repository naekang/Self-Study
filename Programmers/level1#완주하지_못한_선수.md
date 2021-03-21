# [프로그래머스] 완주하지 못한 선수
---

1. 문제 설명 : 마라톤에 참여한 선수들의 이름이 담긴 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return

2. 제한사항
    - 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하
    - completion의 길이는 participant의 길이보다 1 작다.
    - 참가자 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어짐
    - 참가자중 동명이인이 있을 수 있음

3. 예시

    participant|completion|return
    --|--|--
    ["leo","kiki","eden"]|["eden","kiki"]|"leo"
    ["mislav","stanko","mislav","ana"]|["stanko","ana","mislav"]|"mislav"

4. 내가 푼 코드
- 두개의 배열을 정렬한 후 element하나씩 비교하여 참가자 중 없는 사람 출력
```javascript
function solution(participant, completion) {
    // 자바스크립트 내장함수 sort를 이용하여 배열 정렬
    participant.sort();
    completion.sort();
    
    // 반복문을 통해 정렬된 배열끼리 element 하나씩 비교하고 참가자 중 없는 이름 출력
    for (var i=0; i<participant.length; i++)
    {
        if (participant[i] !== completion[i])
        {
            return participant[i];        
        }
    }
}
```