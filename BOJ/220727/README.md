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



#### 2789. 유학금지 [(link)](https://www.acmicpc.net/problem/2789)

> 아주 멀리 떨어져 있는 작은 나라가 있다. 이 나라에서 가장 공부를 잘하는 학생들은 모두 다른 나라로 유학을 간다. 정부는 최고의 학생들이 자꾸 유학을 가는 이유를 찾으려고 했다. 하지만, 학생들의 이유가 모두 달랐기 때문에 정확한 이유를 찾을 수 없었다. 정부의 고위직은 뛰어난 학생들이 자꾸 유학을 가는 현상을 매우 불쾌해 했다.
>
> 가장 많은 학생들이 유학을 가는 대학교는 영국의 캠브리지 대학교이다. 정부는 인터넷 검열을 통해서 해외로 나가는 이메일의 내용 중 일부를 삭제하기로 했다. 이메일의 각 단어 중에서 CAMBRIDGE에 포함된 알파벳은 모두 지우기로 했다. 즉, 어떤 이메일에 LOVA란 단어가 있다면, A는 CAMBRIDGE에 포함된 알파벳이기 때문에, 받아보는 사람은 LOV로 받는다.
>
> 이렇게, 어떤 단어가 주어졌을 때, 검열을 거친 후에는 어떤 단어가 되는지 구하는 프로그램을 작성하시오.

```python
word = input()

ans = []
for i in word:
    if i not in 'CAMBRIDGE':
        ans.append(i)

print(*ans, sep='')
```



#### 2851. 슈퍼 마리오 [(link)](https://www.acmicpc.net/problem/2851)

> 슈퍼 마리오 앞에 10개의 버섯이 일렬로 놓여져 있다. 이 버섯을 먹으면 점수를 받는다.
>
> 슈퍼 마리오는 버섯을 처음부터 나온 순서대로 집으려고 한다. 하지만, 모든 버섯을 집을 필요는 없고 중간에 중단할 수 있다. 중간에 버섯을 먹는 것을 중단했다면, 그 이후에 나온 버섯은 모두 먹을 수 없다. 따라서 첫 버섯을 먹지 않았다면, 그 이후 버섯도 모두 먹을 수 없다.
>
> 마리오는 받은 점수의 합을 최대한 100에 가깝게 만들려고 한다.
>
> 버섯의 점수가 주어졌을 때, 마리오가 받는 점수를 출력하는 프로그램을 작성하시오.

```python
# 먹은 버섯 리스트
eaten = []

# 데이터 입력
for i in range(10):
    point = int(input())
    eaten.append(point)

# 먹은 점수의 초기값
score = 0

for j in eaten:
    score += j
    if score >= 100:
        if score - 100 > 100 - (score - j):
            score -= j
        break

print(score)
```



#### 2920. 음계 [(link)](https://www.acmicpc.net/problem/2920)

> 다장조는 c d e f g a b C, 총 8개 음으로 이루어져있다. 이 문제에서 8개 음은 다음과 같이 숫자로 바꾸어 표현한다. c는 1로, d는 2로, ..., C를 8로 바꾼다.
>
> 1부터 8까지 차례대로 연주한다면 ascending, 8부터 1까지 차례대로 연주한다면 descending, 둘 다 아니라면 mixed 이다.
>
> 연주한 순서가 주어졌을 때, 이것이 ascending인지, descending인지, 아니면 mixed인지 판별하는 프로그램을 작성하시오.

```python
import sys
sys.stdin = open("2920.txt")

input_ = input()

if input_ == "1 2 3 4 5 6 7 8":
    print("ascending")
elif input_ == "8 7 6 5 4 3 2 1":
    print("descending")
else:
    print("mixed")
```



#### 2941. 크로아티아 알파벳 [(link)](https://www.acmicpc.net/problem/2941)

> 예전에는 운영체제에서 크로아티아 알파벳을 입력할 수가 없었다. 따라서, 다음과 같이 크로아티아 알파벳을 변경해서 입력했다.
>
> | 크로아티아 알파벳 | 변경 |
> | ----------------- | ---- |
> | č                 | c=   |
> | ć                 | c-   |
> | dž                | dz=  |
> | đ                 | d-   |
> | lj                | lj   |
> | nj                | nj   |
> | š                 | s=   |
> | ž                 | z=   |
>
> 예를 들어, ljes=njak은 크로아티아 알파벳 6개(lj, e, š, nj, a, k)로 이루어져 있다. 단어가 주어졌을 때, 몇 개의 크로아티아 알파벳으로 이루어져 있는지 출력한다.
>
> dž는 무조건 하나의 알파벳으로 쓰이고, d와 ž가 분리된 것으로 보지 않는다. lj와 nj도 마찬가지이다. 위 목록에 없는 알파벳은 한 글자씩 센다.

```python
croatia = ['c=', 'c-', 'dz=', 'd-', 'lj', 'nj', 's=', 'z=']
word = input()

for i in croatia:
    word = word.replace(i, '*')

print(len(word))
```

