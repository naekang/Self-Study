# [프로그래머스] 가운데 글자 가져오기
---

1. 문제 설명 : 단어 s의 가운데 글자를 반환하는 함수. 단어의 길이가 짝수라면 가운데 두글자를 반환함

2. 제한사항
    - s는 길이가 1이상, 100이하인 스트링

3. 예시

    s|return
    --|--
    "abcde"|"c"
    "qwer"|"we"

4. 내가 푼 코드
- 단어의 길이가 짝수일 경우와 홀수일 경우를 나누어 계산
- 자바스크립트의 substr() 함수를 이용해 특정 인덱스부터 특정 길이만큼 잘라낼 수 있음
```javascript
function solution(s) {
    var answer = '';
    if(s.length % 2 === 0) {
        // 짝수일 경우 가운데 2개의 글자를 추출
        answer = s.substr((Math.floor(s.length / 2) -1), 2);
    } else {
        // 홀수일 경우 가운데 한글자 추출
        answer = s.substr(Math.floor(s.length / 2), 1);
    }
    
    return answer;
}
```