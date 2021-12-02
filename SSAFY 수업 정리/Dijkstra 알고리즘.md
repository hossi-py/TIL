# Dijkstra 알고리즘

시작점 주어진다.

각 정점의 시작점에서의 거리 (가중치)

- 만약 직접 갈 수 없으면 무한대 저장

시작점에서 가장 짧게 갈 수 있는 정점을 선택한다.

가능한 모든 경우의 수를 확인하면서 가중치 값의 최대 혹은 최소를 알 수 있다.



## 코드 구현

```python
'''
6 11
0 1 3
0 2 5
1 2 2
1 3 6
2 1 1
2 3 4
2 4 6
3 4 2
3 5 3
4 0 3
4 5 6
'''

V, E = map(int, input().split())
adj = {i:[] for i in range(V)}
for i in range(E):
    n1, n2, c = map(int, input().split())  #시작정점,끝정점,가중치
    adj[n1].append([n2,c])  #도착정점, 가중치
print(adj)
INF = 999999    #큰값
dist = [INF] * V    #각정점의 최단거리(현재까지의)
selected = [False] * V
#시작점 : 0번에서 시작
dist[0] = 0
cnt = 0
while cnt <= V-1:
    #최소값 찾기
    minV = INF
    u = -1
    for i in range(V):
        #아직 최단거리가 결정 안되고, 최소인 정점을 선택
        if not selected[i] and minV > dist[i]:
            minV = dist[i]
            u = i
    selected[u] = True
    cnt += 1
    #간선완화
    for w, cost in adj[u]:       #도착정점, 가중치
        if dist[w] > dist[u] + cost:
            dist[w] = dist[u] + cost
print(dist)
```

