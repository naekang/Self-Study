# Chapter3 - 자바스크립트 개발 환경과 실행 방법
---

## 3.1 자바스크립트 실행 환경
- 브라우저, Node.js환경은 자바스크립트 엔진을 내장하고 있어 어디든 실행 가능
- 브라우저 - HTML, CSS, JS를 화면에 렌더링 하는게 목적, 파일 생성 및 수정 파일 시스템 미제공
- Node.js - 브라우저 외부에서 JS실행 환경제공이 목적, DOM API 미제공

## 3.2 웹 브라우저
- V8엔진을 탑재한 크롬 브라우저를 기본으로 사용

### 3.2.1 개발자 도구
- F12 단축키를 사용하여 들어갈 수 있음
- 개발자 도구 목록
    패널|설명
    --|--
    Elements|DOM, CSS를 편집하여 렌더링된 뷰 확인가능
    Console|에러 확인 및 console.log 메서드 실행결과 확인 가능
    Sources|로딩된 웹페이지의 자바스크립트 코드 디버깅
    Network|웹페이지에 요청된 네트워크 요청 정보 확인
    Application|웹 스토리지, 세선, 쿠키 확인 관리

### 3.2.2 콘솔
- 에러가 났을때 가장 먼저 확인해봐야 함
- REPL(Read Eval Print Loop) 환경으로 사용가능

### 3.2.4 디버깅
- Sources 탭에 있는 빨긴 밑줄을 확인하며 수정 가능
- 중단점 활용하여 디버깅 모드 실행
- [Tools for Web Developers: 콘솔 사용](https://developers.google.com/web/tools/chrome-devtools/console)
- [Tools for Web Developers: Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/javascript)

## 3.3 Node.js
- Node.js와 npm 필요

### 3.3.1 Node.js와 npm 소개
- npm(node package manager) : Node.js에서 사용할 수 있는 모듈들을 패키지화하여 저장해둠

### 3.3.2 Node.js 설치
- [Node.js 공식 홈페이지](https://nodejs.org/ko/)
- LTS(Long Term Support) -> 장기적으로 안정된 지원 보장
- Current -> 가장 최신버전(beta버전 같은 느낌)
- 다운 받아서 설치 후 다음 명령어로 버전 확인
    ```
    node -v
    npm -v
    ```

### 3.3.3 Node.js REPL
- terminal 실행 후 node 명령어를 입력하면 프롬프트가 >로 변경되며 자바스크립트 코드 실행 가능
- ctrl + c 두번 입력하여 종료