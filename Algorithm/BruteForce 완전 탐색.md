# BruteForce 완전 탐색

--------

> [toc]



## 설명

문제를 해결하기 위해 확인해야 하는 모든 경우를 전부 탐색하는 방법

그 중에서도 `백 트래킹 Back-Tracking` 을 통해야 하는 상황을 해야하기!

*모든 코테 문제에서 기본적으로 접근해 봐야 한다. 많은 연습이 필요!*

장점 : 부분점수를 얻기 좋다

단점 : 전부 탐색하기에 시간 복잡도가 일반적으로 높다



## 코테에 나오는 BruteForce 종류

(총 4가지)

N개 중

1. 중복을 허용해서

2. 중복 없이

   ​	M개를 

   ​		a. 순서 있게 나열하기

   ​		b. 고르기



## 문제

#### 1+A 버전 (N개 중 1.중복을 허용해서 M개를 A.순서 있게 나열하기)



[BOJ 15651_N과 M(3)](https://www.acmicpc.net/problem/15651)

- How to : 

```python
# 시간, 공간 복잡도 계산하기
N = 4, M = 3   ___ ___ ___
    		    4 x 4 x 4 = 4^3
    			
        		시간 : O(N^M) => 7^7 ~= 82만
                공간 : O(M)

# 구현 스케치
변수 N, M
기록하는 배열 selected []

Recurrence Function
1. 만약 M개를 전부 고름 => 조건에 맞는 탐색을 한 가지 성공한 것!
2. 아직 M개를 고르지 않음 => k번째부터 M번째 원소를 조건에 맞게 고르는 모든 방법을 시도한다.
rec_func(int k) {
    if (k == M + 1) { // 다 골랐다!
        # selected[1...M] 배열이 새롭게 탐색된 결과
    } else {
        # 1~N 까지를 k 번 원소로 한 번씩 정하고,
        # 매번 k+1 번부터 M번 원소로 재귀호출 해주기
    }
}


#########


# 입력값 받아서 배열에 저장
import sys
n, m = map(int, sys.stdin.readline().split(' '))

selected = [0 for _ in range(m)]
used = [0 for _ in range(n + 1)]

# 재귀 함수 정의하기
def rec_func(k):
    if k == m:
        for x in selected:
            sys.stdout.write(str(x) + ' ')
        sys.stdout.write('\n')
    else:
        for cand in range(1, n + 1):
            selected[k] = cand
            rec_func(k + 1)
            selected[k] = 0

rec_func(0)

# 
```



[BOJ 15649_N과 M(1)](https://www.acmicpc.net/problem/15649)

- How to : level2

  <img src="C:\Users\biire\AppData\Roaming\Typora\typora-user-images\image-20210317233013416.png" alt="image-20210317233013416" style="zoom:33%;" />

```python
# 시간, 공간 복잡도 확인하기
N = 4, M = 3  ___ ___ ___
			   4 x 3 x 2 = 4!

# 구현 스케치


# 
import sys
n, m = map(int, sys.stdin.readline().split(' '))

selected = [0 for _ in range(m)]
used = [0 for _ in range(n + 1)]
def rec_func(k):
    if k == m:
        for x in selected:
            sys.stdout.write(str(x) + ' ')
        sys.stdout.write('\n')
    else:
        for cand in range(1, n + 1):
            if used[cand]:
                continue
            selected[k] = cand
            used[cand] = 1
            rec_func(k + 1)
            selected[k] = 0
            used[cand] = 0

rec_func(0)
```



#### 1 + B 버전 (N개 중 1. 중복을 허용해서 M개를 B.고르기)



[BOJ 15652_N과 M(4)](https://www.acmicpc.net/problem/15652)

- How to : level 2

  이전 문제와의 차이점 : 고른차순 비내림차순

```python
# 시간, 복잡도 확인
N = 4, M = 3   ___ ___ ___

				4 x 4 x 4 = 4^3 보단 작다
    			시간 : O(N^M) => 8^8 ~= 1677만 보다는 작다.
            	공간 : O(M)
                    
# 구현 스케치
start 는 이전에 쓰였던 숫자 즉, k-1 번째에 쓰였던 숫자보다는 작거나 같아야 한다.
start 가 0이면 1로 바꿔주고 시작,
cand 값이 0 부터 시작하는 것이 아니라 start 부터 시작한다.


# sol
import sys
n, m = map(int, sys.stdin.readline().split(' '))

selected = [0 for _ in range(m)]
used = [0 for _ in range(n + 1)]
def rec_func(k):
    if k == m:
        for x in selected:
            sys.stdout.write(str(x) + ' ')
        sys.stdout.write('\n')
    else:
        start = 1 if k == 0 else selected[k - 1]
        for cand in range(start, n + 1):
            selected[k] = cand
            rec_func(k + 1)
            selected[k] = 0

rec_func(0)


```



#### 2 + B 버전 (N개 중 2. 중복 없이 M개를 B. 고르기)

[BOJ 15650_N과 M(2)](https://www.acmicpc.net/problem/15650)

How to : level 2

<img src="C:\Users\biire\AppData\Roaming\Typora\typora-user-images\image-20210318010620888.png" alt="image-20210318010620888" style="zoom:33%;" />

```python
# 시간, 복잡도 확인
N = 4, M = 3   ___ ___ ___

				4 x 4 x 4 = 4^3 보단 작다
    			시간 : O(N^M) => 8^8 ~= 1677만 보다는 작다.
            	공간 : O(M)

# 구현 스케치


#
```



## SOLUTION

<img src="C:\Users\biire\AppData\Roaming\Typora\typora-user-images\image-20210318010815394.png" alt="image-20210318010815394" style="zoom:50%;" />

BruteForce 완전 탐색 문제 접근법

- BruteForce는 `함수 정의`가 50% 

- 고를 수 있는 값의 종류 파악하기
- `중복`을 허용하는 지
- `순서`가 중요한 지



--------

## [BOJ 14888_연산자 끼워넣기](https://www.acmicpc.net/problem/14888)

How to?

- 

```python
# 구현 스케치
N, max, min, nums, operators, order
order[1...N - 1] 에 연산자들이 순서대로 저장될 것이다.

if k=N: # 모든 연산자들을 전부 나열하는 방법을 찾은 상태
	# 정한 연산자 순서대로 계산해서 정답을 갱신하기
else: # k 번째 연산자는 무엇을 선택할 것인가
    # 4 가지의 연산자들 중에 뭘 쓸 것인지 선택하고 재귀호출하기


# SOL
import sys
n = int(sys.stdin.readline())
nums = list(map(int, sys.stdin.readline().split(' ')))
operators = list(map(int, sys.stdin.readline().split(' ')))
min = 1e9
max = -1e9

def calculator(operand1, operator, operand2):
    if operator == 0:
        return operand1 + operand2
    if operator == 1:
        return operand1 - operand2
    if operator == 2:
        return operand1 * operand2
    if operator == 3:
        if operand1 < 0:
            return - ((-operand1) // operand2)
        else:
            return operand1 // operand2

def rec_func(k, value):
    if k == n - 1:
        global min, max
        min = min if min < value else value
        max = max if max > value else value
    else:
        global operators
        for cand in range(4):
            if operators[cand] >= 1:
                operators[cand] -= 1
                rec_func(k + 1, calculator(value, cand, nums[k + 1]))
                operators[cand] += 1

rec_func(0, nums[0])
print(max)
print(min)
```







------

refs

> [rhs_github]()
>
> 03_19_응용문제 전 까지 완료
>
> 







