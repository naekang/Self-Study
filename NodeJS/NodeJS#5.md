# Promise 기본
---

## CallbackHell
- callback 함수가 결과값을 가지고 callback을 다시 호출하고 이 과정을 인라인으로 처리하며 코드가 복잡하지는 것을 말한다.
- 코드를 따라가기도 어렵고 유지보수 역시 어려워지게 된다.
- 해결방법은 여러가지가 있다.
    1. 인라인 함수에 이름 붙이기
    2. 코드 간결하게 작성하기
    3. 모듈화
    4. Promise 도입
- 앞선 3가지 방법은 아무리해도 한계점이 존재하기에 근본적인 문제를 해결할 수는 없다.

## Promise란
- 자바스크립트 비동기 처리에 사용되는 객체
- 서버에서 받은 데이터를 화면에 표시할 때 사용하며 웹 구현시 다음과 같은 API사용
    ```javascript
    $.get('url주소/products/1', function(response){
        // ...
    });
    ```
- 간단한 에제 코드
    ```javascript
    var _promise = function(param) {
        return new Promise(function (resolve, reject) {
            window.setTimeout(function () {
                if (param) {
                    resolve("해결완료");
                }
                else {
                    reject(Error("실패!!"));
                }
            }, 3000);
        });
    };

    _promise(true).then(function (text) {
        // 성공시
        console.log(text);
    }, function (error) {
        // 실패시
        console.log(error);
    });
    ```
    - 실행 결과 : "해결완료"

## Promise 선언부
- '지금은 없는데 별 문제 없으면 주고 없으면 알려줄게' 라는 약속
    1. pending : 약속을 수행중인 상태
    2. fulfilled : 약속이 지켜진 상태
    3. rejeted : 약속이 어떤 이유에 의해 못 지켜진 상태
    4. settled : 약속이 이행됬든 안됬든 결론이 난 상태