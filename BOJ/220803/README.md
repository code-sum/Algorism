# 📌2022-08-03 BOJ 풀이



#### 1100. 하얀 칸

> 체스판은 8×8크기이고, 검정 칸과 하얀 칸이 번갈아가면서 색칠되어 있다. 가장 왼쪽 위칸 (0,0)은 하얀색이다. 체스판의 상태가 주어졌을 때, 하얀 칸 위에 말이 몇 개 있는지 출력하는 프로그램을 작성하시오.

```python
import sys
sys.stdin = open("1100.txt")

matrix = []
for _ in range(8):
    matrix.append(list(input()))

cnt = 0
for i in range(8):
    for j in range(8):
        if matrix[i][j] == 'F' and (i + j) % 2 == 0:
            cnt += 1

print(cnt)
```



