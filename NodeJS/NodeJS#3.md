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