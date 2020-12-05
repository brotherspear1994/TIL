# swea

# 구간합

### 일자 20200804

#### 풀이

```python
import sys
sys.stdin = open('sample_input.txt', 'r')

T = int(input())
for tc in range(1, T+1):
    N, M = map(int, input().split())
    ai = list(map(int, input().split()))
    # print(N, M)
    # print(ai)

    #출력
    lst = []
    for i in range(N-M+1):
        lst.append(sum(ai[i:i+M]))
    # print(lst)
    print('#{} {}'.format(tc, max(lst)-min(lst)))
```

- 특정 구간의 합을 for문과 인덱스 슬라이싱을 활용해 구해보았다.