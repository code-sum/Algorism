# 📌 2022-07-27 BOJ 풀이



#### 1157. 단어 공부 [(link)](https://www.acmicpc.net/problem/1157)

> 알파벳 대소문자로 된 단어가 주어지면, 이 단어에서 가장 많이 사용된 알파벳이 무엇인지 알아내는 프로그램을 작성하시오. 단, 대문자와 소문자를 구분하지 않는다.

```python
# 변수.upper() = 변수에 있는 영어 소문자를 전부 대문자로 바꿈
word = input().upper()

# 주어진 word 에서 중복 값을 전부 제거하여 새로운 변수를 만듬
unique_word = list(set(word))

cnt_list = []
for i in unique_word:

    # A변수.count(B변수) = A변수에서 B변수 갯수를 세어라
    cnt = word.count(i)
    cnt_list.append(cnt)

# 가장 많이 사용된 알파벳이 여러 개면 "?" 출력
if cnt_list.count(max(cnt_list)) > 1:
    print("?")
else:
    max_index = cnt_list.index(max(cnt_list))
    print(unique_word[max_index])
```



#### 2511. 카드놀이 [(link)](https://www.acmicpc.net/problem/2511)

> 0부터 9까지의 숫자가 표시된 카드를 가지고 두 사람 A와 B가 게임을 한다. A와 B에게는 각각 0에서 9까지의 숫자가 하나씩 표시된 10장의 카드뭉치가 주어진다. 두 사람은 카드를 임의의 순서로 섞은 후 숫자가 보이지 않게 일렬로 늘어  놓고 게임을 시작한다. 단, 게임 도중 카드의 순서를 바꿀 수는 없다.
>
> A와 B 각각이 늘어놓은 카드를 뒤집어서 표시된 숫자를 확인하는 것을 한 라운드라고 한다. 게임은 첫 번째 놓인 카드부터 시작하여 순서대로 10번의 라운드로 진행된다. 각 라운드에서는 공개된 숫자가 더 큰 사람이 승자가 된다. 승자에게는 승점 3점이 주어지고 패자에게는 승점이 주어지지 않는다. 만약 공개된 두 숫자가 같아서 비기게 되면, A, B 모두에게 승점 1점이 주어진다. 
>
> 10번의 라운드가 모두 진행된 후, 총 승점이 큰 사람이 게임의 승자가 된다. 만약, A와 B의 총 승점이 같은 경우에는, 제일 마지막에 이긴 사람을 게임의 승자로 정한다. 그래도 승부가 나지 않는 경우는 모든 라운드에서 비기는 경우뿐이고 이 경우에 두 사람은 비겼다고 한다.
>
> 예를 들어, 다음 표에서 3번째 줄은 각 라운드의 승자를 표시하고 있다. 표에서 D는 무승부를 나타낸다. 이 경우에 A의 총 승점은 16점이고, B는 13점이어서, A가 게임의 승자가 된다. 
>
> | 라운드 | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   |
> | ------ | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
> | A      | 4    | 5    | 6    | 7    | 0    | 1    | 2    | 3    | 9    | 8    |
> | B      | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 0    |
> | 승     | A    | A    | A    | A    | B    | B    | B    | B    | D    | A    |
>
> 아래 표의 경우에는 A와 B의 총 승점은 13점으로 같다. 마지막으로 승부가 난 라운드는 7번째 라운드이고, 이 라운드의 승자인 B가 게임의 승자가 된다. 
>
> | 라운드 | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   |
> | ------ | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
> | A      | 9    | 1    | 7    | 2    | 6    | 3    | 0    | 4    | 8    | 5    |
> | B      | 6    | 3    | 9    | 2    | 1    | 0    | 7    | 4    | 8    | 5    |
> | 승     | A    | B    | B    | D    | A    | A    | B    | D    | D    | D    |
>
> A와 B가 늘어놓은 카드의 숫자가 순서대로 주어질 때, 게임의 승자가 A인지 B인지, 또는 비겼는지 결정하는 프로그램을 작성하시오.

```python
import sys
sys.stdin = open("2511.txt")

# 승자는 각 라운드당 +3 승점
# 패자에게는 승점 없음
# 비길 경우 두 사람에게 +1 승점
# 라운드 종료 후 총점이 큰 사람이 승자
# 승점이 같으면 마지막에 이긴 사람이 승자

a = list(map(int, input().split()))
b = list(map(int, input().split()))

a_cnt = 0; b_cnt = 0
record = [0 for i in range(10)]

for i in range(10):
    if a[i] > b[i]:
        a_cnt += 3; record[i] = "A"
    elif a[i] < b[i]:
        b_cnt += 3; record[i] = "B"
    else:
        a_cnt += 1; b_cnt += 1; record[i] = "D"

# A점수가 더 높을 경우 출력
if a_cnt > b_cnt:
    print(a_cnt, b_cnt)
    print("A")

# B점수가 더 높을 경우 출력
if a_cnt < b_cnt:
    print(a_cnt, b_cnt)
    print("B")

# A와 B 총점이 동점일 경우 출력
if a_cnt == b_cnt:
    if a == b:
        print(a_cnt, b_cnt)
        print("D")
    else:
        print(a_cnt, b_cnt)
        for i in reversed(range(10)):
            if record[i] == "A":
                print("A"); break
            elif record[i] == "B":
                print("B"); break
```



#### 2711. 오타맨 고창영 [(link)](https://www.acmicpc.net/problem/2711)

> 고창영은 맨날 오타를 낸다. 창영이가 오타를 낸 문장과 오타를 낸 위치가 주어졌을 때, 오타를 지운 문자열을 출력하는 프로그램을 작성하시오.
>
> 창영이는 오타를 반드시 1개만 낸다.

```python
import sys
sys.stdin = open("2711.txt")

t = int(input())

for i in range(1, t+1):
    tc = list(input().split())
    # print(*tc)

    spot = int(tc[0])-1
    word = list(tc[1])
    
    for j in range(len(word)):
        if j == spot:
            del word[j]
    
    print(*word, sep='')
```

