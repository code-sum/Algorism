# 📌2022-08-01 BOJ 풀이



#### 1076. 저항 [(link)](https://www.acmicpc.net/problem/1076)

> 전자 제품에는 저항이 들어간다. 저항은 색 3개를 이용해서 그 저항이 몇 옴인지 나타낸다. 처음 색 2개는 저항의 값이고, 마지막 색은 곱해야 하는 값이다. 저항의 값은 다음 표를 이용해서 구한다.
>
> | 색     | 값   | 곱            |
> | :----- | :--- | :------------ |
> | black  | 0    | 1             |
> | brown  | 1    | 10            |
> | red    | 2    | 100           |
> | orange | 3    | 1,000         |
> | yellow | 4    | 10,000        |
> | green  | 5    | 100,000       |
> | blue   | 6    | 1,000,000     |
> | violet | 7    | 10,000,000    |
> | grey   | 8    | 100,000,000   |
> | white  | 9    | 1,000,000,000 |
>
> 예를 들어, 저항의 색이 yellow, violet, red였다면 저항의 값은 4,700이 된다.

```python
import sys
sys.stdin = open("1076.txt")

color = ['black', 'brown', 'red', 
'orange', 'yellow', 'green', 'blue', 'violet', 'grey', 'white']

a = color.index(input())
b = color.index(input())
c = color.index(input())

# 저항값
o = int(str(a) + str(b)) * (10 ** c)
print(o)
```



#### 2161. 카드1 [(link)](https://www.acmicpc.net/problem/2161)

> N장의 카드가 있다. 각각의 카드는 차례로 1부터 N까지의 번호가 붙어 있으며, 1번 카드가 제일 위에, N번 카드가 제일 아래인 상태로 순서대로 카드가 놓여 있다.
>
> 이제 다음과 같은 동작을 카드가 한 장 남을 때까지 반복하게 된다. 우선, 제일 위에 있는 카드를 바닥에 버린다. 그 다음, 제일 위에 있는 카드를 제일 아래에 있는 카드 밑으로 옮긴다.
>
> 예를 들어 N=4인 경우를 생각해 보자. 카드는 제일 위에서부터 1234 의 순서로 놓여있다. 1을 버리면 234가 남는다. 여기서 2를 제일 아래로 옮기면 342가 된다. 3을 버리면 42가 되고, 4를 밑으로 옮기면 24가 된다. 마지막으로 2를 버리고 나면, 버린 카드들은 순서대로 1 3 2가 되고, 남는 카드는 4가 된다.
>
> N이 주어졌을 때, 버린 카드들을 순서대로 출력하고, 마지막에 남게 되는 카드를 출력하는 프로그램을 작성하시오.

```python
# 덱 활용하기
from collections import deque

# 첫째 줄에 정수 N(1 ≤ N ≤ 1,000)이 주어진다.
N = int(input())
card = deque(list(range(1, N+1)))

# 버린 카드를 담아줄 빈 리스트 생성
out = []

while card:
    # card 의 첫번째 요소를 popleft하여 out 에 담기 ------ (1) 떼서 버리기
    card_pop = card.popleft()
    out.append(card_pop)

    # card 의 두번째 요소를 card 의 맨 뒤에 append 하기 -- (2) 떼서 뒤에 붙이기
    if card:
        card_pop = card.popleft()
        card.append(card_pop)

# 첫째 줄에 버리는 카드들을 순서대로 출력한다. 
# 제일 마지막에는 남게 되는 카드의 번호를 출력한다.
# 덱으로 묶여있던 out 객체를 * 표기로 풀어서 print
print(*out)
```



#### 2902. KMP는 왜 KMP일까? [(link)](https://www.acmicpc.net/problem/2902)

> KMP 알고리즘이 KMP인 이유는 이를 만든 사람의 성이 Knuth, Morris, Prett이기 때문이다. 이렇게 알고리즘에는 발견한 사람의 성을 따서 이름을 붙이는 경우가 많다.
>
> 또 다른 예로, 유명한 비대칭 암호화 알고리즘 RSA는 이를 만든 사람의 이름이 Rivest, Shamir, Adleman이다.
>
> 사람들은 이렇게 사람 성이 들어간 알고리즘을 두 가지 형태로 부른다.
>
> - 첫 번째는 성을 모두 쓰고, 이를 하이픈(-)으로 이어 붙인 것이다. 예를 들면, Knuth-Morris-Pratt이다. 이것을 긴 형태라고 부른다.
> - 두 번째로 짧은 형태는 만든 사람의 성의 첫 글자만 따서 부르는 것이다. 예를 들면, KMP이다.
>
> 동혁이는 매일매일 자신이 한 일을 모두 메모장에 적어놓는다. 잠을 자기 전에, 오늘 하루 무엇을 했는지 되새겨 보는 것으로 하루를 마감한다.
>
> 하루는 이 메모를 보던 중, 지금까지 긴 형태와 짧은 형태를 섞어서 적어 놓은 것을 발견했다.
>
> 이렇게 긴 형태로 하루 일을 기록하다가는 메모장 가격이 부담되어 파산될 것이 뻔하기 때문에, 앞으로는 짧은 형태로 기록하려고 한다.
>
> 긴 형태의 알고리즘 이름이 주어졌을 때, 이를 짧은 형태로 바꾸어 출력하는 프로그램을 작성하시오.

```python
import sys
sys.stdin = open("2902_input.txt")

# 긴 형태의 알고리즘 이름이 주어졌을 때, 
# 이를 짧은 형태로 바꾸어 출력하는 프로그램을 작성하시오.

# "-" 로 구분되는 긴 이름 입력
name = list(input().split("-"))

# 짧아진 이름 붙여줄 변수 선언
short_name = ""

for i in name:

    # "-" 이후 첫번째로 등장하는 문자들을 short_name 에 붙이기
    short_name += i[0]        

print(short_name)
```



#### 9012. 괄호 [(link)](https://www.acmicpc.net/problem/9012)

> 괄호 문자열(Parenthesis String, PS)은 두 개의 괄호 기호인 ‘(’ 와 ‘)’ 만으로 구성되어 있는 문자열이다. 그 중에서 괄호의 모양이 바르게 구성된 문자열을 올바른 괄호 문자열(Valid PS, VPS)이라고 부른다. 한 쌍의 괄호 기호로 된 “( )” 문자열은 기본 VPS 이라고 부른다. 만일 x 가 VPS 라면 이것을 하나의 괄호에 넣은 새로운 문자열 “(x)”도 VPS 가 된다. 그리고 두 VPS x 와 y를 접합(concatenation)시킨 새로운 문자열 xy도 VPS 가 된다. 예를 들어 “(())()”와 “((()))” 는 VPS 이지만 “(()(”, “(())()))” , 그리고 “(()” 는 모두 VPS 가 아닌 문자열이다. 
>
> 여러분은 입력으로 주어진 괄호 문자열이 VPS 인지 아닌지를 판단해서 그 결과를 YES 와 NO 로 나타내어야 한다. 

```python
import sys
sys.stdin = open("9012_input.txt")

# 테스트 케이스의 수
tc = int(input())

for i in range(tc):

    # '(' 와 ')' 로 이루어진 자료 input
    input_bracket = input()

    # '(' + ')' 모양이 완성되었을 때 이를 담아줄 리스트 생성
    done = []

    for j in input_bracket:

        # 괄호 열기'(' 는 done 에 일단 넣어줌
        if j == "(":
            done.append(j)

        # 괄호 닫기')' 는 done 을 검사
        elif j == ")":

            # 검사결과 done 이 비어있지 않으면 pop
            # 괄호열기 + 괄호닫기 완성의 결과가 pop 이므로
            if done:
                done.pop()

            # 검사결과 done 이 빈 상태면 "NO" 출력
            else:
                print("NO")
                break
    
    # 위의 for 문에서 break 발생한 적이 없으면?
    else:
        
        # 반복문 연산 결과 done 이 최종적으로 비어있는 상태라면
        # 짝이 모두 맞아 떨어져서 pop 된 상태기 때문에 "YES" 프린트
        if not done:
            print("YES")

        # done 안에 여전히 뭔가가 남아있으면 짝이 맞지 않으니 "NO" 프린트
        else:
            print("NO")
```



#### 10546. 배부른 마라토너 [(link)](https://www.acmicpc.net/problem/10546)

> 마라토너라면 국적과 나이를 불문하고 누구나 참가하고 싶어하는 백준 마라톤 대회가 열린다. 42.195km를 달리는 이 마라톤은 모두가 참가하고 싶어했던 만큼 매년 모두가 완주해왔다. 단, 한 명만 빼고! 
>
> 모두가 참가하고 싶어서 안달인데 이런 백준 마라톤 대회에 참가해 놓고 완주하지 못한 배부른 참가자 한 명은 누굴까?

```python
import sys
from collections import defaultdict

sys.stdin = open("10546.txt")

n = int(input())

ans = defaultdict(int)

for _ in range(n):
    input_ = input().rstrip()
    ans[input_] += 1

for _ in range(n-1):
    fin_ = input().rstrip()
    ans[fin_] -= 1

for k, v in ans.items():
    if v == 1:
        print(k)
```



#### 14720. 우유 축제 [(link)](https://www.acmicpc.net/problem/14720)

> 영학이는 딸기우유, 초코우유, 바나나우유를 좋아한다.
>
> 입맛이 매우 까다로운 영학이는 자신만의 우유를 마시는 규칙이 있다.
>
> 1. 맨 처음에는 딸기우유를 한 팩 마신다.
> 2. 딸기우유를 한 팩 마신 후에는 초코우유를 한 팩 마신다.
> 3. 초코우유를 한 팩 마신 후에는 바나나우유를 한 팩 마신다.
> 4. 바나나우유를 한 팩 마신 후에는 딸기우유를 한 팩 마신다. 
>
> 영학이는 우유 축제가 열리고 있는 우유거리에 왔다. 우유 거리에는 우유 가게들이 일렬로 늘어서 있다.
>
> 영학이는 우유 거리의 시작부터 끝까지 걸으면서 우유를 사먹고자 한다.
>
> 각각의 우유 가게는 딸기, 초코, 바나나 중 한 종류의 우유만을 취급한다.
>
> 각각의 우유 가게 앞에서, 영학이는 우유를 사마시거나, 사마시지 않는다.
>
> 우유거리에는 사람이 많기 때문에 한 번 지나친 우유 가게에는 다시 갈 수 없다.
>
> 영학이가 마실 수 있는 우유의 최대 개수를 구하여라.

```python
import sys
sys.stdin = open("14720.txt")

# 딸기(0) - 초코(1) - 바나나(2) - 딸기(0)
# 한 번 지나친 우유 가게는 다시 갈 수 없음
# 영학이가 마실 수 있는 우유의 최대 개수는?

# 우유 가게의 개수
n = int(input())

# 우유 가게의 정보
s = list(map(int, input().split()))

cnt = 0

for i in range(n):
    if s[i] == cnt % 3:
        cnt += 1

print(cnt)
```



#### 20001. 고무오리 디버깅 [(link)](https://www.acmicpc.net/problem/20001)

> 백준 문제 풀이에 힘들어하는 수진이를 위해 민우는 문제해결에 도움이 되는 고무오리를 준비했다. 민우가 준비한 고무오리는 신비한 능력이 존재하는데, 최근에 풀던 백준 문제를 해결해주는 능력이다. 신비한 고무오리와 함께 수진이의 백준 풀이를 도와주자!
>
> 고무오리의 사용법은 다음과 같다.
>
> - "고무오리 디버깅 시작" 이라고 외친다
> - 문제들을 풀기 시작한다
> - 고무오리를 받으면 최근 풀던 문제를 해결한다
> - "고무오리 디버깅 끝" 이라고 외치면 문제풀이를 종료한다.
>
> 하지만 고무오리에는 치명적인 문제가 있는데, 풀 문제가 없는데 사용한다면 고무오리는 벌칙으 로 두 문제를 추가한다는 점이다.

```python
import sys
sys.stdin = open("20001.txt", "r", encoding="UTF-8")

list_ = []
 
while True:
    s = input()

    if s == '문제':
        list_.append(1)

    elif s == '고무오리':
        if not list_:
            list_.append(1)
            list_.append(1)
        else:
            list_.pop()
            
    elif s == '고무오리 디버깅 끝':
        break
 
if not list_:
    print('고무오리야 사랑해')
else:
    print('힝구')
```

