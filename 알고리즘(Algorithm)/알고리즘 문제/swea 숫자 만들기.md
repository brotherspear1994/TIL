# swea

# 숫자 만들기

### 일자 20201030

### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AWIeRZV6kBUDFAVH&categoryId=AWIeRZV6kBUDFAVH&categoryType=CODE)

#### 풀이

```python
import sys; sys.stdin = open("숫자만들기.txt", "r")

def go(k,acc):
    global max_ans; global min_ans
    if k == N:
        max_ans = max(max_ans, acc)
        min_ans = min(min_ans, acc)
        return
    else:
        if operations[0]:
            operations[0] -= 1
            go(k+1,acc+numbers[k])
            operations[0] += 1
        if operations[1]:
            operations[1] -= 1
            go(k+1,acc-numbers[k])
            operations[1] += 1
        if operations[2]:
            operations[2] -= 1
            go(k+1, acc*numbers[k])
            operations[2] += 1
        if operations[3]:
            operations[3] -= 1
            go(k+1, int(acc/numbers[k]))
            operations[3] += 1


for tc in range(1,int(input())+1):
    N = int(input())
    operations = list(map(int,input().split()))
    numbers = list(map(int,input().split()))
    # print(operations)
    # print(numbers)
    min_ans = 0xffff
    max_ans = -0xffff

    go(1, numbers[0])
    ans = max_ans - min_ans
    print("#%d" % tc, ans)
```

- 문제에서 주어진 조건대로, if문을 이용해 케이스를 잘게 나누어 연산을 해주며 재귀함수를 실행해주면 된다.
- 다소 무식해보이지만, 케이스를 잘게 쪼갬으로써 저절로 백트랙킹도 함께 된다.(러닝타임이 줄어든다.)