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


  ---

  ### Disjoint set과 Union-find 개념

  #### Disjoint Set의 개념

  - Disjoint Set이란
    서로 중복되지 않는 부분 집합들 로 나눠진 원소들에 대한 정보를 저장하고 조작하는 자료구조

  즉, 공통 원소가 없는, 즉 “상호 배타적” 인 부분 집합들로 나눠진 원소들에 대한 자료구조이다.
  Disjoint Set = 서로소 집합 자료구조

  

  #### Union-Find의 개념
  - Union-Find란
    Disjoint Set을 표현할 때 사용하는 알고리즘

  집합을 구현하는 데는 비트 벡터, 배열, 연결 리스트를 이용할 수 있으나 그 중 가장 효율적인 트리 구조 (아래 참고*)를 이용하여 구현한다.
  아래의 세 가지 연산을 이용하여 Disjoint Set을 표현한다.

  - Union-Find의 연산
    - make-set(x)
      - 초기화
        x를 유일한 원소로 하는 새로운 집합을 만든다.
    - union(x, y)
      - 합하기
        x가 속한 집합과 y가 속한 집합을 합친다. 즉, x와 y가 속한 두 집합을 합치는 연산
    - find(x)
      - 찾기
        x가 속한 집합의 대표값(루트 노드 값)을 반환한다. 즉, x가 어떤 집합에 속해 있는지 찾는 연산

  ---

  ## Union-Find 란?

  `Union-Find` 란 `Disjoint Set` 을 표현할 때 사용하는 독특한 형태의 자료구조로,

  ```cpp
  공통 원소가 없는, 즉 "상호 배타적" 인 부분 집합 들로 나눠진 원소들에 대한 정보를 저장하고 조작하는 자료구조
  ```

  입니다.

  위의 상황을 표현하기 위해서는 초기화 과정과 다음과 같은 두 가지 연산을 지원해야 하기 때문에, `Union-Find` 자료구조 라고 부르게 되었다고 합니다.

  ```
  Union-Find 지원 연산
  ```

  1. **초기화** : N 개의 원소가 각각의 집합에 포함되어 있도록 초기화 합니다.
  2. **Union (합치기) 연산** : 두 원소 a, b 가 주어질 때, 이들이 속한 두 집합을 하나로 합칩니다.
  3. **Find (찾기) 연산** : 어떤 원소 a 가 주어질 때, 이 원소가 속한 집합을 반환합니다.