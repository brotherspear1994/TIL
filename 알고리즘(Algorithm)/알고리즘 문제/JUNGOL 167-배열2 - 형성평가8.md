# JUNGOL

# 167 : 배열2 - 형성평가8

### 문제

4행 2열의 배열을 입력받아 가로평균과 세로평균 그리고 전체평균을 출력하는 프로그램을 작성하시오. (소수점 이하는 버림 한다.)

```python
'''
16 27
39 100
19 88
61 20
'''
# 입력
lst=[]
final_lst=[]
for l in range(4):
    N = list(map(int, input().split()))
    lst.append(N)
# 계산

result_1=[]
for i in range(len(lst)):
    result_1.append(int(sum(lst[i])/len(lst[i])))
# print(result_1)

result_2=[]
for j in range(len(lst[0])):
    sum_sub = 0
    for i in range(len(lst)):
        sum_sub += lst[i][j]
    result_2.append(int(sum_sub/len(lst)))
# print(result_2)

result_3=[]
sum_sub_sub = 0
total = 0
for i in range(len(lst)):
    for j in range(len(lst[i])):
        sum_sub_sub += lst[i][j]
        total += 1
result_3.append(int(sum_sub_sub/total))
# print(result_3)

#출력
final_lst.append(result_1)
final_lst.append(result_2)
final_lst.append(result_3)
# print(final_lst)

for i in final_lst:
    for j in i:
        print(j, end=' ')
    print()

```



- 출력을 쉽게 하는 법을 알아내어 기쁘다 :)