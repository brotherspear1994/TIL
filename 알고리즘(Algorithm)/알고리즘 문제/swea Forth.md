# swea

# Forth

### 일자 20200901



### 문제

Forth라는 컴퓨터 언어는 스택 연산을 기반으로 하고 있어 후위 표기법을 사용한다. 예를 들어 3+4는 다음과 같이 표기한다.


3 4 + .

Forth에서는 동작은 다음과 같다.


숫자는 스택에 넣는다.

연산자를 만나면 스택의 숫자 두 개를 꺼내 더하고 결과를 다시 스택에 넣는다.

‘.’은 스택에서 숫자를 꺼내 출력한다.

 

Forth 코드의 연산 결과를 출력하는 프로그램을 만드시오. 만약 형식이 잘못되어 연산이 불가능한 경우 ‘error’를 출력한다.


다음은 Forth 연산의 예이다.


| 코드    | 출력 |
| ------- | ---- |
| 4 2 / . | 2    |
| 4 3 - . | 1    |

**[입력]**


첫 줄에 테스트 케이스 개수 T가 주어진다. 1≤T≤50


다음 줄부터 테스트 케이스의 별로 정수와 연산자가 256자 이내의 연산코드가 주어진다. 피연산자와 연산자는 여백으로 구분되어 있으며, 코드는 ‘.’로 끝난다.

나눗셈의 경우 항상 나누어 떨어진다.

**[출력]**

\#과 1번부터인 테스트케이스 번호, 빈칸에 이어 계산결과를 정수로 출력하거나 또는 ‘error’를 출력한다.



#### 풀이1

```python
T = int(input())
for tc in range(1,T+1):
    operator = list(input().split())
    # print(operator)
    op_list = ['+','-','*','/']
    stack = []
    bool = True
    result = 0
    for element in operator:
        try:
            if element in op_list:
                if element == operator[0]: bool = False
                if len(stack) < 2: bool = False
                elif element == '+':
                    num2, num1 = int(stack.pop()), int(stack.pop())
                    result = num1 + num2
                elif element == '-':
                    num2, num1 = int(stack.pop()), int(stack.pop())
                    result = num1 - num2
                elif element == '*':
                    num2, num1 = int(stack.pop()), int(stack.pop())
                    result = num1 * num2
                elif element == '/':
                    num2, num1 = int(stack.pop()), int(stack.pop())
                    result = num1 // num2
            if result:
                stack.append(result)
                result = 0
            if element == '.':
                if bool == False:
                    print("#{} error".format(tc))
                if bool == True:
                    if len(stack) > 1 or len(stack)==0:
                        print("#{} error".format(tc))
                    else: print("#{} {}".format(tc, stack[0]))
            if element not in op_list and element != '.':
                stack.append(element)
        except:
            print("{} error".format(tc))
```

- 우선 `후위표기법`이 어떠한 것인지는 간략하게 나마 알고 있어야한다.
- 그 이후 스택을 활용해 문제에서 주어진대로 사칙연산을 적절히 시켜주면 된다.
- 스택을 얼마나 잘 사용할 수 있는지를 물어보는 문제이다.



#### 풀이2

```python
def find():
    s = [] #스텍준비
    for i in range(len(code)):
        #연산자면 연산
        #아니면 연산
        if code[i] == "+" or code[i] == '-' or code[i] == '*' or code[i] == '/':
            if len(s) >= 2: #연산가능할때
                op2, op1 = int(s.pop()), int(s.pop())
                if code[i] == "+":
                    s.append(op1+op2)
                elif code[i] == "-":
                    s.append(op1-op2)
                elif code[i] == "*":
                    s.append(op1*op2)
                elif code[i] == "/":
                    s.append(op1//op2)
            else: return "error"


        #숫자면 스텍에 넣기
        elif code[i] != ' ' and code[i] != '.':
            s.append(code[i])
        elif code[i] == ".":
            if len(s) == 1:
                return s.pop()
            else:
                return "error"
T = int(input())
for tc in range(1,T+1):
    code = list(input().split())
    # print(code)
    print("#{} {}".format(tc,find()))
```

- 처음 문제를 푼 후 교수님의 풀이도 배워보았다.
- 마찬가지로 후위 표기법으로 잘 정리해주고 연산만 해주면 된다.
- 첫번째 풀이법과는 다르게 try, except를 사용해주지 않고 if문을 이용해 에러가 발생할 경우를 잘 나누어 주었다.
- 강의 후에는 혼자 코드를 짜보는 시간도 가졌다.