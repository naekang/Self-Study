# **Chapter6 - 힙과 힙 정렬**
---

## **6.1 힙**
- 힙(heap)은 내부노드에 키를 저장하면서 두 가지 속성을 만족하는 이진트리
    1. 힙순서(heap-order): 모든 부모-자식 관계에서 부모노드의 키가 자식노드의 키보다 작거나 같도록 구성된 이진트리
    2. 완전 이진 트리(complete binary tree)로 구성

### **6.1.1 힙의 높이**
- n개의 키를 저장한 힙의 높이는 O(log n)


## **6.2 힙을 이용한 우선순위 큐 구현**
- 힙을 이용하여 우선순위 큐 ADT 구현 가능

### **6.2.1 힙에 삽입**
1. 삽입 노드 z, 새로운 마지막 노드 찾음
2. k를 z에 저장 후 z을 내부노드로 확장
3. 힙순서 속성 복구

```
Alg insertItem(k)
    input key k, node last
    output none

1. advanceLast()
2. z <- last
3. Set node z to k
4. expandExternal(z)
5. upHeap(z)
6. return
```

```
Alg upHeap(v)
    input node v
    output none

1. if (isRoot(v))
    return
2. if (key(v) >= key(parent(v)))
    return
3. swapElements(v, parent(v))
4. upHeap(parent(v))
```

- 힙이 연결트리로 구현된 경우 insertItem이 호출하는 expandExternal(z)는 트리 노드 삽입을 위한 구체적인 작업 수행
- 노드의 왼쪽과 오른쪽에 각각 동적메모리로부터 할당받은 외부노드 자식을 추가함으로써 노드 z를 내부노드로 확장
```
Alg expandExternal(z)
    input external node(z)
    output none

1. l <- getnode()
2. r <- getnode()
3. l.left <- ∅
4. l.right <- ∅
5. l.parent <- z
6. r.left <- ∅
7. r.right <- ∅
8. r.parent <- z
9. z.left <- l
10. z.right <- r
11. return 
```

### **6.2.2 힙으로부터 삭제**
1. 루트 키를 마지막 노드 w의 키로 대체
2. w와 그의 자식들을 잎으로 축소
3. 힙순서 속성 복구

```
Alg removeMin()
    input node last
    output key

1. k <- key(root())
2. w <- last
3. Set root to key(w)
4. retreatLast()
5. z <- rightChild(w)
6. reduceExternal(z)
7. downHeap(root())
8. return k
```

```
Alg downHeap(v)
    input node v whose left and right subtrees are heaps
    output a heap with root v

1. if(isExternal(leftChild(v)) & isExternal(rightChild(v)))
    return
2. smaller <- leftChild(v)
3. if (isInternal(rightChild(v)))
    if (key(rightChild(v)) < key(smaller))
        smaller <- rightChild(v)
4. if (key(v) <= key(smaller))
    return
5. swapElements(v, smaller)
6. downHeap(smaller)
```

```
Alg reduceExternal(z)
    input external node z
    output the node replacing the parent node of the removed node z

1. w <- z.parent
2. zs <- sibling(z)
3. if (isRoot(w))
    root <- zs
    zs.parent <- ∅
else
    g <- w.parent
    zs.parent <- g
    if (w = g.left)
        g.left <- zs
    else {w = g.right}
        g.right <- zs
4. putnode(z)
5. putnode(w)
6. return zs
```

### **6.2.3 마지막 노드 갱신**
- 힙에 대한 삭제, 삽입 모두 마지막 노드의 갱신을 필요로 함 


## **6.3 힙 구현과 성능**

힙 구현|size, isEmpty|isertItem,removeMin|minKey,minElement|advancedLast,retreatLast|공간소요
--|--|--|--|--|--
연결|O(1)|O(log n)|O(1)|O(log n)|O(n)
순차|O(1)|O(log n)|O(1)|O(1)|O(n)