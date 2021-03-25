# [프로그래머스] 핸드폰 번호 가리기
---

1. 문제 설명 : 전화번호가 문자열 phone_number로 주어졌을 때, 전화번호 뒷 4자리를 제외한 나머지 숫자를 전부 `*`으로 가린 문자열을 리턴하는 함수, solution을 완성하시오.

2. 제한사항
    - s는 길이 4 이상, 20이하인 문자열

3. 예시

phone_number|return
--|--
"01033334444"|"*******4444"
"027778888"|"*****8888"

4. 내가 푼 코드
```javascript
function solution(phone_number) {
    // phone_number의 마지막 4자리를 추출하여 backNumber에 저장
    var backNumber = phone_number.substr(phone_number.length-4, phone_number);
    
    // phone_number 총 길이에서 뒤의 4자리를 뺀 나머지 횟수만큼 * 반복 후 뒷 4자리와 더하기
    return '*'.repeat(phone_number.length-4) + backNumber;
}