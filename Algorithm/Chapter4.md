# **Chapter4 - 기본 추상자료형**
---

## **4.1 리스트 ADT**

### **4.1.1 추상자료형이란**
- ADT(Abstract Data Type): 인간이 데이터를 다루는 관점에서 데이터구조를 명세한 것
    - 다루는 데이터
    - 데이터에 대한 작업들
    - 발생 가능한 에러상황들

### **4.1.2 리스트ADT**
- 연속적인 임의 개체들 모델링

### **4.1.3 리스트 ADT 메소드**
- 일반 메소드
    - `integer size()`: 원소 수 반환
    - `boolean isEmpty()`: 비어있는지 확인
    - `iterator elements()`: 원소 전체 반환

- 접근 메소드
    - `element get(r)`: r에 저장된 원소 반환

- 갱신 메소드
    - `element set(r, e)`
    - `add(r, e)`
    - `addFirst(e)`
    - `addLast(e)`
    - `element remove(r)`
    - `element removeFirst()`
    - `element removeLast()`

- 예외
    - `invalidRankException()`
    - `fullListException`
    - `emptyListException`

### **4.1.4 리스트 ADT 구현과 성능**
- add, remove -> O(n)
- size, isEmpty, get, set -> O(1)
- 탐색 시간은 빠름 -> O(1)


## **4.2 집합 ADT**

### **4.2.1 집합 ADT**
- 중복이 없는 유일한 개체를 담음, unordered

### **4.2.2 집합 ADT 메소드**
- `set union(B)`: 합집합
- `set intersect(B)`: 교집합
- `set substract(B)`: 차집합

- 일반 메소드
    - `integer size()`: 집합의 원소 수
    - `boolean isEmpty()`: 집합이 비어있는지 유무
    - `iterator elements()`: 집합의 전체 원소 반환

- 질의 메소드
    - `boolean member(x)`: 개체 x가 집합의 원소인지 여부
    - `boolean subset(B)`: 부분집합인지 여부

- 갱신 메소드
    - `addElem(x)`: 원소 x추가
    - `removeElem(x)`: 원소 x삭제

### **4.2.3 집합 ADT 구현과 성능**
- 배열에 의한 구현
- 연결리스트에 의한 구현: 각 노드는 하나의 집합 원소 표현


## **4.3 스택 ADT**

### **4.3.1 스택 ADT**
- 후입선출(LIFO)의 순서를 따르는 추상 데이터 구조

### **4.3.2 스택 ADT 메소드**
- 주요 메소드
    - `push(e)`: 원소 e 삽입
    - `element pop()`: 가장 나중에 삽입된 원소 삭제하여 반환

- 보조 메소드
    - `element top()`: 가장 나중에 삽입된 원소를 삭제하지 않고 반환
    - `integer size()`: 저장된 원소 수 반환
    - `boolean isEmpty()`: 스택이 비어있는지 여부
    - `iterator element`: 스택 원소 전체 반환

- 예외
    - `emptyStackException()`: 비어있는 스택에 pop이나 top을 실행할 때
    - `fullStackException()`

### **4.3.3 스택 ADT 구현과 성능**
- 순차 스택(Sequential Stack)
- 배열을 이용한 방식
- 연결리스트를 이용한 방식: 동적 메모리 허용 한도내에서 노드 자유롭게 할당 가능


## **4.4 큐 ADT**

### ** 4.4.1 큐 ADT
- 선입선출(FIFO)의 순서를 따르는 추상 데이터 구조

### **4.4.2 큐 ADT 메소드
- 주요 메소드
    - `enqueue(e)`: 큐의 rear에 e 삽입
    - `element dequeue()`: 큐의 front에서 원소 삭제 반환

- 보조 메소드
    - `element front()`: 큐의 front의 원소를 삭제하지 않고 반환
    - `integer size()`
    - `boolean isEmpty()`
    - `iterator elements()`

- 예외
    - `emptyQueueException()`
    - `fullQueueException()`

### **4.4.3 큐 ADT 구현과 성능**
- 배열을 이용한 방식: 순차큐는 비효율적, 원형큐는 rear과 front를 사용하여 구현
- 연결리스트를 이용한 방식: 연결큐(Linked Queue)


## **4.5 트리 ADT**

### **4.5.1 트리 ADT**
- 계층적으로 추상화한 데이터 구조
- 자식 원소와 부모 원소를 가짐

###  **4.5.2 트리 용어***
1. 노드(Node): 데이터 원소
2. 간선(Edge): 노드 사이의 연결(부모, 자식 관계)
3. 루트(Root): 트리 맨 위의 부모가 없는 노드
4. 내부노드(Internal Node): 적어도 한 개의 자식을 가진 노드
5. 외부노드(External Node, Leaf): 자식이 없는 노드
6. 조상(Ancestor): 직계 상위 노드들
7. 자손(Descendant): 직계 하위 노드들
8. 형제(Sibilings): 같은 부모를 가진 노드들
9. 경로(Path): 조상 또는 자손을 따라 이어진 Node Sequence
10. 경로 길이(Path Length): 경로 내 Edge 수
11. 노드 깊이(Depth): 루트부터 노드까지 유일한 경로 길이
12. 노드 높이(Height): 외부노드에 이르는 가장 긴 경로 길이
13. 트리 높이(Height of a tree): 루트의 높이

### **4.5.3 트리 ADT 메소드**
- 일반 메소드
    - `boolean isEmpty()`
    - `integer size()`

- 접근 메소드
    - `node root()`
    - `node parent(v)`
    - `node children(v)`
    - `element element(v)`

- 질의 메소드
    - `boolean isInternal(v)`
    - `boolean isExternal(v)`
    - `boolean isRoot(v)`

- 갱신 메소드
    - `swapElements(v, w)`
    - `element setElement(v, e)`

- 예외
    - `invalidNodeException()`

- 깊이의 재귀적 정의
    1. 만약 v가 root라면 깊이는 0
    2. 그렇지 않다면 깊이는 부모의 깊이 +1

- 높이의 재귀적 정의
    1. v가 외부노드이면 높이는 0
    2. 그렇지 않다면 높이는 v의 자식들 중 최대 높이 +1

- 순회(traversal)
    1. 선위 순회(Preorder Traversal): VLR
    2. 후위 순회(Postorder Traversal): LRV
    3. 중위 순회(Inorder Traversal): LVR

### **4.5.4 이진트리 ADT**
- 순서트리 모델링
- 왼쪽, 오른쪽 자식 둘 다 가지면 적정 이진트리
- 완전 이진트리