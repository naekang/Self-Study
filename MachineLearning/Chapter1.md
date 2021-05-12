# Chapter1 - 파이썬 기반의 머신러닝 생태계 이해
---

## 01 머신러닝의 개념
- 머신러닝(Machine Learning): Application을 수정하지 않고 데이터를 기반으로 패턴을 학습하고 결과를 예측하는 알고리즘
- 데이터를 기반으로 통계적인 신뢰도를 강화하고 예측 오류를 최소화하기 위해 다양한 수학적 기법을 적용하여 패턴을 스스로 인지하고 신뢰도있는 결과를 도출

#### 머신러닝의 분류
- 지도학습(Supervised Learning)
  - 분류
  - 회귀
  - 추천 시스템
  - 시각 / 음성 감지 / 인지
  - 텍스트 분석, NLP

- 비지도학습(Un-supervised Learning)
  - 클러스터링
  - 차원 축소
  - 강화학습

#### 데이터 전쟁
- 머신러닝의 가장 큰 단점: 데이터에 매우 의존적
- 최적의 머신러닝 알고리즘 + 다양하고 광대한 데이터

#### 파이썬 vs R 기반 머신러닝 비교
- 파이썬
  - 직관적인 문법 + 객체지향 + 함수형
  - `소리 없이 프로그래밍 세계를 점령하는 언어`
  - 뛰어난 확장성, 유연성, 호환성
  - 많은 딥러닝 프레임워크 존재 ex) TensorFlow, Keras, PyTorch

- R
  - 통계 전용 프로그램 언어
  - 많은 통게 패키지 보유


## 02 파이썬 머신러닝 생태계를 구성하는 주요 패키지
- 머신러닝 패키지
  - Scikit-Learn: 데이터 마이닝 기반 머신러닝에서 독보적인 위치

- 행렬/선형대수/통계 패키지
  - Numpy: 행렬과 선형대수를 다루는 대표적인 패키지
  - SciPy: 자연과학과 통계를 위한 패키지 제공

- 데이터 핸들링
  - Pandas: 2차원 데이터 처리에 특화, Matplotlib를 호출하여 시각화 기능 제공

- 시각화
  - Matplotlib: 세분화된 API로 익히기 번거로움
  - Seaborn: Matplotlib의 단점을 해결하기 위한 패키지

- Jupyter Notebook
  - 아이파이썬 지원 툴
  - 필기하듯 코드 단위로 설명을 적고 코드를 수행하여 결과를 직관적으로 볼 수 있음

#### 파이썬 머신러닝을 위한 S/W 설치
- 맥OS 기반 설치 방법

1. Anaconda 설치
    - [Anaconda 공식 사이트](https://www.anaconda.com/products/individual#Downloads)에 접속하여 설치 프로그램 다운로드
    - 설치가 잘 되었는지 확인하고 업데이트 진행
        ```
        ### 아나콘다 버전 확인
        conda --version

        ### 아나콘다 최신버전 업데이트 
        conda update conda
        ```
    - 설치에 오류가 있는 경우 환경변수 설정
        - 각자의 쉘에 맞게 ~/.zshrc 또는 ~/.bash_profile에 들어가 다음 내용 추가
        ```
        export PATH="/opt/anaconda3/bin:$PATH"
        ```
        - 다음 명령어를 통해 프로파일 업데이트
        ```
        source ~/.zshrc
        ```

2. Jupyter Notebook 설치
    - terminal 또는 iterm2를 열고 pip 최신버전 업데이트
    ```
    pip3 install --upgrade pip
    ```
    - 주피터 노트북 설치
    ```
    pip3 install jupyter
    ```
    - 주파터 노트북 실행
    ```
    jupyter notebook
    ```

3. Microsoft Visual Studio 설치
    - [공식홈페이지](https://visualstudio.microsoft.com/ko/downloads/)에 접속하여 각자의 환경에 맞게 설치

4. VSCode 에서 Jupyter Notebook 사용하기
    - python extension 설치
    - cmd + shift + P 를 통해 명령 팔레트 실행
    - Create New Blank Jupyter Notebook 실행
    - 변수 내용, 타입등을 print 출력 없이 확인 가능!

## 03 넘파이(Numpy)
- Numerical Python
- 선형대수 기반 프로그램 지원
- 파이썬 언어 자체의 느린 속도 문제를 해결하기 위해 C/C++ 기반의 코드를 작성하고 이를 넘파이에서 호출

#### Numpy ndarray 개요
```python
### numpy를 호출하고 np 약어로 표현
import numpy as np
```

- 넘파이 기반의 데이터 타입: ndarray
- array()함수: 다양한 인자를 ndarray 형태로 변환 shape 변수를 통해 크기를 알 수 있음
```python
array1 = np.array([1,2,3])
print('array1 type:', type(array1))
print('array1 array 형태:', array1.shape)

array2 = np.array([[1,2,3], [2,3,4]])
print('array2 type:', type(array2))
print('array2 array 형태:', array2.shape)

array3 = np.array([[1,2,3]])
print('array3 type:', type(array3))
print('array3 array 형태:', array3.shape)

print('array1: {:0}차원, array2: {:1}차원, array3: {:2}차원'.format(array1.ndim, array2.ndim, array3.ndim))
```
결과화면
```
array1 type: <class 'numpy.ndarray'>
array1 array 형태: (3,)
array2 type: <class 'numpy.ndarray'>
array2 array 형태: (2, 3)
array3 type: <class 'numpy.ndarray'>
array3 array 형태: (1, 3)
array1: 1차원, array2: 2차원, array3:  2차원
```

#### ndarray의 데이터 타입
- 숫자, 문자열, 불 값 모두 가능
- 내부 데이터 타입은 같은 데이터 타입만 가능
- `.dtype`을 통해 확인 가능
- 다른 데이터 타입이 있을 경우 더 큰 데이터 타입으로 형 변환 일괄 적용
    ```python
    list3 = [1,2,3.0]
    array3 = np.array(list3)
    print(array3.dtype)
    ```

    ```
    float64
    ```

- `astype()`메서드를 이용하여 원하는 타입 지정 가능

#### ndarray를 편리하게 생성하기 - arange, zeros, ones
- 특정 크기와 차원을 가진 ndarray를 연속값이나 0 또는 1로 초기화할 경우가 있을 떄
- 0으로 초기화 하기
```python
sequence_array = np.arange(10)
print(sequence_array)
print(sequence_array.dtype, sequence_array.shape)
```

```
[0 1 2 3 4 5 6 7 8 9]
int64 (10,)
```

- 1로 초기화 하기
```python
zero_array = np.zeros((3,2), dtype='int32')
print(zero_array)
print(zero_array.dtype, zero_array.shape)

one_array = np.ones((3,2))
print(one_array)
print(one_array.dtype, one_array.shape)
```

```
[[0 0]
 [0 0]
 [0 0]]
int32 (3, 2)
[[1. 1.]
 [1. 1.]
 [1. 1.]]
float64 (3, 2)
```

#### ndarray의 차원과 크기를 변경하는 reshape()
- `reshape()`메서드를 이용하여 특정 차원 및 크기로 변환 가능
```python
array1 = np.arange(10)
print('array1:\n', array1)

array2 = array1.reshape(2, 5)
print('array2:\n', array2)

array3 = array1.reshape(5, 2)
print('array3:\n', array3)
```

```
array1:
 [0 1 2 3 4 5 6 7 8 9]
array2:
 [[0 1 2 3 4]
 [5 6 7 8 9]]
array3:
 [[0 1]
 [2 3]
 [4 5]
 [6 7]
 [8 9]]
```

- -1을 인자로 사용하면 ndarray와 호환되는 새로운 shape로 변환
- `tolist()`메서드를 이용하여 리스트 자료형으로 변환 가능

#### 넘파이의 ndarray의 데이터 세트 선택하기 - 인덱싱(Indexing)
1. 특정 데이터만 추출 - 원하는 인덱스 값 지정
2. 슬라이싱(Slicing) - 연속된 인덱스상 ndarray 추출
3. 팬시 인덱싱(Fancy Indexing) - 일정한 인덱싱 집합을 리스트 또는 ndarray 형태로 지정해 해당 위치에 있는 데이터의 ndarray 반환
4. 불린 인덱싱(Boolean Indexing) - 특정 조건에 해당하는지 여부를 True/False 값을 기반으로 True에 해당하는 인덱싱 데이터 반환

##### 단일 값 추출
- 1차원 ndarray에서 한 개의 데이터 추출
  ```python
  array1 = np.arange(1, 10)
  print(array1)

  value = array1[2]
  print(value)
  print(type(value))
  ```

  ```
  [1 2 3 4 5 6 7 8 9]
  3
  <class 'numpy.int64'>
  ```