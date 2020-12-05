# swea

# 문자열 비교

### 일자 20200825

#### 풀이 1

```python
'''
3
XYPV
EOGGXYPVSY
STJJ
HOFSTJPVPP
ZYJZXZTIBSDG
TTXGZYJZXZTIBSDGWQLW
'''

def brute(s1, s2):
    i, j = 0, 0
    while i < len(s1) and j < len(s2):
        if s1[i] != s2[j]:
            j = j-i
            i = -1
        i += 1
        j += 1
    if i == len(s1):
        return 1
    else:
        return 0

for tc in range(1,int(input())+1):
    str1 = input()
    str2 = input()
    # print(str1, str2)

    #계산
    result = brute(str1, str2)
    print('#{} {}'.format(tc, result))
```



### 풀이2 

```python
def find(str1,str2):
    for i in range(0,len(str2)-len(str1)+1):
        j = 0
        while str1[j] == str2[i+j]:
            j += 1
            if j == len(str1):
                return 1
    return 0


T= int(input())
for tc in range(1,T+1):
    str1 = input()
    str2 = input()

    print(find(str1, str2))
```

- brute 개념을 배운 직후 풀어본 brute 기본문제이다.
- brute 알고리즘을 직접 대입해 풀 수 있는 문제라 어렵지는 않았다.
- 이후에는 while문을 활용한 find함수를 직접 만들어 푸는 방법도 익혀보았다.
