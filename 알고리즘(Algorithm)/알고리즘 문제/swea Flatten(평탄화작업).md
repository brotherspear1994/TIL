# swea

# Flatten(평탄화)

### 일자 20200804

### 문제

한 쪽 벽면에 다음과 같이 노란색 상자들이 쌓여 있다.

높은 곳의 상자를 낮은 곳에 옮기는 방식으로 최고점과 최저점의 간격을 줄이는 작업을 평탄화라고 한다.

평탄화를 모두 수행하고 나면, 가장 높은 곳과 가장 낮은 곳의 차이가 최대 1 이내가 된다.

평탄화 작업을 위해서 상자를 옮기는 작업 횟수에 제한이 걸려있을 때, 제한된 횟수만큼 옮기는 작업을 한 후 최고점과 최저점의 차이를 반환하는 프로그램을 작성하시오.


 


가장 높은 곳에 있는 상자를 가장 낮은 곳으로 옮기는 작업을 덤프라고 정의한다.





A부분의 상자를 가장 낮은 B부분에 덤프하였으며, A대신 A’부분의 상자를 사용해도 무방하다.





A’부분의 상자를 옮겨서, C부분에 덤프하였다. 이때 C 대신 C’부분에 덤프해도 무방하다.

2회의 덤프 후, 최고점과 최저점의 차이는 8 – 2 = 6 이 되었다 (최초덤프 이전에는 9 – 1 = 8 이었다).

덤프 횟수가 2회로 제한된다면, 이 예시 문제의 정답은 6이 된다.

**[제약 사항]**

가로 길이는 항상 100으로 주어진다.

모든 위치에서 상자의 높이는 1이상 100이하로 주어진다.

덤프 횟수는 1이상 1000이하로 주어진다.

주어진 덤프 횟수 이내에 평탄화가 완료되면 더 이상 덤프를 수행할 수 없으므로 그 때의 최고점과 최저점의 높이 차를 반환한다 (주어진 data에 따라 0 또는 1이 된다).

**[입력]**

총 10개의 테스트 케이스가 주어지며, 각 테스트 케이스의 첫 번째 줄에는 덤프 횟수가 주어진다. 그리고 다음 줄에 각 상자의 높이값이 주어진다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 테스트 케이스의 최고점과 최저점의 높이 차를 출력한다.

#### 풀이1

```python
import sys
sys.stdin = open('input (2).txt', 'r')

for tc in range(1,11):
    dump_limit = int(input())
    height = list(map(int, input().split()))
    for i in range(dump_limit):
        max_h, min_h = max(height), min(height)
        index_max_h = height.index(max_h)
        # print((index_max_h))
        index_min_h = height.index(min_h)
        height[index_max_h] -= 1
        height[index_min_h] += 1
    print("#{} {}".format(tc, max(height) - min(height)))
```

### 풀이 2

```python
def find(lst):
    max_num = 0
    max_idx = 0
    min_num = 10000
    min_idx = 0
    for i in range(len(lst)):
        if lst[i] >= max_num:
            max_num = lst[i]
            max_idx = i
        if lst[i] <= min_num:
            min_num = lst[i]
            min_idx = i
    return (max_num, max_idx, min_num, min_idx)



for tc in range(1,11):
    max_box = 0
    max_idx = 0
    min_box = 0
    min_idx = 0
    limit = int(input())
    boxs = list(map(int,input().split()))
    # print(find(boxs))

    for _ in range(limit):
        max_box, max_idx, min_box, min_idx = find(boxs)
        boxs[max_idx] -= 1
        boxs[min_idx] += 1
    result = find(boxs)
    ans = result[0]-result[2]
    print("#{} {}".format(tc, ans))
```

- SWEA 역량테스트 IM대비를 위해 시간이지나 까먹을 수 있는 부분들을  다시 한 번 풀며 복습해봤다.(0829기준)
- 지금 두 코드를 비교해보니 둘 다 내가 푼 풀이이지만 자연스레 많이 차이가 나는 것이 보인다.