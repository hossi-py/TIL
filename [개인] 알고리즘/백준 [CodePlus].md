# 백준 [CodePlus]

[TOC]

## 10430. 나머지

```python
# 10430. 나머지
A, B, C = map(int, input().split())

print((A + B) % C)
print(((A % C) + (B % C)) % C)
print((A * B) % C)
print(((A % C) * (B % C)) % C)

```

## 4375. 1

```python
# 4375. 1
import sys

while True:
    n = sys.stdin.readline().rstrip()

    if n == '':
        break

    n = int(n)

    a = '11'

    if n == 1:
        print(1)

    else:

        while True:

            if int(a) % n == 0:
                print(len(a))
                break

            else:
                a += '1'

```

> 시간 단축

```python
# 4375. 1
import sys


def check(n):
    mul = 1

    while mul % n != 0:
        mul = mul * 10 + 1

    return len(str(mul))


while True:
    n = sys.stdin.readline().rstrip()

    if n == '':
        break

    n = int(n)

    print(check(n))

```



## 1037. 약수

```python
# 1037. 약수
import sys

N = int(input())    # 약수의 개수

nums = list(map(int, input().split()))  # 진짜 약수

nums.sort()

if len(nums) % 2 == 0:
    print(nums[0] * nums[-1])

else:
    print(nums[len(nums) // 2] ** 2)
```



## 17427. 약수의 합 2

```python
# 17427. 약수의 합 2

# 약수 구하기
_max = 1000000

N = int(input())

f = [1] * (_max + 1)   # f[i] = 자연수 i의 약수의 합

g = [0] * (_max + 1)   # g[i] = i까지 약수의 합

for i in range(2, _max + 1):
    j = 1

    # i부터 max 까지 i의 배수인 부분에 i를 더해준다.
    while i * j <= _max:
        f[i * j] += i
        j += 1

for i in range(1, N + 1):
    g[i] = g[i - 1] + f[i]

print(g[N])

```



## 2609. 최대공약수와 최소공배수

```python
# 2609. 최대공약수와 최소공배수
from math import gcd
num1, num2 = map(int, input().split())

# 최대공약수
_gcd = gcd(num1, num2)

# 최소공배수
n_num1, n_num2 = num1 // _gcd, num2 // _gcd

print(_gcd)

print(_gcd * n_num1 * n_num2)
```



## 1978. 소수 찾기

```python
# 1978. 소수 찾기

# 소수판정
def prime_check(n):
    global prime

    for i in range(2, n + 1):
        if prime[i] == True:    # 만약 소수이면
            # 배수는 소수가 아님
            for j in range(2 * i, n + 1, i):
                prime[j] = False

    return prime


N = int(input())

nums = list(map(int, input().split()))

prime = [False, False] + [True] * (max(nums) - 1)

n = max(nums)

prime_check(n)

cnt = 0
for i in range(N):
    if prime[nums[i]] == True:
        cnt += 1
        
print(cnt)

```



## 1929. 소수 구하기

```python
# 1929. 소수 구하기
M, N = map(int, input().split())

prime = [False, False] + [True] * (N - 1)

for i in range(2, N + 1):
    if prime[i] == True:
        for j in range(2 * i, N + 1, i):
            prime[j] = False

for i in range(M, N + 1):
    if prime[i] == True:
        print(i)

```



## 6588. 골드바흐의 추측

```python
# 6588. 골드바흐의 추측
import sys
# 4보다 큰 모든 짝수는 두 홀수 소수의 합으로 나타낼 수 있다.

_max = 1000000

prime = [False, False] + [True] * (_max - 1)

for i in range(2, int(_max ** 0.5) + 1):
    if prime[i] == True:
        for j in range(2 * i, _max + 1, i):
            prime[j] = False

while True:
    N = int(sys.stdin.readline().rstrip())

    if N == 0:
        break

    flag = False

    for i in range(3, _max):
        if prime[i] == True:
            # 첫 소수에서 주어진 수와 그 소수를 뺀 수가 소수일 때
            if prime[N - i] == True:
                print("%d = %d + %d" % (N, i, N-i))
                flag = True
                break

    if flag == False:
        print("Goldbach's conjecture is wrong.")
```



## 2309. 일곱 난쟁이

```python
# 2309. 일곱 난쟁이
from itertools import combinations

dwarf = []

for i in range(9):
    dwarf.append(int(input()))

dwarf.sort()

combi = set(combinations(dwarf, 7))

for com in combi:
    _sum = sum(com)
    if _sum == 100:
        answer = com

for c in answer:
    print(c)
```

## 1748. 수 이어쓰기 1

```python
# 1748. 수 이어 쓰기1

# 1 - 9 : 길이 1
# 10 - 99 : 길이 2
# 100 - 999 : 길이 3

N = int(input())

nines = [int('9' + '0' * i) for i in range(0, len(str(N)))]

result = 0

for i, s in enumerate(nines):
    if s == nines[-1]:  # 마지막 자릿수를 계산
        result += len(str(s)) * (N - sum(nines[:-1]))

    else:
        i += 1
        result += i * s

print(result)
```



## 9095. 1, 2, 3 더하기

```python
# 9095. 1, 2, 3 더하기
T = int(input())

dp = [0, 1, 2, 4] + [0] * 7

for i in range(4, 11):
    dp[i] = dp[i - 1] + dp[i - 2] + dp[i - 3]

for tc in range(1, T + 1):
    n = int(input())

    print(dp[n])
```



## 15650. N과 M (2)

```python
# 15650. N과 M (2)
N, M = map(int, input().split())

# 1부터 N까지 자연수 중에서 중복 없이 2개를 고른 수열

from itertools import permutations

nums = [i for i in range(1, N + 1)]

if M == 1:
    for n in nums:
        print(n)

else:
    result = []
    per = permutations(nums, M)

    for row in per:
        row = list(row)
        row.sort()

        if row not in result:
            result.append(row)

    for res in result:
        print(*res)

```

```python
# 15650. N과 M (2)
N, M = map(int, input().split())


def dfs(start, N, M, result):
    if len(result) == M:
        print(*result)
        return

    for i in range(start, N + 1):
        if i not in result:
            result.append(i)
            dfs(i, N, M, result)
            result.pop()


dfs(1, N, M, [])
```



## 15651. N과 M (3)

```python
# 15651. N과 M (3)
N, M = map(int, input().split())


def dfs(start, N, M, result):
    if len(result) == M:
        print(*result)
        return

    for i in range(1, N + 1):
        result.append(i)
        dfs(1, N, M, result)
        result.pop()


dfs(1, N, M, [])
```



## 15652. N과 M (4)

```python
# 15652. N과 M (4)
N, M = map(int, input().split())


def dfs(start, N, M, result):
    if len(result) == M:
        print(*result)
        return

    for i in range(start, N + 1):
        result.append(i)
        dfs(i, N, M, result)
        result.pop()


dfs(1, N, M, [])
```



## 15654. N과 M (5)

```python
# 15654. N과 M (5)
def dfs(start, N, M, result):
    if len(result) == M:
        print(*result)
        return

    for i in range(start, len(nums)):
        if nums[i] not in result:
            result.append(nums[i])

            dfs(0, N, M, result)

            result.pop()


N, M = map(int, input().split())

nums = list(map(int, input().split()))

nums.sort()

dfs(0, N, M, [])

```



## 15655. N과 M (6)

```python
# 15655. N과 M (6)
def dfs(start, N, M, result):
    if len(result) == M:
        print(*result)
        return

    for i in range(start, len(nums)):
        if nums[i] not in result:
            result.append(nums[i])

            dfs(i, N, M, result)

            result.pop()


N, M = map(int, input().split())

nums = list(map(int, input().split()))

nums.sort()

dfs(0, N, M, [])

```



## 15656. N과 M (7)

```python
# 15656. N과 M (7)
def dfs(start, N, M, result):
    if len(result) == M:
        print(*result)
        return

    for i in range(start, len(nums)):

        result.append(nums[i])

        dfs(0, N, M, result)

        result.pop()


N, M = map(int, input().split())

nums = list(map(int, input().split()))

nums.sort()

dfs(0, N, M, [])

```



## 15657. N과 M (8)

```python
# 15657. N과 M (8)
def dfs(start, N, M, result):
    if len(result) == M:
        print(*result)
        return

    for i in range(start, len(nums)):

        result.append(nums[i])

        dfs(i, N, M, result)

        result.pop()


N, M = map(int, input().split())

nums = list(map(int, input().split()))

nums.sort()

dfs(0, N, M, [])

```



## 1759. 암호 만들기

```python
# 1759. 암호 만들기
def dfs(start, L, C, result):
    global c_count, v_count

    if len(result) == L:
        c_count, v_count = 0, 0

        for i in range(L):
            if result[i] in vowel:
                v_count += 1
            else:
                c_count += 1

        if c_count >= 2 and v_count >= 1:
            for res in result:
                print(res, end='')
            print()
        return

    for i in range(start, C):
        if alpha[i] not in result:
            result.append(alpha[i])

            dfs(i, L, C, result)

            result.pop()


L, C = map(int, input().split())    # L자리의 패스워드 / C개의 알파벳

alpha = list(input().split())

alpha.sort()

vowel = ['a', 'i', 'e', 'o', 'u']

c_count, v_count = 0, 0

dfs(0, L, C, [])

```



## 14889. 스타트와 링크

```python
import sys
from itertools import combinations

# 14889. 스타트와 링크
N = int(input())
board = [list(map(int, input().split())) for _ in range(N)]

players = [x for x in range(N)]
teams = []

for team in list(combinations(players, N // 2)):
    teams.append(team)

_min = float("inf")

for i in range(len(teams) // 2):
    start = teams[i]
    start_stat = 0  # start 팀 능력치

    for j in range(len(start)):
        player = start[j]

        for k in start:
            start_stat += board[player][k]

    link = teams[-i - 1]
    link_stat = 0   # link 팀 능력치

    for j in range(len(link)):
        player = link[j]

        for k in link:
            link_stat += board[player][k]

    temp = abs(start_stat - link_stat)

    if temp < _min:
        _min = temp

print(_min)

```



## 15661. 링크와 스타트

```python
import sys
from itertools import combinations

# 15661. 링크와 스타트
N = int(input())
board = [list(map(int, input().split())) for _ in range(N)]

players = [x for x in range(N)]
teams = []

for i in range(2, N - 1):
    for team in combinations(players, i):
        teams.append(team)

_min = float("inf")

for i in range(len(teams) // 2):
    start = teams[i]
    start_stat = 0  # start 팀 능력치

    for j in range(len(start)):
        player = start[j]

        for k in start:
            start_stat += board[player][k]

    link = teams[-i - 1]
    link_stat = 0   # link 팀 능력치

    for j in range(len(link)):
        player = link[j]

        for k in link:
            link_stat += board[player][k]

    temp = abs(start_stat - link_stat)

    if temp < _min:
        _min = temp

print(_min)

```

