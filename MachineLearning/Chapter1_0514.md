# Chapter1 - 파이썬 기반의 머신러닝 생태계 이해 #2
---

#### 선형대수 연산 - 행렬 내적과 전치 행렬 구하기

##### 행렬 내적(행렬 곱)
- np.dot()을 이용해 계산 가능
    ```python
    A = np.array([[1,2,3],[4,5,6]])
    B = np.array([[7,8],[9,10],[11,12]])

    dot_product = np.dot(A, B)
    print('행렬 내적 결과: \n', dot_product)
    ```

    ```
    행렬 내적 결과: 
    [[ 58  64]
    [139 154]]
    ```

##### 전치 행렬
- A^T 행렬 구하기
    ```python
    A = np.array([[1,2],[3,4]])
    transpose_mat = np.transpose(A)
    print('A의 전치행렬:\n', transpose_mat)
    ```

    ```
    A의 전치행렬:
    [[1 3]
    [2 4]]
    ```

## 04 데이터 핸들링 - 판다스
- 고수준 API 제공
- 핵심 객체: DataFrame