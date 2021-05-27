# Chapter3 - 영어 단어 선택과 외래어 표기법
---

## 비슷한 듯 다른 듯, 단어 선택
- 반대: show vs hide, header vs footer, under vs over, import vs export
- 비슷: stop(잠시 중단, 언제든 재시작 가능), end(완전히 중단, 재시작 가능성 없음), finish(재시작 고려할 필요 없음), pause(아주 잠시 일시적 중단), suspend(다음 단계 시작을 중단), hold(의도가 있어서 중단)
    ```java
    stopUserRegister(); // 사용자 등록을 잠시 중단 
    // 재개하려면 startUserRegister()이나 restartUserRegister() 사용

    endUserRegister(); // 사용자 등록 종료
    // 사용자 등록을 새롭게 시작하려면 beginUserRegister()

    finishUserRegister(); // 사용자 등록을 완전히 종료
    // 다시 사용자 등록을 요청하면 에러 발생해야함
    ```

- get: 값을 돌려받아서 반환하는 함수, return: 함수 안에서 제어
- 검색에 무게가 실리면 retrieve 사용, acquire은 독점, fetch는 현재 값을 가리키는 포인터가 다음 값으로 이동한 것을 가져옴

- set: 값을 변경하거나 설정하는 함수, init은 초기화
- register는 정해진 틀에 값을 넣기, create는 정해진 틀이 없음
- parameter: 변수, argument: 전달 인자, attribute: HTML안에서 속성을 넣을 때, property: HTML DOM에서
- must: 필수 요구 사항, should: 권고 사항

- 정확성 + 일관성 + 개연성

## 외산 제품 표기와 외래어 표기법
- 이미 굳어진 외래어는 관용을 존중하되, 그 범위와 용례는 따로 정함
- [국립국어원 외래어 표기 용례 찾기](https://kornorms.korean.go.kr/m/m_exampleList.do)
- [한글라이즈](https://hangulize.org/)


참고문헌: [개발자의 글쓰기](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9791158391744&orderClick=LAG&Kc=#N)