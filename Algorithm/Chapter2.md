# **Chapter2 - 재귀**
---

## **2.1 재귀 알고리즘**
- 재귀(Recursion) : 문제에 대한 해결을 할 때 일부만 답하고 나머지는 또 다른 문제로 남겨두는 것
- 재귀 호출(Recursive Call) : 알고리즘이 자기 자신을 호출하는 것
    ```
    Alg sum(n)
    1.  if (n = 1)              {base case}
            return 1
        else                    {recursion}
            return n + sum(n-1)
    ```

- 재귀 케이스(recursive case) : 재귀호출은 반드시 원래 문제보다 작은 문제들을 대상으로 해야함
- 베이스 케이스(base case) : 부문제들이 작아지면 직접 해결

## **2.2 재귀의 작동원리**
- 재귀와 관련된 내부 처리는 컴퓨터 내부에서 자동 수행
- 대기중인 호출들은 시스템 Stack에 저장되었다가 꺼내짐

## **2.3 재귀의 기본 규칙**
1. 배이스 케이스: 항상 가져야 함 -> 마지막은 스스로 풀어야 함
2. 재귀의 진행 방향: 항상 베이스 케이스를 향하는 방향으로 진행
3. 정상 작동 가정

### 2.3.1 잘못 설계된 재귀
- sum1은 베이스 케이스가 없음
- sum2는 진행될수록 베이스 케이스에서 멀어짐
```
Alg sum1(n)
1. return n + sum1(n-1)

Alg sum2(n)
1. if (n = 1)                   {base case}
        return 1
    else                        {recursion}
        return n + sum2(n+1)
```

### 2.3.2 잘 설계된 재귀
- 직접재귀, 간접재귀: 본격적인 재귀 알고리즘은 분리하여 따로 작성하는 경우가 많음
```
Alg printDigits()                   {driver}
1. write("Enter a number")
2. n <- read()
3.  if (n < 0)                      {error check}
        write("Negative number!")
    else
        rPrintDigits(n)             {initial call}

Alg rPrintDigits(n)                 {recursive}
1.  if (n < 10)                     {base case}
        write(n)
    else                            {recursion}
        rPrintDigits(n/10)
        write(n%10)
```

## **2.4 응용 문제**

### **2.4.1 재귀적 곱하기와 나누기**
1. a와 b의 곱을 계산하는 재귀 알고리즘 product(a,b)
    ```
    Alg product(a,b)
        input positive integer a,b
        output a * b

    1.  if (b=1)                        {base case}
            return a
        else                            {recursion}
            return a + product(a, b-1) 
    ```

2. a를 b로 나눈 나머지를 계산하는 재귀 알고리즘 modulo(a,b)
    ```
    Alg modulo(a,b)
    input positive integer a,b
    output a % b

    1.  if (a < b)                  {base case}
            return a
        else                        {recursion}
            return modulo(a-b, b)
    ```

3. a를 b로 나눈 몫을 계산하는 재귀 알고리즘 quotient(a,b)
    ```
    Alg quotient(a,b)
    input positive integer a,b
    output a / b

    1.  if (a < b)                      {base case}
            return 0
        else                            {recursion}
            return 1 + qoutient(a-b, b)
    ```


### **2.4.2 하노이탑**
- 변수 지정
    1. n: 이동해야 할 원반 수
    2. from: 출발 말뚝
    3. aux: 보조 말뚝
    4. to: 목표 말뚝

```
Alg hanoi(n)
1. rHanoi(n,'A','B','C')                    {initial call}
2. return

Alg rHanoi(n, from, aux, to)                {recursive}
    input integer n, peg from, aux, to
    output move sequence

1.  if(n = 1)                               {base case}
        write("move from", from, "to", to)
        return
2.  rHanoi(n-1, from, to, aux)              {recursion}
3.  write("move from", from, "to", to)
4.  rHanoi(n-1, aux, from, to)              {recursion}
5.  return 
```