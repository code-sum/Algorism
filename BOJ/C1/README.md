# 📌BOJ solved.ac CLASS1

>  총 36문제 중 실습기간에 건너뛴 문제들 풀이



#### 1001. A-B [(link)](https://www.acmicpc.net/problem/1001)

> 두 정수 A와 B를 입력받은 다음, A-B를 출력하는 프로그램을 작성하시오.

```python
a,b = map(int, input().split())
print(a-b)
```



#### 1008. A/B [(link)](https://www.acmicpc.net/problem/1008)

> 두 정수 A와 B를 입력받은 다음, A/B를 출력하는 프로그램을 작성하시오.

```python
a,b = map(int, input().split())
print(a/b)
```



#### 1152. 단어의 개수 [(link)](https://www.acmicpc.net/problem/1152)

> 영어 대소문자와 공백으로 이루어진 문자열이 주어진다. 이 문자열에는 몇 개의 단어가 있을까? 이를 구하는 프로그램을 작성하시오. 단, 한 단어가 여러 번 등장하면 등장한 횟수만큼 모두 세어야 한다.

```python
import sys
sys.stdin = open("1152.txt")

words = list(map(str, input().split()))
print(len(words))
```



#### 1546. 평균 [(link)](https://www.acmicpc.net/problem/1546)

> 세준이는 기말고사를 망쳤다. 세준이는 점수를 조작해서 집에 가져가기로 했다. 일단 세준이는 자기 점수 중에 최댓값을 골랐다. 이 값을 M이라고 한다. 그리고 나서 모든 점수를 점수/M*100으로 고쳤다.
>
> 예를 들어, 세준이의 최고점이 70이고, 수학점수가 50이었으면 수학점수는 50/70*100이 되어 71.43점이 된다.
>
> 세준이의 성적을 위의 방법대로 새로 계산했을 때, 새로운 평균을 구하는 프로그램을 작성하시오.

```python
import sys
sys.stdin = open("1546.txt")

n = int(input())
scores = list(map(int, input().split()))
scores2 = []

for i in scores:
    scores2.append((i/max(scores))*100)
print(sum(scores2)/n)
```



#### 2475. 검증수 [(link)](https://www.acmicpc.net/problem/2475)

> 컴퓨터를 제조하는 회사인 KOI 전자에서는 제조하는 컴퓨터마다 6자리의 고유번호를 매긴다. 고유번호의 처음 5자리에는 00000부터 99999까지의 수 중 하나가 주어지며 6번째 자리에는 검증수가 들어간다. 검증수는 고유번호의 처음 5자리에 들어가는 5개의 숫자를 각각 제곱한 수의 합을 10으로 나눈 나머지이다.
>
> 예를 들어 고유번호의 처음 5자리의 숫자들이 04256이면, 각 숫자를 제곱한 수들의 합 0+16+4+25+36 = 81 을 10으로 나눈 나머지인 1이 검증수이다.

```python
numbers = list(map(int, input().split()))
ans = 0

for i in numbers:
    ans += i**2

print(ans%10)
```



#### 2557. Hello World [(link)](https://www.acmicpc.net/problem/2557)

> Hello World!를 출력하시오.

```python
print("Hello World!")
```



#### 2562. 최댓값 [(link)](https://www.acmicpc.net/problem/2562)

> 9개의 서로 다른 자연수가 주어질 때, 이들 중 최댓값을 찾고 그 최댓값이 몇 번째 수인지를 구하는 프로그램을 작성하시오.
>
> 예를 들어, 서로 다른 9개의 자연수
>
> 3, 29, 38, 12, 57, 74, 40, 85, 61
>
> 이 주어지면, 이들 중 최댓값은 85이고, 이 값은 8번째 수이다.

```python
import sys
sys.stdin = open("2562.txt")

numbers = []

for i in range(9):
    numbers.append(int(input()))
print(max(numbers))

for i in range(len(numbers)):
    if numbers[i] == max(numbers):
        print(i+1)
```



#### 2577. 숫자의 개수 [(link)](https://www.acmicpc.net/problem/2577)

> 세 개의 자연수 A, B, C가 주어질 때 A × B × C를 계산한 결과에 0부터 9까지 각각의 숫자가 몇 번씩 쓰였는지를 구하는 프로그램을 작성하시오.
>
> 예를 들어 A = 150, B = 266, C = 427 이라면 A × B × C = 150 × 266 × 427 = 17037300 이 되고, 계산한 결과 17037300 에는 0이 3번, 1이 1번, 3이 2번, 7이 2번 쓰였다.

```python
import sys
sys.stdin = open("2577.txt")

multi = 1
for _ in range(3):
    multi *= int(input())

ans = list(str(multi))
for i in range(10):
    print(ans.count(str(i)))
```



#### 2675. 문자열 반복 [(link)](https://www.acmicpc.net/problem/2675)

> 문자열 S를 입력받은 후에, 각 문자를 R번 반복해 새 문자열 P를 만든 후 출력하는 프로그램을 작성하시오. 즉, 첫 번째 문자를 R번 반복하고, 두 번째 문자를 R번 반복하는 식으로 P를 만들면 된다. S에는 QR Code "alphanumeric" 문자만 들어있다.
>
> QR Code "alphanumeric" 문자는 `0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ\$%*+-./:` 이다.

```python
import sys
sys.stdin = open("2675.txt")

t = int(input())

for _ in range(t):
    num, char = input().split()
    new_num = int(num)

    ans = []
    for i in char:
        ans.append(i*new_num)
    print(*ans, sep='')
```

