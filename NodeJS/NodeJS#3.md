# Express
---

## View Engine - Nunjucks
- View Engine : 데이터베이스의 내용을 자연스럽게 HTML에 보여주는 엔진
- nunjucks 설치 : npm install nunjucks 명령어를 사용해 설치
- app.js에 추가할 코드
    ```javascript
    const nunjucks = require("nunjucks");

    nunjucks.configure("template", {
        autoscape: true,
        express: app
    })
    ```
- admin.js 수정 코드
    ```javascript
    router.get("/products", (req,res) {
        res.sender("admin/products.html", {
            message: "hello"
        });
    });
    ```
- admin/products.html
    ```html
    express {{ message }}
    ```

> localhost:3000/admin/products에 express hello 가 표시됨

## 템플릿 상속
- template/layout/base.html
    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>{{ title }}</title>

        // Bootstrap
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-BmbxuPwQa2lc/FVzBcNJ7UAyJxM6wuqIj61tLrc4wSX0szH/Ev+nYRRuWlolflfl" crossorigin="anonymous">
    </head>
    <body>
        <div class="container" style="padding-top: 100px;">
            {% block content %}{% endblock %}
        </div>
    </body>
    </html>
    ```

- template/admin/products.html
    ```html
    <!-- title 지정 -->
    {% set title = "관리자 리스트" %} 
    <!-- base.html 파일을 불러옴 -->
    {% extends "layout/base.html" %} // ba

    {% block content -%}
        <table class="table table-bordered table-hover">
            <tr>
                <th>제목</th>
                <th>작성일</th>
                <th>삭제</th>
            </tr>
            <tr>
                <td>제품 이름</td>
                <td>
                    2021-03-10
                </td>
                <td>
                    <a href="%" class="btn btn-danger">삭제</a>
                </td>
            </tr>
        </table>

        <a href="/admin/products/write" class="btn btn-default">작성하기</a>

    {% endblock %}
    ```

- 화면이 바뀌어도 상단 navbar, footer등을 유지하기 위해 사용

## Middleware
- 미들웨어 함수란 클라이언트에게 요청이 오고 그 요청을 보내기 위해 응답하려는 중간에 목적에 맞게 처리하는 즉, 거쳐가는 함수
- 예를들면 로그인이 됬는지의 유무를 판단하고 보여주는 페이지가 다를수 있음
```javascript
function loginRequired(req, res, next) {
    if(로그인이 되어있지 않으면) {
        res.redirect(로그인창)
    } else {
        next();
    }
}

// localhost:3000/admin
router.get("/", loginRequired, (req, res) => {
    res.send("admin 이후 url");
});
```

- 미들웨어는 req, res, next 3개의 인자를 받음

## form(body-parser)
- parsing(파싱) : 데이터를 내가 원하는 형태로 가공
- 미들웨어 없이 req.body에 접근할 경우 기본적으로 undefined로 설정이 되어 있기 때문에 body-parser 같은 미들웨어를 사용하여 데이터 값에 접근
- 특정 버전 이후 express는 npm install 과정을 거치지 않고도 자바스크립트 파일에 간단한 코드만 추가하여 사용이 가능하다.
    ```javascript
    // app.js
    const bodyParser = require("body-parse");

    app.use(bodyParser.urlencoded({ extended: false }));
    ```

## 정적파일
- 이미지, css, js를 올리는 경우 경로를 지정하여 코드를 짜는 방법도 있지만 이는 코드를 굉장히 복잡하게 만듦
```javascript
app.use("/public", express.static("public"));
// "/public"은 url, "public"은 폴더명
```
- express.static 메서드는 node프로세스 디렉터리에 상대적이기 때문에 절대 경로를 사용하는 것이 안전함
    ```javascript
    app.use("/static", express.static(__dirname + "/public"));
    ```

## 404, 500 error handling
- template/common폴더에 404.html, 500html을 만듦
```html
{% set title = "페이지가 없습니다" %}
{% extends "layout/base.html" %}

{% block content -%}

<div class="container">
    <div class="page_area">
        <h1>페이지가 없습니다.</h1>
    </div>
</div>

{%- endblock %}
```
- 위 코드와 같은 형식으로 404.html, 500html 만들기
- app.js 마지막 부분에 추가할 코드
    ```javascript
    app.use((req, res, next) => {
        res.status(400).render("common/404.html");
    })
    ```

## express 권장 구조
- controllers/index: 대분류 url + 폴더 위치
- controllers/admin/index.js: admin url + 미들웨어
- controllers/admin/admin.ctrl.js: 컨트롤러 역할

## url추가 없이 메서드만 변경해서 작업 처리
1. GET /users -> 사용자 정보
2. POST /users -> 사용자 추가
3. GET /users/(ID) -> 한명만 볼때
4. PUT /users(ID) -> 한명 수정
5. DELETE /users/(ID) -> 삭제