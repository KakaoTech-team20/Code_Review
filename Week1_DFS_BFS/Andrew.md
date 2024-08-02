## 프로그래머스 : 네트워크

---

설명
- DFS/BFS 특성을 활용할 필요 없이, 네트워크의 수만 구하면 되었기 때문에 둘 다 사용 가능하다고 판단
- BFS가 DFS보다는 일반적인 경우에 수행시간이 좋기 때문에, BFS 사용
- 인접 행렬 방식으로 그래프 정보가 주어졌기 때문에, queue에서 꺼내온 노드와 연결된 노드를 확인하기 위해서는 인접행렬을 range(n)을 통해 전체적으로 훑으면서 해당 노드와의 연결을 확인해야 함
- bfs 함수를 solution 함수 내에 넣어서 구현하는 방식도 존재함

```python
from collections import deque

def bfs(n, computers, i, visited):
    queue = deque([i])
    while queue:
        com = queue.popleft()
        visited[com] = True
        for k in range(n):
            if computers[com][k] and not visited[k]:
                queue.append(k)
    
def solution(n, computers):
    answer = 0
    
    visited = [False] * n
    for i in range(n):
        if not visited[i]:
            bfs(n, computers, i, visited)
            answer += 1
            
    return answer
```

# 소감
그래프 형식이 `인접 리스트` 방식이 아니라 `인접 행렬` 방식으로 주어져도, 기본 알고리즘을 활용해 구현할 수 있도록 연습을 해야겠다!
