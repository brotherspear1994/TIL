# SWEA

# 암호코드 스캔

### 일자 20201027

#### 문제

[본문 링크 참조](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV15JEKKAM8CFAYD&categoryId=AV15JEKKAM8CFAYD&categoryType=CODE)

#### 풀이

```python
endeciaml = {'112':0, '122':1, '221':2,'114':3, '231':4,'132':5, '411':6, '213':7, '312':8, '211':9}
enbinary = {'0':'0000', '1':'0001', '2':'0010','3':'0011','4':'0100','5':'0101','6':'0110','7':'0111','8':'1000','9':'1001',
            'A':'1010','B':'1011','C':'1100','D':'1101','E':'1110','F':'1111'}


def certificated(lst):
    a = lst[0]+lst[2]+lst[4]+lst[6]
    b = lst[1]+lst[3]+lst[5]+lst[7] # 우리는 거꾸로부터 긁어서 res에 맨끝자리부터 집어넣었음을 유의.
    if (a+b*3) % 10 == 0:
        return True
    else:
        return False


for tc in range(1,int(input())+1):
    N, M = map(int, input().split())
    code = [input()[:M] for _ in range(N)]

    for n in range(N):
        bin = ''
        for char in code[n]:
            bin += enbinary[char]
        code[n] = bin
    # for c in code:
    #     print(c)
    # print()
    visited = []
    res = []
    ans = 0
    for n in range(N):
        f1 = f2 = f3 = 0
        if '1' in code[n]:
            for m in range(M*4-1,-1,-1):
                if f2==0 and f3==0 and code[n][m] == '1': f1 += 1
                elif f1 and f3==0 and code[n][m] == '0': f2 += 1
                elif f1 and f2 and code[n][m] == '1': f3 += 1
                elif f3 and code[n][m] == '0':
                    common_denominator = min(f1,f2,f3)
                    res.append(endeciaml[str(f1//common_denominator)+str(f2//common_denominator)+str(f3//common_denominator)])
                    f1=f2=f3=0
                    if len(res)==8:
                        if res not in visited:
                            if certificated(res):
                                ans += sum(res)
                            visited.append(res)
                        res = []
    print("#%d" % tc, ans)
```

- 최초 입력을 받을 때 M의 길이 만큼 슬라이싱을 해서 각 암호코드의 배열의 크기를 맞춰준다.

- 이진화도 비트연산자나 ord를 사용하지 않고 하드코딩(딕셔너리)를 활용해 줘야 한다.

- 이진코드로 변환시킨후 코드의 넓이의 비를 구할때는 뒤에서부터 읽어나가기 때문에, 뒷자리부터비율을 매칭시키고, 4자리 전부 사용할 필요없이 3자리만 이용해준다.

- 넓이의 비는 배수로 나올수 있으므로, 최대공약수를 구해 각 비율을 최대공약수로 나누어준다.

- for문이 반복될때마다 f1,f2,f3과 res가 최신화 되지만 같은 행에 또다른 암호코드가 주어질수 있으므로 각각의 사용이 완료되자마자 바로 초기화를 해준다.

  