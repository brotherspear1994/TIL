# swea

# 숫자카드

### 일자 20200804

#### 풀이

```python
import sys
sys.stdin = open("sample_input.txt", "r")

T = int(input())
for tc in range(1, T+1):
    N = int(input())
    ai = int(input())
    # print(ai)
    card_lst = []
    while ai != 0:
        card_lst.append(ai % 10)
        ai //= 10
    # print(card_lst)
    checknumber = [0] * 10
    # print(checknumber)
    for i in card_lst:
        checknumber[i] += 1
    # print("{} {}".format(tc, checknumber))
    max_num = 0
    index = 0
    for j in range(len(checknumber)):
        if checknumber[j] >= max_num:
            index = j
            max_num = checknumber[j]



        # print(checknumber[j])


    print("#{} {} {}".format(tc, index, max_num))
```

