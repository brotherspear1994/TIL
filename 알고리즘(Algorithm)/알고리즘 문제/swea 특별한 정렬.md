# swea

# 특별한 정렬

### 일자 20200806

#### 풀이

```python
T = int(input())
for tc in range(1, T+1):
    N = int(input())
    ai = list(map(int, input().split()))
    result = []
    for i in range(10):
        max_num, min_num = ai[0], ai[0]
        idx = 0
        if i % 2 == 0:
            for j in range(len(ai)):
                if ai[j] >= max_num:
                    max_num = ai[j]
                    idx = j
        else:
            for j in range(len(ai)):
                if ai[j] <= min_num:
                    min_num = ai[j]
                    idx = j

        result.append(ai.pop(idx))

    print("#{} {}".format(tc, ' '.join(map(str, result))))
```



- 주어진 리스트에서 차례로 가장 큰값과 가장 작은값을 순차적으로 나열하게끔 하는 문제이다.

- for문을 이용해 원하는 값을 추출해 다시 재배열 시킬수있는지 묻는 문제였다.

- 매우 기초적인 for문 문제이다.

  