# Chapter 2 - 자바스크립트란?
---

## 2.1 자바스크립트의 탄생
- 1995년 90%이상의 점유율을 자랑하던 넷스케이프 커뮤니케이션즈에서 경량 프로그래밍 언어 도입을 결정하고 '브렌덴 아이크'가 'Mocha'라는 이름으로 개발 -> 'Livescript'라는 이름을 거쳐 'Javascript'로 최종 명명되었다.

## 2.2 자바스크립트의 표준화
- 자바스크립트가 탄생하고나서 마이크로소프트는 파생버전인 JScript를 출시하였다.
- 이후 자사 브라우저에만 동작하는 기능들을 추가하는 등의 경쟁으로 '크로스 브라우징 이슈'가 발생하였고 결국 넷스케이프는 ECMA International에 자바스크립트 표준화를 요청하여 승인을 받는다.
- 꾸준한 업데이트로 2021년 작성시간 기준 ES11까지 나와있는 상태이다.

## 2.3 자바스크립트 성장의 역사
- 초기에는 HTML, CSS파일을 단순 렌더링 하는 수준

### 2.3.1 Ajax
- Javascript를 이용하여 서버와 브라우저가 비동기(Asynchronous)방식으로 데이터를 교환하는 기능
- 이전에는 html코드를 전송받아 전체를 렌더링 했기에 불필요한 통신이 생기고 순간적인 깜빡임 현상도 나타났다.
- Ajax는 필요한 부분에 한해 한정적인 렌더링을 실행한다.

### 2.3.2 jQuery
- DOM(Document Object Model)을 쉽게 제어하고 크로스 브라우징 이슈 해결

### 2.3.3 V8 자바스크립트 엔진
- 자바스크립트의 성능을 발휘할수 있는 빠른 엔진 탑재

### 2.3.4 Node.js
- V8 자바스크립트 엔진으로 빌드된 자바스크립트 런타임 환경
- 자바스크립트 엔진을 브라우저에서 독립
- 서버사이드 어플리케이션 개발에 주로 사용되며 모듈, 파일시스템, HTTP, 빌트인 API 제공
- 비동기 I/O 지원, 단일 스레드 이벤트 루프 기반 -> 요청 처리 성능이 좋음
- 자바스크립트는 크로스 플랫폼을 위한 가장 중요한 언어

### 2.3.5 SPA Framework
- Component based development 방법론을 기반으로한 SPA가 대중화 되면서 Vue.js, React, Angular 등 다양한 프레임워크 존재

## 2.4 자바스크립트와 ECMAScript
- ECMAScript는 자바스크립트 표준 사양인 ECMA-262를 말함 -> 핵심 문법 규정
- 자바스크립트는 ECMAScript뿐 아니라 클라이언트 사이드 Web API 등을 아우르는 개념

## 2.5 자바스크립트 특징
- 웹에서 동작하는 유일한 언어
- 컴파일러가 존재하지 않는 Interpreter Language
- 명령형, 함수형, 프로토타입 기반 객체지향 프로그래밍 지원 (class 개념은 ES6 이후 도입)

## 2.6 ES6 브라우저 지원 현황
- [ECMAScript지원현황](http://kangax.github.io/compat-table/es6/) 참고
- Babel과 같은 트랜스파일러를 이용하여 다운그레이드 가능