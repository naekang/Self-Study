# AWS의 기본
---

## AWS란
- 아마존에서 개발한 클라우드 컴퓨팅 플랫폼
- 가상 컴퓨터, 네트워크 인프라 등의 서비스 제공
- 

## 클라우드 컴퓨팅
- 실제 컴퓨터와 같은 리소스들을 네트워크 기반 형태로 제공하는 것
- 장점 : 비용 절감, 속도 개선, 빠른 설치 및 편한 관리

## AWS 설치 및 배포 방법(Mac 기준)
1. AWS에 들어가 기본 정보 및 해외 결제가 가능한 카드정보 입력
2. 계정 생성 후 프리티어 ubunu버전을 선택하여 인스턴스 생성
3. pem 생성 후 바탕화면에 저장하기
4. terminal을 열고 다음 명령어들을 순서대로 입력
    ```
    cd Desktop/ // pem 저장 디렉토리로 이동

    chmod 700 test.pem // 권한 수정

    ssh -i test.pem ubuntu@(퍼블릭 IPv4 DNS주소)
    ```
## Node.js 설치