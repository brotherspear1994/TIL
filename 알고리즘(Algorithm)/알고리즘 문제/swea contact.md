# swea

# contact

### 일자 20200903

### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV15B1cKAKwCFAYD&categoryId=AV15B1cKAKwCFAYD&categoryType=CODE)



### 풀이

```python
def search(startR):
    Q = []
    Q.append(startR)
    visited[startR] = 1
    while Q:
        R = Q.pop(0)
        for w in range(101):
            if Graph[R][w] and visited[w] == 0:
                Q.append(w)
                visited[w] = 1
                distance[w] = distance[R]+1
    Q.clear()
    return

for tc in range(1,11):
    Data_len, start = map(int,input().split())
    Data = list(map(int,input().split()))
    Graph = [[0 for _ in range(101)] for _ in range(101)]
    for i in range(Data_len//2):
        s, e = Data[i*2], Data[i*2+1]
        Graph[s][e] = 1
    # for row in Graph:
    #     print(row)
    # print()
    visited = [0]*101
    distance = [0]*101
    search(start)
    Max = 0
    MaxIdx = 0
    for idx in range(101):
        if Max <= distance[idx]:
            Max = distance[idx]
            MaxIdx = idx
    print("#{} {}".format(tc, MaxIdx))
```

- 노드의 거리, 미로의 거리와 매우 유사한 문제이다.
- 해당 문제는 BFS 스택을 이용해 문제에서 주어진 조건에 맞게 답을 출력해내면 된다.