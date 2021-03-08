# 프로그래머스 [카카오인턴십] 키패드 누르기
---
1. 문제 설명 : 키패드에서 왼손과 오른손의 엄지손가락만을 이용하여 숫자를 입력하려고 한다. 맨 처음 엄지손가락은 * 키패드에 오른손 엄지손가락은 # 키패드 위치에서 시작한다. 
- 상세규칙
  1. 엄지손가락은 상하좌우로만 움직이며 거리는 1칸이다.
  2. 1,4,7은 왼손 엄지손가락만 사용한다.
  3. 3,6,9는 오른손 엄지손가락만 사용한다.
  4. 가운데열의 4개 숫자 2,5,8,0은 두 엄지손가락의 마지막 위치에서 더 가까운 거리의 엄지손가락이 움직이며 거리가 같을 경우 오른손 잡이는 오른손으로 왼손잡이는 왼손을 사용한다.

2. 제한사항
   - numbers 배열의 크기는 1이상 1,000 이하
   - numbers 배열 원소의 값은 0 이상 9이하인 정수
   - hand는 "left" 또는 "right"
   - 왼손을 사용한 경우 return L, 오른손을 사용한 경우 return R


3. 내가 푼 코드
```javascript
// 각 키보드의 위치에 맞게 좌표를 지정해준다.
const keypad = [[3,1],[0,0],[0,1],[0,2],[1,0],[1,1],[1,2],[2,0],[2,1],[2,2],[3,0],[3,2]];

// 오른손, 왼손의 첫 시작점을 지정
var leftStartPoint = 10;
var rightStartPoint = 12;

// 두 입력 값 사이의 거리를 구하기 위한 함수
function dis(a,b) {
        return Math.abs(keypad[a][0]-keypad[b][0]) + Math.abs(keypad[a][1]-keypad[b][1]);
    }

// 오른손으로 입력해야하는 경우 값을 저장
function rightHand(num) {
    rightStartPoint = num;
    return "R";
}

// 왼손으로 입력해야하는 경우 값을 저장
function leftHand(num) {
    leftStartPoint = num;
    return "L";
}


function solution(numbers, hand) {
    var answer = "";
    
    // map method: 배열의 있는 값들의 반환값으로 새로운 배열을 만들기 위해 사용
    var answer = numbers.map(num => {
        
        if (num === 1 || num === 4 || num === 7) {
           return leftHand(num); // 1,4,7은 무조건 왼손 엄지
        } else if (num === 3 || num === 6 || num === 9) {
           return rightHand(num); // 3,6,9는 무조건 오른손 엄지
        } else {
           var lDis = dis(num,leftStartPoint); // 왼손엄지의 마지막 입력값과의 거리
           var rDis = dis(num,rightStartPoint); // 오른손엄지의 마지막 입력값과의 거리
           
           if (lDis === rDis) { // 거리가 같을 경우 오른손잡이, 왼손잡이에 따라 반환값이 달라짐
              if (hand === "right") {
                  return rightHand(num);
              } else {
                  return leftHand(num);
              }
           } else { // 거리가 다를 경우 거리가 가까운쪽의 손가락이 이동
               if (lDis > rDis) {
                   return rightHand(num);
               } else {
                   return leftHand(num);
               }
           }
       }
    });
    
    return answer.join(""); // answer배열을 seperator없이 연결된 문자열 리턴
}
```