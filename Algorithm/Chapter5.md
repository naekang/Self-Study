# **Chapter5 - 우선순위 큐**
---

## **5.1 우선순위 큐 ADT**
- 정렬에 자주 응용

### **5.1.1 우선순위 큐 ADT**
- 임의의 데이터 항목이 삽입되며, 일정한 순서에 의해 삭제되는 데이터구조
- 일반적인 큐와 비교했을 때 삽입과 삭제가 가능한 것은 동일하지만 일반적인 큐는 삽입 순서 그대로 삭제되고 우선순위 큐는 키 순서에 따라 삭제

### **5.1.2 우선순위 큐 응용**
- 정렬(Sort): 데이터원소들을 일정한 키 순서에 의해 다시 배치하는 것

### **5.1.3 우선순위 큐 ADT 메서드**
- 주요 메서드
    - `insertItem(k, e)`: 키 k인 원소 e를 큐에 삽입
    - `element removeMin()`

- 일반 메서드
    - `integer size()`
    - `boolean isEmpty()`

- 접근 메서드
    - `element minElement()`
    - `element minKey()`

- 예외
    - `emptyQueueException()`
    - `fullQueueException()`


## **5.2 우선순위 큐를 이용한 정렬**
```
Alg PQ-Sort(L)
    input list L
    output sorted list L

1. P <- empty priority queue
2. while (!L.isEmpty())
    e <- L.removeFirst()
    P.insertItem(e)
3. while (!P.isEmpty())
    e <- P.removeMin()
    L.addLast(e)
4. return 
```

1. 무순리스트 구현(unordered list)
   - 리스트에 임의 순서로 저장 
   - insertItem: O(1) / removeMin, minKey, minElement: O(n)
2. 순서리스트 구현(ordered list) 
   - 리스트에 키 순서로 저장
   - insertItem: O(n) / removeMin, minKey, minElement: O(1)


### **5.2.1 선택 정렬**
- 우선순위 큐가 무순리스트로 구현
- O(n^2)

### **5.2.2 삽입 정렬**
- 우선순위 큐가 순서리스트로 구현
- O(n^2)


## **5.3 제자리 정렬**
- 원래 리스트 자체를 위한 내부 공간 이외에 추가로 O(1) 크기의 외부 공간만을 사용한다면 제자리에서 수행한다고 함

### **5.3.1 제자리 선택 정렬**
- 원소들을 순차적으로 탐색하며 최소값의 위치를 바꿔 정렬

### **5.3.2 제자리 삽입 정렬**
- 원소들을 순차적으로 탐색하며 적절한 위치에 삽입하여 정렬


## **5.4 선택 정렬과 삽입 정렬 비교**

우선순위 큐|insertItem|removeItem|minKey,minElement|정렬방식
--|--|--|--|--
무순리스트|O(1)|O(n)|O(n)|선택 정렬
순서리스트|O(n)|O(1)|O(1)|삽입 정렬



참고 문헌 : [국형준, 알고리즘 원리와 응용, 21세기사](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9788984688100&orderClick=LET&Kc=)