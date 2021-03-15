# Sequelize 기본
---

## sequelize란
- ORM(Object-Relational Mapping) Nodejs로 mysql 또는 db를 제어할 수 있게 해줌
- ORM이란 객체와 관계형 데이터 베이스 관계를 매핑해주는 도구
- mysql 사용시 raw Query문을 사용하지 않고 쉽게 다룰 수 있도록 도와주는 라이브러리
- 웹용 엑셀!

## dotenv 설정
- Node.js로 개발을 진행하면서 전역으로 필요한 여러 정보들이 존재하는데 이때 환경변수들을 관리하기 편하게 하는 방법
- 설치방법
```
npm install dotenv
```
- 프로젝트에 .env.sample 파일 만들기
```
DATABASE = "데이터베이스명"
DB_USER = "아이디"
DB_PASSWORD = "패스워드"
DB_HOST = "DB호스트"
```
- 접근하고 싶을시 process.env.DB_USER 의 형식을 통해 접근 가능

## Database 생성
1. mysql 실행하기
    ```
    mysql.server start
    ```
2. mysql 접속하기
    ```
    mysql -u root -p
    ```
3. 데이터베이스 만들기
    ```sql
    CREATE DATABASE exercise;
    ```
4. 데이터베이스가 잘 만들어졌는지 확인
    ```sql
    SHOW DATABASES;
    ```

## DB 접속
1. sequelize 설치
    ```
    npm install sequelize
    ```
2. mysql2 설치
    ```
    npm install mysql2
    ```
3. .env 파일 내용 수정
4. models 폴더 생성 후 index.js 파일 만들기
    - 데이터베이스 sync하여 테이블 자동생성

## 모델 작성
1. 테이블 작성 -> models 폴더 안에 Products.js 파일 생성
    ```javascript
    const { sequelize } = require(".");

    module.exports = (sequelize, DataTypes) => {
        const Products = sequelize.define("Products", {
            id: { type: DataTypes.INTEGER, primartKey: true, autoIcrement: true },
            name: { type: DataTypes.STRING },
            price: { type: DataTypes.INTEGER },
            description: { type: DataTypes.TEXT },
        });
        return Products;
    };

    ```