# swea

# atoi 연습문제

### 일자 20200825

#### 풀이

```python
def atoi(str):
    value = 0
    for i in range(len(str)):
        c = str[i]
        # 0 ~ 9
        if c >= '0' and c <= "9":
            digit = ord(c) - ord('0')
            # print(ord(c), ord('0'))
        else:
            break
        value = value*10 + digit
    return value
a = "123"
# print(type(a))
b = atoi(a)
print(b)
print(type(b))
```

- 숫자를 문자열로 입력받아 숫자형으로 전환시키는 int 기능을 직접 구현해 봤다.