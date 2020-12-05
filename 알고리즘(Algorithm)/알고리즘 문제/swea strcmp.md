# swea

# strcmp 연습문제

### 일자 20200825

#### 풀이

```python
def strcmp(s1, s2):
    if len(s1) != len(s2):
        return False
    else:
        i = 0
        while i < len(s1) and i < len(s2):
            if s1[i] != s2[i]:
                return False
            i += 1
    return True

a = "abc"
b = "acb"

print(strcmp(a, b))
```

- 두 문자열의 동일 여부를 True or False 값으로 반환하는 strcmp 함수를 만들어 보았다.
- if 조건문의 == 기능을 직접구현해 봤다고 할 수 있다.