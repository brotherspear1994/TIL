# JUNGOL

# 1523 : 별삼각형1

### 문제

[JUNGOL 홈페이지 본문 참조](http://jungol.co.kr/bbs/board.php?bo_table=pbank&wr_id=795&sca=2020)



**< 처리조건 >** 

숫자의 진행 순서는 처음에 왼쪽에서 오른쪽으로 너비 m만큼 진행 한 후 방향을 바꾸어서 이를 반복한다.

```python
n, m = map(int, input().split())
if m == 1:
    arr_1= [['*' * s_1] for s_1 in range(1, n+1)]
    for p_1 in range(len(arr_1)):
        for star_1 in arr_1[p_1]:
            print(star_1, end = ' ')
        print()

if m == 2:
    arr_2= [['*' * s_2] for s_2 in range(1, n+1)]
    for p_2 in range(len(arr_2)-1,-1,-1):
        for star_2 in arr_2[p_2]:
            print(star_2, end = ' ')
        print()

if m == 3:
    arr_3 = []
    for s_3 in range(1,n+1):
        if s_3 < n:
            arr_3.append([' ']*int(int((2*n-1)-(2*s_3-1))/2)+['*'*(2*s_3-1)]+[' ']*int(int((2*n-1)-(2*s_3-1))/2))
        else:
            arr_3.append(['*'*(2*s_3-1)])
    for p_3 in range(len(arr_3)):
        for star_3 in arr_3[p_3]:
            print(star_3, end = '')
        print() 
# lst = []
# arrr_1 = ([' ']*5 + ['*'*3] + [' ']*5)
# arrr_2 = ([' ']*6 + ['*'*3] + [' ']*6)
# lst.append(arrr_1)
# lst.append(arrr_2)
# print(lst)

```



- 우선 숫자를 2로 나누면 float type로 바뀐다는 사실을 알았다. 예로 6을 2로 나누면 3이 아닌 3.0으로 표시된다. 따라서 이를 str과 곱해주고 싶을때는 int처리를 해주어야 한다.

- print(,end='') 기능은 ''사이에 오는 문자단위로 이어서 출력해주는 기능으로만 알고있었다. 예컨대 1,2,3,4,5를반복문으로 출력할때 print(~,end='*')로 출력하면 

  ```python
  1*2*3*4*5*
  ```

  로 출력된다. 다만 위 문제에서 별모양을 print(~,end=' ')로 하면 위 규칙과 다르게 별이다 출력되고 난 직후 바로 다음줄로 넘어가버린다. 이유를 알아내지는 못했다 ㅜ.

