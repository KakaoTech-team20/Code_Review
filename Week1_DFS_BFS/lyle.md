## DFS 
### 네트워크 구성 수 구하기

```python
def solution(n, computers):

    visited = [False for _ in range(n)]
    result = 0
    def dfs(node):
        visited[node] = True

        for nextNode in range(n): # 연결된 다른 노드 탐색
            if computers[node][nextNode] == 1 and not visited[nextNode]:
            # 연결되어 있는데 방문하지 않았다면
                dfs(nextNode)


    for i in range(n): #모든 노드를 확인
        if not visited[i]: #방문하지 않은 노드라면
            dfs(i)
            result += 1

    return result
```

1. 방문 기록 노드 리스트 생성
2. 첫번째 노드를 탐색
-> 2-1. 인접 노드가 있으면 해당 노드 탐색
3. 다음 노드 탐색
-> 3-1. 방문하지 않은 노드가 있으면 탐색
4. 새롭게 탐색한 횟수를 리턴
- 맨 처음 배열이 [x,y,z]로 구성되어 있어 [x,y]가 z이면 노드가 연결되어 있는 것으로 해석하여 문제 풀이가 어려움이 있었다.
- 인접행렬을 사용
- 시간 복잡도 n^2
