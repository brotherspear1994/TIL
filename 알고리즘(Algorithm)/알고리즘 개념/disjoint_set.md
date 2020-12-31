# Union Find와 Disjoint_set(서로소 조합)

[TOC]

### 알고리즘 코드

```python
def make_set(x):
    p[x] = x

# find_set : x의 대표자를 리턴
# path compression 적용
# -> findset을 하면서 거쳑나 정점의 부모를 대표자로 설정
def find_set(x):
    if p[x] == x: return x
    else:
        X = find_set(p[x])
        p[x] = X
        return X

# union: x와 y가 속한 집합을 합침
# x와 y의 대표를 찾음
# x의 대표, y의 대표의 랭크를 비교
# 랭크에 따라 p[x] <- y, p[y] <- x 일지를 결정
def union(x,y):
    if rank[x] > rank[y]:
        p[find_set(y)] = find_set(x)
    else:
        if rank[x] < rank[y]:
            p[find_set(x)] = find_set(y)
        elif rank[x] == rank[y]:
            p[find_set(y)] = find_set(x)
            rank[x] += 1

N = 8
p = [0] * (N+1) # 각 정점의 부모를 저장
rank = [0] * (N+1) # 각 정점의 rank(서브트리의 깊이)

for i in range(1,N+1):
    make_set(i)

print(p)
union(1,2)
union(3,4)
union(5,6)
union(7,8)
union(2,4)
union(6,8)
# union(1,5)
print(p)
# a = find_set(5)
# print(a)
# print(p)
```

- 다수의 노드들 중에 연결된 노드를 찾거나 노드들을 합칠때 사용하는 알고리즘.

- 구현 과정에 대한 개념을 아래 간략히 정리해본다.

  - **Making new sets**

    - The *MakeSet* operation adds a new element. This element is placed into a new set containing only the new element, and the new set is added to the data structure. If the data structure is instead viewed as a partition of a set, then the *MakeSet* operation enlarges the set by adding the new element, and it extends the existing partition by putting the new element into a new subset containing only the new element.

  - **Finding set representatives**

    - The *Find* operation follows the chain of parent pointers from a specified query node *x* until it reaches a root element. This root element represents the set to which *x* belongs and may be *x* itself. *Find* returns the root element it reaches.
    - Performing a *Find* operation presents an important opportunity for improving the forest. The time in a *Find* operation is spent chasing parent pointers, so a flatter tree leads to faster *Find* operations. When a *Find* is executed, there is no faster way to reach the root than by following each parent pointer in succession. However, the parent pointers visited during this search can be updated to point closer to the root. Because every element visited on the way to a root is part of the same set, this does not change the sets stored in the forest. But it makes future *Find* operations faster, not only for the nodes between the query node and the root, but also for their descendants. This updating is an important part of the disjoint-set forest's amortized performance guarantee.

  - **Merging two sets**

    - The operation *Union*(*x*, *y*) replaces the set containing *x* and the set containing *y* with their union. *Union* first uses *Find* to determine the roots of the trees containing *x* and *y*. If the roots are the same, there is nothing more to do. Otherwise, the two trees must be merged. This is done by either setting the parent pointer of *x* to *y*, or setting the parent pointer of *y* to *x*.

    ​	