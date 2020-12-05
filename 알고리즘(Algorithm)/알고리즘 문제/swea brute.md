# swea

# brute 연습문제

### 일자 20200825

#### 풀이

```python
text = "TTTTAACCA"
pattern = "TTA"

def brute(t, p):
    i, j = 0, 0
    while i < len(t) and j < len(p):
        if t[i] != p[j]:
            i = i-j
            j = -1
        i += 1
        j += 1
    if j == len(p):
        return 1
    else:
        return 0
print(brute(text, pattern))
```

- 주어진 두개의 문자열을 바탕으로 한 문자열을 다른 문자열 패턴 속에서 몇개를 찾을 수 있는지 찾아보는 연습을 했다.
- brute 알고리즘은 워낙 유명한 알고리즘이라 당시에 나 혼자 반복숙달 연습을 해보았던 기억이 난다.