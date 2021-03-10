# Express
---
## Express란
- Node.js의 핵심 모듈인 http와 Connect Component를 기반으로 하는 웹 프레임워크
- 프로젝트에 필요한 라이브러리를 원하는대로 선택할 수 있어 유연한 개발 가능
- 사용자가 많아 오류가 났을때 혼자 삽질할 가능성이 적어진다...

## 내장모듈을 사용해서 웹서버 띄워보기
```javascript
const http = require('http');

http.createServer( (req, res) => {
    res.writeHead(200, {'Content-Type' : 'text/plain'}); // 문서 타입
    res.write('Hello Server');
    res.end();
}).listen(3000);
```
- index.js 파일에 작성 후 node index.js 명령어 입력
- localhost:3000을 들어가면 결과물이 보임
- request(URL접속, form전송) / response(텍스트, 이미지)

## http 상태코드
|상태코드|설명|
|--|--|
|1XX|조건부응답|
|2XX|응답성공|
|3XX|리다이렉션|
|4XX|요청오류(ex 404 Not Found)|
|5XX|서버오류|

## express로 웹서버 띄워보기
- npm install express 명령어를 사용하여 json에 express 의존성 추가 및 모듈 다운로드
```javascript
const express = require("express");

const app = express();
const port = 3000;

app.get("/", (req, res) => {
    res.send("hello express");
});

// get요청을 통해 localhost:3000/jinho에 jinho hi를 띄워라라는 요청을 함
app.get("/jinho", (req, res) => {
    res.send("jinho hi");
})

app.listen(port, () => {
    console.log("Express listening on port", port);
});
```

## nodemon설치
- node를 이용할때 내부 코드를 수정할 경우 서버를 내렸다가 다시 올려야 하는 번거로움이 있다.
- 이를 해결하기 위해 수정을 자동으로 감지하고 서버를 다시 띄워주는 nodemon!
- npm install nodemon 명령어를 이용하여 간편히 설치 가능

## Routing
- app.js
    ```javascript
    const express = require("express");

    const admin = require("./routes/admin");

    const app = express();
    const port = 3000;

    app.get("/", (req, res) => {
        res.send("hello express");
    });

    app.use("/admin", admin);

    app.listen(port, () => {
      console.log("Express listening on port", port);
    });
    ```

- routes/admin.js (admin과 관련된 url을 routes폴더를 만들어 따로 저장)
    ```javascript
    const express = require("express");
    const router = express.Router();

    // localhost:3000/admin
    router.get("/", (req, res) => {
        res.send("admin 이후 url");
    });

    // localhost:3000/admin/products
    router.get("/products", (req, res) => {
        res.send("products url");
    });

    // localhost:3000/admin/contacts
    router.get("/contacts", (req, res) => {
        res.send("contacts url");
    });

    module.exports = router;
    ```