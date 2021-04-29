# 1. 그리디 알고리즘(Greedy Algorithm)
---

- 그리디 알고리즘은 가장 단순하지만 강력한 문제 해결 방법 -> 탐욕법
- 현재 상황에서 당장 가장 좋은 것만 고르는 방법
- 현재의 선택이 나중에 미칠 영향까지는 고려하지 않음
- 유형이 매우 다양하기 때문에 문제를 많이 접하면서 훈련하는 것을 추천

> 문제를 풀기위한 최소한의 아이디어를 생각해낼 수 있는 능력 요구 = 창의력

### 예제: 거스름돈
1. 문제 설명: 거스름돈으로 500원, 100원, 50원, 10원짜리 동전이 무한히 존재한다고 가정하고 거스름돈이 N원일 때 거슬러줘야 할 동전의 최소 개수 (단, N은 항상 10의 배수)

2. 내가 푼 코드
```python
import sys

N = int(sys.stdin.readline())

a = N // 500
N = N % 500
b = N // 100
N = N % 100
c = N // 50
N = N % 50
d = N // 10

print(a + b + c + d)
```

3. 문제 해설
- `가장 큰 화폐 단위부터` 돈을 거슬러 주는 것

4. 예시 답안
```python
import sys

N = int(sys.stdin.readline())
count = 0

# 큰 단위의 화폐부터 차레대로 확인
coin_types = [500, 100, 50, 10]

for coin in coin_types:
    count += N // coin  # 해당 화폐로 거슬러 줄 수 있는 동전의 개수 세기
    N %= coin

print(count)
```

5. 분석
- 화폐의 종류가 K개라고 할 때 위 코드의 시간복잡도는 O(K)
- 동전의 총 종류에만 영향을 받고 거슬러 줘야하는 금액의 크기와는 무관


### 그리디 알고리즘의 정당성
- 거스름돈 문제에서 화폐단위가 500, 400, 100 이였을 경우 위와 같은방법으로는 풀지 못함
- 대부분의 그리디 알고리즘의 문제에서는 문제를 풀기위한 최소한의 아이디어를 생각한 후 이 방법이 정당한것인지 확인하는 작업이 필요함


### 예제: 큰 수의 법칙
> 난이도: 하 | 풀이 시간:  30분 | 시간 제한: 1초 | 메모리 제한: 128MB | 기출: 2019 국가 교육기관 코딩 테스트

1. 문제 설명: 다양한 수로 이루어진 배열이 있을 때 주어진 수들을 M번 더하여 가장 큰 수를 만들기 (단, 배열의 특정한 번호에 해당하는 수가 연속해서 K번을 초과하여 더해질 수 없음)

2. 내가 푼 코드
```python
import sys

N, M, K = map(int, sys.stdin.readline().split())

num = sorted(list(map(int, sys.stdin.readline().split())))

num.reverse()

sum = 0

while True:
    for i in range(K):
        if M == 0:
            break
        else:
            sum += num[0]
            M -= 1
    if M == 0:
        break
    else:
        sum += num[1]
        M -= 1

print(sum)
```

3. 문제 해설
- 전형적인 그리디 알고리즘
- 입력값 중 가장 큰 수와 두번째로 큰 수만 이용하면 된다. 연속으로 더할 수 있는 수가 K번이기 때문에 가장 큰 수를 K번 더하고 두번째로 큰 수를 1번 더하는 연산 반복

4. 효율적인 문제 해결
- 아마 주어진 값이 더 크다면 시간초과가 발생할 것
- 반복되는 수열의 특징을 활용하여 해결 가능
```python
import sys

N, M, K = map(int, sys.stdin.readline().split())

data = list(map(int, sys.stdin.readline().split()))

data.sort()  # 입력받은 수 정렬
first = data[N-1]  # 가장 큰 수
second = data[N-2]  # 두번째로 큰 수

# 가장 큰 수가 더해지는 횟수 계산
count = int(M / (K + 1)) * K
count += M % (K + 1)

result = 0
result += (count) * first  # 가장 큰 수 더하기
result += (M-count) * second  # 두번째로 큰 수 더하기

print(result)
```


### 예제: 숫자 카드 게임
1. 문제 설명
    - 숫자가 쓰인 카드들이 N X N 형태로 놓여있다. 이때 N은 행의 개수, M은 열의 개수
    - 먼저 뽑고자 하는 카드가 포함되어있는 행을 선택
    - 그 다음 선택된 행에 포함된 카드들 중 가장 숫자가 낮은 카드를 뽑아야 한다.
    - 따라서 처음에 카드를 골라낼 행을 선택할 때, 이후에 해당 행에서 가장 숫자가 낮은 카드를 뽑을 것을 고려하여 최종적으로 가장 높은 숫자의 카드를 뽑을 수 있도록 전략을 세워야 한다.

2. 입력 조건
    - 첫째 줄에 숫자 카드들이 놓인 행의 개수 N과 열의 개수 M이 공백을 기준으로 하여 각각 자연수로 주어진다.
    - 둘째 줄부터 N개의 줄에 걸쳐 각 카드에 적힌 숫자가 주어진다. 각 숫자는 1 이상 10,000 이하의 자연수이다.

3. 출력 조건
    - 첫쨰 줄에 게임의 룰에 맞게 선택한 카드에 적힌 숫자를 출력한다.

4. 내가 푼 코드
```python
import sys
import time
start_time = time.time()

N, M = map(int, sys.stdin.readline().split())

new_num = []
for i in range(N):
    num = list(map(int, sys.stdin.readline().split()))
    new_num.append(min(num))

print(max(new_num))


end_time = time.time()
print("time: ", end_time - start_time)
# 예시1 : 13.402998924255371, 예시2 : 10.651026964187622
```

5. 문제 해설
    - 각 행마다 가장 작은 수를 찾은 뒤에 그 수 중에서 가장 큰 수 찾기

6. 답안 예시
```python
import sys
import time
start_time = time.time()

N, M = map(int, sys.stdin.readline().split())

# 버전 1 - min() 함수 응용
result = 0
for i in range(N):
    data = list(map(int, sys.stdin.readline().split()))
    min_value = min(data)
    result = max(result, min_value)

print(result)

end_time = time.time()
print("time: ", end_time - start_time)
# 예시1 : 9.07591700553894, 예시2 : 14.52392292022705
```

```python
import sys
import time
start_time = time.time()

N, M = map(int, sys.stdin.readline().split())

# 버전 2 - 2중 반복문 이용
result = 0
for i in range(N):
    data = list(map(int, sys.stdin.readline().split()))
    min_value = 10001
    for a in data:
        min_value = min(min_value, a)
    result = max(result, min_value)

print(result)

end_time = time.time()
print("time: ", end_time - start_time)
# 예시1 : 13.716645240783691, 예시2 : 12.932592153549194
```

### 예제: 1이 될 때까지
1. 문제 설명
    - 어떤 수 N이 1이 될 떄까지 두 과정 중 하나를 반복적으로 수행한다.
        1. N에서 1을 뺀다.
        2. N을 K로 나눈다.

2. 입력 조건
    - 첫째 줄에 N과 K가 공백으로 구분되며 각각 자연수로 주어진다. 이떄 N은 K보다 항상 크거나 같다.

3. 출력 조건
    - 첫째 줄에 N이 1이 될 때까지 1번 혹은 2번의 과정을 수행해야 하는 횟수의 최소값을 출력한다.

4. 내가 푼 코드
```python
import sys

N, K = map(int, sys.stdin.readline().split())

cnt = 0

while N >= K:
    if N % K == 0:
        N //= K
        cnt += 1
    else:
        N -= 1
        cnt += 1

while N > 1:
    N -= 1
    cnt += 1

print(cnt)
# 예시1 : 2.7745001316070557
```

5. 문제 해설
- 가장 많이 나누기 위한 방법을 찾아야 함
- 나누기를 우선적으로 생각
- 나누어지지 않는 경우 나누어질 때 까지 1을 빼면서 계산

6. 답안 에시
```python
import sys

N, K = map(int, sys.stdin.readline().split())

result = 0

while True:
    # N == K 로 나누어 떨어지는 수가 될때까지 1씩 빼기
    target = (N // K) * K
    result += (N - target)
    N = target
    # N이 K보다 작을 때 반복문 탈출
    if N < K:
        break
    result += 1
    N //= K

result += (N - 1)
print(result)
# 예시1 : 3.07131290435791
```


- 참고한 책: [이것이 취업을 위한 코딩테스트다 with 파이썬](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9791162243077&orderClick=LEa&Kc=)