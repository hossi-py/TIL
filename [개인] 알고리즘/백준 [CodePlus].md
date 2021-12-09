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

