# **Chapter1 - 알고리즘 분석**

## **1.1 실행시간**

- 알고리즘(Algorithm) : 주어진 문제를 일정 시간내에 해결하는 단계적 절차

- 자료구조(Data Structure) : 데이터를 효율적으로 관리하기 위한 구조

- **좋은** 알고리즘 : 실행 시간이 짧고 메모리를 적게 요구하는 알고리즘

### **1.1.1 평균 실행 시간과 최악 실행 시간**

- 실행 시간의 종류 

  1. 최선 실행 시간(best-case running time)

  2. 평균 실행 시간(average-case running time)

  3. 최악 실행 시간(worst-case running time) : 분석이 용이하고 유용성을 평가하는 가장 결정적인 요소

### **1.1.2 실행 시간 구하기**

1. 실험적 방법

   - 실제 알고리즘을 구현하고 입력 값을 다양화 하며 측정하는 방법

   - 모든 데이터를 입력할 수는 없기에 정확성이 떨어짐

   - 알고리즘을 비교하기 위한 변인통제가 현실적으로 어려움

   - 알고리즘을 직접 구현한 후 비교하는 것은 시간이나 비용측면에서 효율성이 떨어짐

2. 이론적 방법

   - 모든 입력 가능성 고려 가능

   - 변인통제의 어려움도 해결 가능

   - 의사코드를 이용하기 때문에 부담이 줄어들게 됨

## **1.2 의사코드(Pseudo-code)**

- 알고리즘을 설명하기 위해 상세하게 구현하는 것이 아닌 기본 문법을 사용하여 간략하고 구조적으로 기술한 것

- 배열 A에서 최대값을 찾기 위한 의사코드의 예시
    ```c
    Alg arrayMax(A, n)
        input array A of n integer
        output maximum element of A

    1. currentMax <- A[0]
    2. for i <- 1 to n-1
        if (A[i]>currentMax)
            currentMax <- A[i]
    3. return currentMax
    ```

### **의사코드 문법**
1. 연산(arithmetic)
    - <-            {치환}
    - =, <, >, ≤, ≥ {관계 연산자}
    - &, ||, !      {논리 연산자}
    - S < n^2       {첨자 등 수학적 표현 허용}

2. 제어(control)
    - if(exp) ...
      [elseif (exp) ...]*               {0회 이상 중첩 elseif절 가능}
      [else]                            {else절 생략 가능}
    - for var <- exp1 to|downto exp2    {var의 값이 exp1에서 exp2에 이를때까지 1씩 증가(감소)하며 0회 이상 반복}
    - for each var ∈ exp                {집합 exp이 포함하는 각 원소 var에 대해 0회 이상 반복}
    - while (exp)                       {exp이 참인 동안 0회 이상 반복}
    - do ... while(exp)                 {exp이 참인 동안 1회 이상 반복}

3. 메소드(Method) 정의, 반환, 호출
    - Alg method([arg [, arg]*])        {메소드(알고리즘) 정의}
    - return [exp [, exp]]              {메소드(알고리즘)로부터의 반환}
    - method([arg [, arg]*])            {메소드(알고리즘) 호출}

4. 주석(comments)
    - input ...             {메소드(알고리즘)의 입력 명세}
    - output ...      
    -       {메소드(알고리즘)의 출력 명세}
    - {This is a comment}   {코드 내 주석}

5. 범위 지정
    - 들여쓰기(indentation)


## **1.3 실행시간 측정과 표기**

### **1.3.1 임의 접근 기계 모델**
- 이론적인 방법으로 실행시간을 구하기 위해 가상의 기계인 RAM을 정의
- CPU + 무제한의 메모리 셀
- 셀 접근 시 동일한 시간단위 소요

### **1.3.2 원시작업**
- 알고리즘에 의해 수행되는 기본적인 계산들로 의사코드로 표현 가능
    ```
    Alg arrayMax(A, n)
        input array A of n integer
        output maximum element of A
                                    {operation count}
    1. currentMax <- A[0]           {IND, ASS 2}
    2. for i <- 1 to n-1            {ASS, EXP 1+n}
        if (A[i]>currentMax)        {IND, EXP 2(n-1)}
            currentMax <- A[i]      {IND, ASS 2(n-1)}
            {increment counter i}   {EXP, ASS 2(n-1)}
    3. return currentMax            {RET      1}
                                    {Total    7n-2}
    ```

### **1.3.3 실행시간 측정**
- arrayMax의 최악 실행 시간 = 7n-2
- a(7n-2) ≤ T(n) ≤ b(7n-2)

### **1.3.4 실행시간 표기**
- __Big-Oh__ 표기법 : 함수 증가율의 상한을 나타냄
- 계산 요령
    1. f(n)이 상수면 f(n) = O(c) 또는 O(1)
    2. f(n)이 다항식이면 f(n) = O(n^d)
    3. 최소한의 함수계열 사용
    4. 해당 함수계열 중 가장 단순한 표현 사용

### **1.3.5 점근분석(asymptotic analysis)**
1. 최악의 원시작업 수행 횟수를 입력크기의 함수로 구함   
2. 이 함수를 big-Oh 표기법으로 나타냄

### **1.3.6 분석의 지름길**
1. 다중의 원시작업
    - 하나의 식에 나타나는 여러 개의 원시작업을 하나로 계산  


2. 반복문
    - 반복문의 실행시간 × 반복 횟수  


3. 중첩 반복문
    - 반복문의 실행시간 × ∏ 각 반복문의 크기  


4. 연속문 
    - 각 문의 실행시간 합산 후 최대값 선택

## **1.4 전형적인 함수들의 증가율**

[https://velog.io/@qksud14/Algorithm-BigO](빅오 표기법에 대해 잘 정리해주신 분의 블로그 참조)





참고 서적 : 국형준, 알고리즘 원리와 응용, 21세기사

[www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9788984688100&orderClick=LAG&Kc=](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9788984688100&orderClick=LAG&Kc=)