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



## SOL

BruteForce는 `함수 정의`가 50% 



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

- How to :

```python
#


#


#
```


























