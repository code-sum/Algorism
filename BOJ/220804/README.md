# 📌2022-08-04 BOJ 풀이



#### 1547. 공 [(link)](https://www.acmicpc.net/problem/1547)

> 세준이는 컵 3개를 탁자 위에 일렬로 엎어놓았다. 컵의 번호는 맨 왼쪽 컵부터 순서대로 1번, 2번 3번이고, 세준이는 이 컵을 이용해서 게임을 하려고 한다.
>
> 먼저 1번 컵의 아래에 공을 하나 넣는다. 세준이는 두 컵을 고른 다음, 그 위치를 맞바꾸려고 한다. 예를 들어, 고른 컵이 1번과 2번이라면, 1번 컵이 있던 위치에 2번 컵을 이동시키고, 동시에 2번 컵이 있던 위치에 1번 컵을 이동시켜야 한다. 이때 공은 움직이지 않기 때문에, 공의 위치는 맨 처음 1번 컵이 있던 위치와 같다.
>
> 세준이는 컵의 위치를 총 M번 바꿀 것이며, 컵의 위치를 바꾼 방법이 입력으로 주어진다. 위치를 M번 바꾼 이후에 공이 들어있는 컵의 번호를 구하는 프로그램을 작성하시오.

```python
import sys
sys.stdin = open("1547.txt")

t = int(input())

# 공이 있는 자리 ans
ans = 1

for _ in range(1, t+1):
    a, b = map(int, input().split())
    if a == ans:
        ans = b
    elif b == ans:
        ans = a
    else:
        continue
print(ans)
```



#### 1652. 누울 자리를 찾아라 [(link)](https://www.acmicpc.net/problem/1652)

> 일 년 동안 세계일주를 하던 영식이는 여행을 하다 너무 피곤해서 근처에 있는 코레스코 콘도에서 하룻밤 잠을 자기로 하고 방을 잡았다.
>
> 코레스코 콘도에 있는 방은 NxN의 정사각형모양으로 생겼다. 방 안에는 옮길 수 없는 짐들이 이것저것 많이 있어서 영식이의 누울 자리를 차지하고 있었다. 영식이는 이 열악한 환경에서 누울 수 있는 자리를 찾아야 한다. 영식이가 누울 수 있는 자리에는 조건이 있다. 똑바로 연속해서 2칸 이상의 빈 칸이 존재하면 그 곳에 몸을 양 옆으로 쭉 뻗으면서 누울 수 있다. 가로로 누울 수도 있고 세로로 누울 수도 있다. 누울 때는 무조건 몸을 쭉 뻗기 때문에 반드시 벽이나 짐에 닿게 된다. (중간에 어정쩡하게 눕는 경우가 없다.)
>
> ![img](https://www.acmicpc.net/JudgeOnline/upload/201005/map.PNG)
>
> 만약 방의 구조가 위의 그림처럼 생겼다면, 가로로 누울 수 있는 자리는 5개이고, 세로로 누울 수 있는 자리는 4개 이다. 방의 크기 N과 방의 구조가 주어졌을 때, 가로로 누울 수 있는 자리와 세로로 누울 수 있는 자리의 수를 구하는 프로그램을 작성하시오.

```python
import sys
sys.stdin = open("1652.txt")

'''
5
....X
..XX.
.....
.XX..
X....
5 4
'''

# 첫째 줄에 방의 크기 N이 주어진다.
n = int(input())

matrix = []
r, c = 0, 0
cnt = 0

# input 받기
for _ in range(n):
    matrix.append(list(input()))

# 가로 누울 자리 세기
for i in range(n):
    cnt = 0
    for j in range(n):
        if matrix[i][j] == ".":
            cnt += 1
        else:
            cnt = 0
        if cnt == 2:
            r += 1

# 세로 누울 자리 세기
for i in range(n):
    cnt = 0
    for j in range(n):
        if matrix[j][i] == ".":
            cnt += 1
        else:
            cnt = 0
        if cnt == 2:
            c += 1

print(r, c)
```



#### 2592. 대표값 [(link)](https://www.acmicpc.net/problem/2592)

> 어떤 수들이 있을 때, 그 수들을 대표하는 값으로 가장 흔하게 쓰이는 것은 평균이다. 평균은 주어진 모든 수의 합을 수의 개수로 나눈 것이다. 예를 들어 10, 40, 30, 60, 30, 20, 60, 30, 40, 50의 평균은 (10 + 40 + 30 + 60 + 30 + 20 + 60 + 30 + 40 + 50) / 10 = 370 / 10 = 37이 된다.
>
> 평균 이외의 또 다른 대표값으로 최빈값이라는 것이 있다. 최빈값은 주어진 수들 가운데 가장 많이 나타나는 수이다. 예를 들어 10, 40, 30, 60, 30, 20, 60, 30, 40, 50이 주어질 경우, 30이 세 번, 40과 60이 각각 두 번, 10, 20, 50이 각각 한 번씩 나오므로, 최빈값은 30이 된다.
>
> 열 개의 자연수가 주어질 때 이들의 평균과 최빈값을 구하는 프로그램을 작성하시오.

```python
import sys
sys.stdin = open("2592.txt")

dic = {}
avg_ = 0

for i in range(10):
    n = int(input())

    avg_ += n
    if n not in dic:
        dic[n] = 1
    else:
        dic[n] += 1

print(avg_//10)

# 딕셔너리에서 최대 value 를 갖는 key 찾는 코드
max_k = max(dic, key=dic.get)
print(max_k)
```



#### 2669. 직사각형 네개의 합집합의 면적 구하기 [(link)](https://www.acmicpc.net/problem/2669)

> 평면에 네 개의 직사각형이 놓여 있는데 그 밑변은 모두 가로축에 평행하다. 이 네 개의 직사각형들은 서로 떨어져 있을 수도 있고, 겹쳐 있을 수도 있고, 하나가 다른 하나를 포함할 수도 있으며, 변이나 꼭짓점이 겹칠 수도 있다.
>
> 이 직사각형들이 차지하는 면적을 구하는 프로그램을 작성하시오.
>
> ![img](https://www.acmicpc.net/upload/images/8vR77Ew2O2PqvZ1lER716.png)

```python
import sys
sys.stdin = open("2669.txt")

'''
1 2 4 4
2 3 5 7
3 1 6 5
7 3 8 6
26
'''

# 입력은 네 줄이며, 각 줄은 직사각형의 위치를 나타내는 네 개의 정수
# 첫 번째와 두 번째의 정수는 사각형의 왼쪽 아래 꼭짓점의 x좌표, y좌표
# 세 번째와 네 번째의 정수는 사각형의 오른쪽 위 꼭짓점의 x좌표, y좌표

# 0을 100 X 100 matrix 에 채워넣기
matrix = []
for _ in range(100):
    matrix.append([0]*100)

# 문제에서 주어진 직사각형 4개의 영역을 0 -> 1 값으로 매핑하기
for _ in range(4):
    x1, y1, x2, y2 = map(int, input().split(" "))
    for i in range(x1, x2):
        for j in range(y1, y2):
            matrix[i][j] = 1

# 0 과 1로만 이루어진 matrix 위의 모든 값을 더하기
cnt = 0
for blocks in matrix:
    cnt += sum(blocks)

print(cnt)
```



#### 2693. N번째 큰 수 [(link)](https://www.acmicpc.net/problem/2693)

> 배열 A가 주어졌을 때, N번째 큰 값을 출력하는 프로그램을 작성하시오.
>
> 배열 A의 크기는 항상 10이고, 자연수만 가지고 있다. N은 항상 3이다.

```python
import sys
sys.stdin = open("2693.txt")

t = int(input())

for _ in range(1, t+1):
    arr = sorted(list(map(int, input().split())), reverse=True)
    
    print(arr[2])
```



#### 3003. 킹, 퀸, 룩, 비숍, 나이트, 폰 [(link)](https://www.acmicpc.net/problem/3003)

> 동혁이는 오래된 창고를 뒤지다가 낡은 체스판과 피스를 발견했다.
>
> 체스판의 먼지를 털어내고 걸레로 닦으니 그럭저럭 쓸만한 체스판이 되었다. 하지만, 검정색 피스는 모두 있었으나, 흰색 피스는 개수가 올바르지 않았다.
>
> 체스는 총 16개의 피스를 사용하며, 킹 1개, 퀸 1개, 룩 2개, 비숍 2개, 나이트 2개, 폰 8개로 구성되어 있다.
>
> 동혁이가 발견한 흰색 피스의 개수가 주어졌을 때, 몇 개를 더하거나 빼야 올바른 세트가 되는지 구하는 프로그램을 작성하시오.

```python
import sys
sys.stdin = open("3003.txt")

a = [1, 1, 2, 2, 2, 8]
c = list(map(int, input().split()))

for i in range(6):
    print(a[i]-c[i], end=' ')
```



#### 4396. 지뢰 찾기 [(link)](https://www.acmicpc.net/problem/4396)

> 지뢰찾기는 n × n 격자 위에서 이루어진다. m개의 지뢰가 각각 서로 다른 격자 위에 숨겨져 있다. 플레이어는 격자판의 어느 지점을 건드리기를 계속한다. 지뢰가 있는 지점을 건드리면 플레이어가 진다. 지뢰가 없는 지점을 건드리면, 그곳의 상하좌우 혹은 대각선으로 인접한 8개의 칸에 지뢰가 몇 개 있는지 알려주는 0과 8 사이의 숫자가 나타난다. 완전히 플레이되지 않은 게임에서 일련의 동작이 아래에 나타나 있다.
>
> ![img](https://www.acmicpc.net/upload/images3/Image1.gif)![img](https://www.acmicpc.net/upload/images3/Image2.gif)![img](https://www.acmicpc.net/upload/images3/Image3.gif) 
>
> 여기서, n은 8이고, m은 10이며, 빈 칸은 숫자 0을 의미하고, 올라가 있는 칸은 아직 플레이되지 않은 위치이며, 별표 모양(*)과 닮은 그림은 지뢰를 의미한다. 맨 왼쪽의 그림은 일부만이 플레이된 게임을 나타낸다. 첫 번째 그림에서 두 번째 그림으로 오면서, 플레이어는 두 번의 이동을 시행해서, 두 번 다 안전한 곳을 골랐다. 세 번째 그림을 볼 때 플레이어는 운이 썩 좋지는 않았다. 지뢰가 있는 곳을 골라서 게임에서 졌다. 플레이어는 m개의 열리지 않은 칸을 남길 때까지 계속해서 안전한 곳을 고르면 이긴다. 그 m개의 칸은 반드시 지뢰이다.
>
> 당신이 할 일은 일부가 플레이된 게임의 정보를 읽어 해당하는 격자를 출력하는 것이다.

```python
import sys

sys.stdin = open("4396.txt")

n = int(input())

graph1 = list(input() for _ in range(n))
graph2 = list(input() for _ in range(n))
ans = [["."] * n for _ in range(n)]

# 열린 칸 주변에 지뢰가 몇 개 있는지 알기 위해, 해당 위치에서 8방향 탐색
dx = [-1, -1, -1, 0, 1, 1, 1, 0]
dy = [-1, 0, 1, 1, 1, 0, -1, -1]


def findBoom():
    for i in range(n):
        for j in range(n):

            if graph1[i][j] == "." and graph2[i][j] == "x":  # 지뢰가 없으면서 열린 칸
                boom = 0
                for k in range(8):
                    nx = i + dx[k]
                    ny = j + dy[k]

                    if nx < 0 or nx >= n or ny < 0 or ny >= n:  # 리스트 좌표 벗어났을때
                        continue

                    if graph1[nx][ny] == "*":
                        boom += 1
                ans[i][j] = boom  # 31번 절의 조건을 통과하지 않아도 boom 적용

            if graph1[i][j] == "*" and graph2[i][j] == "x":  # 지뢰가 있는 칸이 열렸다면
                makeFail()


def makeFail():
    global ans
    for i in range(n):
        for j in range(n):
            if graph1[i][j] == "*":  # 첫번째 입력 중 지뢰가 있는 칸이면
                ans[i][j] = "*"  # 지뢰가 있는 모든 칸을 별표로 표시


findBoom()
for i in range(n):
    for j in range(n):
        print(ans[i][j], end="")
    print()
```

