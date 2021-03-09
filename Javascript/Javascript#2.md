# Javascript 기본 문법 정리
---

## jQuery 기본 정리
1. jQuery의 장점
   - 주요 웹브라우저의 구버전을 포함한 대부분의 브라우저에서 지원함
   - HTML DOM을 쉽게 조작할 수 있으며 CSS도 간단히 적용 가능
   - 애니메이션 효과, 대화형 처리 간단 적용 가능
   - 짧은 프로그래밍 가능
   - 오픈소스로서 누구나 사용가능
   - 참고 문서가 많다

2. 적용방법
   - [jquery cdn](https://code.jquery.com/) 참고

3. 기본 문법 정리
    1. 기본 문법
    ```javascript
    $(선택자).동작함수();
    // $: jQuery에 접근할 수 있게 해주는 식별자
    ```
    
    2. $() 함수
    - 선택된 HTML요소를 jQuery에서 이용할 수 있는 형태로 생성
    - $() 함수를 통해 생성된 요소 = jQuery object
    
    3. Document객체의 ready() 메소드
    - 아직 생성되지 않은 HTML요소에 속성을 추가하는 예제
    ```javascript
    function func() {
        addAttribute(); // 아이디가 "para"인 HTML요소에 속성을 추가
        createElement(); // 아이디가 "para"인 HTML요소 생성
    }
    function createElement() {
        var criteriaNode = document.getElementById("text");
        var newNode = document.createElement("p")
        newNode.innerHTML = "새로운 단락입니다.";
        newNode.setAttribute("id","para");
        document.body.insertBefore(newNode, criteriaNode);
    }
    function addAttribute() {
        document.getElementById("para").setAttribute("style","color:red");
    }
    ```

    - jQuery에서는 Document객체의 ready() 메소드를 이용하여 문서가 모두 로드된 뒤 코드가 실행되도록 함
    ```javascript
    $(document).ready(function() {
        jQuery Code;
    });
    ```

    4. CSS선택자를 이용한 선택
    - $() 함수에 전달되는 인수는 반드시 ""를 사용한 문자열의 형태로 전달되어야 함
    ```javascript
    $(function () {
        $("p").on("click", function() { // <p>요소 선택
            $("span").css("fontsize", "29px"); // <span>요소 모두 선택
        })
    })
    ```
    - 요소 선택 후 :eq(n), :gt(n) 등을 사용하여 필터링 가능

    5. getter, setter 메소드
    - getter 메소드: 선택된 요소에 접근하여 그 값을 읽어오기 위한 메소드
    - setter 메소드: 선택된 요소에 접근하여 그 값을 설정하기 위한 메소드
    ex) <h1> 요소에 접근하고 id가 text인 요소의 값을 해당값으로 설정하는 코드
    ```javascript
    $(function() {
        $("button").on("click", function() {
            var newText = $("h1").html(); // <h1>요소의 텍스트를 읽어오는 getter 메소드
            $"#text".html(newText); // 
        })
    })
    ```
    
## ES5 vs ES6
1. 변수 선언 방식의 추가
- var뿐만 아니라 let, const 추가
    1. var - Function Level Scope
    ```javascript
    var name = "javascript";
    console.log(name); // javascript

    var name = "cafe";
    console.log(name); // cafe
    ```
    - 같은 변수를 한번 더 출력했으나 에러 안남
    - 간단한 코딩테스트에는 편리하지만 코드량이 많아지는 경우 값이 바뀌는 문제 발생

    2. let - Block Level Scope
    ```javascript
    let name = "javascript";
    console.log(name); // javascript

    let name = "cafe";
    console.log(name);
    // Uncaught SyntaxError: Identifier 'name' has already been declared

    name = "waffle";
    console.log(name); // waffle
    ```
    - 변수 재할당은 가능하지만 재선언은 불가능

    3. const - Block Level Scope
    ```javascript
    const name = "javascript";
    console.log(name); // javascript

    const name = "cafe";
    console.log(name); 
    // Uncaught SyntaxError: Identifier 'name' has already been declared

    name = "waffle"
    console.log(name);
    // Uncaught TypeError: Assignment to constant variable
    ```
    - 변수 재할당과 재선언 모두 불가능

    >재할당이 필요없는 경우 const를 사용하여 불필요한 변수의 재사용을 방지하고 재할당이 필요한 경우 let을 사용하는 것이 좋음

2. Arrow Function 추가
- 흔히 화살표 함수라고 하는 것이 추가되어 가독성 및 보수성이 향상되었다.
```javascript
// es5
function sum (a+b) {
    return a+b;
}

// es6
const sum = (a,b) => a+b;
```

3. Templete Literal 추가
- ``(back tick)과 ${}를 사용하여 간결하게 표현 가능
- 여러 라인의 문자열도 처리 가능
```javascript
// es5
var firstName = "jinho";
var lastName = "Kim";
var name = "My name is " + first + " " + last + ".";

// es6
var name = `My name is ${first} ${last}.`;
```

4. 클래스

5. 모듈

6. Promises
- 기존 비동기 통신의 경우 콜백함수를 사용하였으나 ES6로 넘어오면서 promise가 도입되었고 콜백 지옥의 문제에서 벗어날 수 있었음
