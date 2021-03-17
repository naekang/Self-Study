# 커널과의 첫 만남
---

## 커널 소스 구하기
    - [최신 코드 받기](https://www.kernel.org/)
    - Git
        1. git clone git://git.k[ernel.org/pub/scm/linux/kernel/git/torvalds/linux-2.6.git](http://ernel.org/pub/scm/linux/kernel/git/torvalds/linux-2.6.git) 의 명령어를 통해 리누스의 소스 트리 사본 받기
        2. git pull 명령어를 통해 최신 버전 커널로 업데이트
    - 커널 소스 설치
        - 압축 성능이 좋은 bzip2의 형태가 일반적임
        - $ tar xvjf linux-x.y.z.tar.bz2 의 명령어를 통해 압축 해제
        - 만약 GNU zip의 형태라면 $ tar xvzf linux-x.y.z.tar.gz 명령 실행
        - 하지만 git을 사용한다면 이 방법 사용할 필요가 없음
    - 패치
        - 점증적 패치 방법을 적용하면 간편하게 다른 버전으로 바꿀 수 있음
        - $ patch -p1 < ../patch-x.y.z

## 커널 소스 트리

    [커널 소스 최상위 디렉토리](https://www.notion.so/2f3927945bc4476e96dc76a8d2f305cb)

    [소스 트리 최상위 파일](https://www.notion.so/f7435850715b40efb0bcca5fcf599ba3)

## 커널 빌드
    - 커널 설정
        - 설정 옵션은 CONFIG로 시작함 ex) CONFIG_FEATURE, CONFIG_SMP
        - CONFIG_SMP: SMP 지원 여부 설정 가능
        - CONFIG_PREEMPT: 빌드 과정 제어 설정
        - $ make config → 옵션을 돌아가면서 yes, no, module중 어떤걸 선택할지 물어봄
    - 빌드 메시지 최소화
        - $ make > ../detritus 를 통해 make의 출력 리다이렉트
        - $ make > /dev/null 을 통해 불필요한 출력을 /dev/null로 보냄
    - 빌드 작업을 동시에 여러 개 실행
        - make 파일에는 빌드 과정을 병렬 작업으로 분리해 주는 기능이 있음
        - 커널 Makefile의 의존성 정보는 정확하므로 여러개의 작업을 생성해도 문제X
        - $ make -jn (n은 생성할 작업의 개수)
    - 새 커널 설치
        - 커널 빌드 후 커널 설치
        - 부트로더 사용법 참고

## 다른 성질의 야수
    - libc와 표준 헤더 파일을 사용할 수 없음
        - 커널은 표준 C라이브러리와 링크 X → 너무 크고 비효율적
        - libc함수의 상당수는 커널 안에 구현
        - printf() 함수 대신 printk() 함수 제공 → 형식화한 문자열을 커널 로그에 복사해 syslog 프로그램으로 처리
        - printk() 함수는 우선순위 플래그를 줄 수 있음
        - ex) printk(KERN_ERR "this is an error!\n"); → KERN_ERR와 출력 메시지 사이에 , 가 없음
    - GNU C
        - 리눅스 커널은 C로 프로그램 되어있으며 gcc를 통해 언어 확장 기능 제공
        - 인라인 함수
            - 함수 호출과 반환 시 발생하는 부가 비용 제거 가능
            - 컴파일러가 함수를 호출하는 코드와 호출되는 코드를 하나로 보고 최적화할 수 있어서 정교한 최적화 가능
            - 함수의 내용이 호출되는 자리에 복사되어 들어가기 때문에 코드의 크기가 커지고 메모리 사용량과 명령어 캐시 사용량이 늘어남
            - 함수 정의 부분에 static과 inline 지시어를 사용해 선언

            ```c
            static inline void wolf(unsigned long tail_size)
            ```

        - 인라인 어셈블러
            - 일반적인 C함수 안에 어셈블리 명령을 삽입
            - ex) x86프로세서의 rdtsc 인스트럭션을 실행해서 tscdml 내용을 받아오는 코드

            ```c
            unsigned int low, high;
            asm volatile ("rdtsc" : "=a" (low), "-d" (high));
            //low와 high에는 각각 64비트 tsc의 하위 32비트, 상위 32비트의 값이 들어감
            ```

        - 분기 구문 표시
            - 분기 시에 어느 쪽의 발생 가능성이 높은지를 이용해 최적화하는 내장 지시자가 있음

            ```c
            // 거의 실행되지 않는다고 표시
            if (unlikely(error)) {
            	/* ... */
            }
            ```

            ```c
            // 항상 실행될 것같음
            if (likely(success)) {
            	/* ... */
            }
            ```

    - 메모리 보호 없음
        - 사용자가 메모리 접근을 잘못하면 오류 탐지 후 프로세스를 종료시킬 수 있지만 커널이 잘못 접근한 경우는 제어가 쉽지 않음
        - 패이징 기능 사용 불가
    - 부동 소수점을 쉽게 사용할 수 없음
        - 커널이 잡다한 일을 해야하기 때문에 사용하지 않아야함
    - 작은 고정 크기의 스택
        - 커널의 스택은 크지 않고 동적 확장도 불가능
    - 동기화와 동시성
        - 커널은 경쟁상태에 놓이기 쉬우며 공유 자원에 대한 동시 접근을 허용해야하기 때문에 동기화를 필요로함
        - 리눅스는 선점형 멀티태스킹 운영체제 → 프로세스 스케줄러에 의해 실행 순서 조정
        - 대칭형 다중 프로세서(SMP) 지원 →
        - 현재 실행 코드와 상관없이 비동기식 인터럽트가 발생함 → 적절한 보호 장치가 없을 경우 자원 사용 도중에 인터럽트가 발생하고 핸들러에서 같은 자원에 접근하는 상황이 발생함
        - 선점형 → 접근하는 커널 코드가 실행 중인 커널 코드 선점하는 일이 발생할 수도 있음

        > spinlock이나 semaphore를 이용하여 해결 가능

    - 이식성의 중요성
        - 리눅스는 이식성이 좋으며 그 특성을 유지해야함
- 결론