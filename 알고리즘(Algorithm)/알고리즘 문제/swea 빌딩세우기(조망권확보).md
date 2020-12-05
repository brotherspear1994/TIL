# swea

# 빌딩세우기

### 일자 20200803

#### 풀이

```python
def sol(arr):
    count = 0
    # 조망권이 확보된 세대수를 세기 위해 count를 0으로 놔준다.
    for i in range(2, len(arr)-2):
        # 문제에서 맨 왼쪽 두칸과 맨 오른쪽 두칸에는 건물을 짓지 않는다 했으므로,
        # 범위를 range(2, len(arr)-2)로 놔주고 각 빌딩(i)는 이 범위안에서만
        # 반복문을 돈다.
        height = arr[i]
        # 빌딩수의 높이(=한 빌딩의 세대수)는 각 index(i) 값
        left = max(arr[i-2:i])
        # 좌로 두칸이상의 공백을 확보했는지 여부를 알기위해 i기준으로 좌측 두칸에
        # 최대 값(최고 높이 빌딩)을 구한다.
        right = max(arr[i+1:i+3])
        # 마찬가지로 오른쪽 조망권 확인 함수도 위와같이 설정해준다.
        # 아래부터 왼쪽 조망권 확인
        if height < left:
            continue
            # 왼쪽 조망권 확보를 못했으므로 i+1로 넘어가줌.
        if height < right:
            continue # 오른쪽 조망권 확보 못해도 마찬가지임.
        # 만약 위 조건을 통과하고 조망권을 확보할 만큰 충분히 높다면,
        height_next = max(left, right)
        count += (height - height_next)
    return count

for test_case in range(1, 11):
    trash = input()
    arr = list(map(int, input().split()))
    result = sol(arr)
    print(f'#{test_case} {result}')
```

- 내가 타게팅 한 빌딩을 기준으로 좌 우의 빌딩 높이를 고려해야하는 수리적 사고가 필요하다.
- for문을 활용한다.



> 알고리즘 공부 시작즘 부터 지금까지 배웠던 SWEA academy 문제들을 차근차근 올리려 한다.