# Node.js 기본
---

## Node.js란?
- Chrome V8 Javascript 엔진으로 빌드된 Javascript 런타임
- 웹 브라우저에서 쓰이는 자바스크립트를 서버에서 사용가능하게 만드는 것
- Ryan Lienhart Dahl이 개발

## Node.js 설치 (Mac OS 기준 - 본인이 설치한 방법)
1. terminal 또는 Iterm 2에 들어가서 Homebrew를 설치해준다.
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
- 맥에서 패키지들을 설치할 때 정말 유용함

2. Homebrew 명령어를 사용하여 node 설치
```
brew install node
```

3. 설치가 끝났다면 버전 확인하기
```
npm --version

node --version
```

- 이외에도 [nodejs 홈페이지](https://nodejs.org/ko/)에 들어가서 각자의 운영체제에 맞게 설치하는 방법도 있음

## Node.js를 위한 에디터
- 기본적으로 사용하던 vscode 사용할 예정

## Node.js 기본 실행
1. 에디터에서 index.js파일 만들고 코드 작성
```javascript
console.log('hello world');
```

2. 터미널에서 작업폴더 경로로 들어가서 Node 실행
```
node index.js
```

3. 터미널에 결과가 잘 찍히는지 확인

## Node.js 모듈 패턴
1. 내보낼때
    - Module.exports 변수
2. 불러올때
    - require 파일명

- 예시(실행할파일 : index.js, 내보낼파일: myvar.js)
    1. myvar.js
    ```javascript
    function Myvar() {
        this.name = "my instance";
    }
    module.exports = Myvar;
    ```

    2. index.js
    ```javascript
    const Myvar = require('./myvar');
    const setVar = new Myvar();
    
    console.log(setVar.name);
    // 실행 결과 : my instance
    ```

## npm(Nodejs Package Manager)
- Node.js로 만들어진 패키지를 관리해주는 툴
- homebrew를 통해 node를 설치하는 과정에서 이미 설치 완료
- npm init 명령어를 통해 package.json파일 생성

1. package.json파일 알아보기
    - JAVA Maven의 pom.xml과 비슷한 역할
    - dependencies : 프로젝트가 의존하는 패키지들의 이름과 버전 명시
    - devDependencies : 개발단계에서만 사용하는 패키지 명시
    - package name : 패키지 이름
    - version : 패키지 버전
    - entry point : 자바스크립트 실행파일 진입점 일반적으로 index.js또는 app.js 사용
    - test command : 코드 테스트할 때 입력할 명령어
    - git repository : 코드를 저장해둔 git 저장소 주소
    - keywords : npm 공식 홈페이지에서 패키지 쉽게 찾도록 도와줌
    - license : 해당 패키지의 라이선스