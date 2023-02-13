# 📌2022-08-02 BOJ 풀이



#### 1269. 대칭차집합 [(link)](https://www.acmicpc.net/problem/1269)

> 자연수를 원소로 갖는 공집합이 아닌 두 집합 A와 B가 있다. 이때, 두 집합의 대칭 차집합의 원소의 개수를 출력하는 프로그램을 작성하시오. 두 집합 A와 B가 있을 때, (A-B)와 (B-A)의 합집합을 A와 B의 대칭 차집합이라고 한다.
>
> 예를 들어, A = { 1, 2, 4 } 이고, B = { 2, 3, 4, 5, 6 } 라고 할 때, A-B = { 1 } 이고, B-A = { 3, 5, 6 } 이므로, 대칭 차집합의 원소의 개수는 1 + 3 = 4개이다.

```python
n, m = map(int, input().split())

# 집합A, 집합B 생성
A = set(map(int, input().split()))
B = set(map(int, input().split()))

# 대칭차집합 원소의 갯수 출력(set의 len() 구하기)
print(len(A-B)+len(B-A))
```



#### 2750. 수 정렬하기 [(link)](https://www.acmicpc.net/problem/2750)

> N개의 수가 주어졌을 때, 이를 오름차순으로 정렬하는 프로그램을 작성하시오.

```python
import sys
sys.stdin = open("2750.txt")

# 첫째줄에 수의 개수 n 입력
n = int(input())

num_list = []

# 입력뇌는 n개의 수를 num_list 에 넣은 다음 정렬하기
for i in range(n):
    num_list.append(int(input()))

sorted_list = sorted(num_list)

# 정렬한 리스트의 원소들을 한줄씩 차례대로 출력
for i in range(len(num_list)):
    print(sorted_list[i])
```

