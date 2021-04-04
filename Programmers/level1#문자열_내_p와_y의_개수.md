# [프로그래머스] 3진법 뒤집기
---

1. 문제 설명 : 대문자와 소문자가 섞여있는 문자열 s가 주어집니다. s에 'p'의 개수와 'y'의 개수를 비교해 같으면 True, 다르면 False를 return 하는 solution를 완성하세요. 'p', 'y' 모두 하나도 없는 경우는 항상 True를 리턴합니다. 단, 개수를 비교할 때 대문자와 소문자는 구별하지 않습니다.

예를 들어 s가 "pPoooyY"면 true를 return하고 "Pyy"라면 false를 return합니다.

2. 제한사항
    - 문자열 s의 길이 : 50 이하의 자연수
    - 문자열 s는 알파벳으로만 이루어져 있습니다.

3. 예시

    s|answer
    --|--
    "pPoooyY"|true
    "Pyy"|false

4. 내가 푼 코드
- p와 y의 count를 0으로 초기화 한 후 조건에 맞는 경우 1 증가
- pCount값과 yCount값이 같을 경우 true 반환
```javascript
function solution(s){
    var pCount = 0;
    var yCount = 0;
    
    for(var i=0; i<s.length; i++) {
        // 문자열을 돌며 소문자(대문자) p(P) 가 있는지 확인
        if(s[i] === 'p' || s[i] === 'P') {
            pCount++;
        }
        // 문자열을 돌며 소문자(대문자) y(Y) 가 있는지 확인
        if(s[i] === 'y' || s[i] === 'Y') {
            yCount++;
        }
    }
    if(pCount === yCount) {
        return true;
    } else
        return false;
}
```