## 프로그래머스 : 네트워크

---

처음 푼 코드
- 문제점
  - DFS/BFS를 사용하지 않음
  - 직접 연결된 컴퓨터만 고려해서 간접적인 연결을 놓칠 수 있음 ( 하지만 프로그래머스가 통과 시켜줌 )
  - 기존 데이터 구조가 파괴됨
  - 시간 복잡도 쩜
```python
def solution(n, computers):
    # 각 컴퓨터가 연결된 컴퓨터의 인덱스를 집합 형태로 저장
    computers = [{idx for idx, value in enumerate(computer) if value == 1} for computer in computers]
    print(computers)  # 연결 상태를 출력
    
    for idx, computer in enumerate(computers):
        for target_idx in range(n):
            if idx == target_idx:
                continue  # 자기 자신과의 비교는 건너뛰기
                
            # 두 컴퓨터가 서로 연결된 경우 두 컴퓨터의 연결 정보를 합침
            if computers[idx] & computers[target_idx]:
                computers[idx] |= computers[target_idx]
                computers[target_idx] = set()  # 합친 후에는 다른 집합을 비워줌
                
    # 비어 있지 않은 집합의 개수를 계산, 즉 네트워크의 개수
    result = sum(1 for out in computers if out != set())
    return result
```
---

두번째 푼 코드
- 문제점
  - 완벽함
- 변경점
  - DFS를 통해 탐색을 한다

```python
def solution(n, computers):
    def dfs(v):
        # 현재 노드를 방문 처리
        visited[v] = True
        # 모든 컴퓨터에 대해 반복
        for i in range(n):
            # 현재 노드와 연결되어 있고 아직 방문하지 않은 노드라면
            if computers[v][i] == 1 and not visited[i]:
                # 해당 노드로 DFS 재귀 호출
                dfs(i)
    
    # 방문 여부를 추적하는 리스트 초기화
    visited = [False] * n
    
    # 네트워크의 수를 카운트할 변수 초기화
    cnt = 0
    
    # 모든 컴퓨터에 대해 반복
    for i in range(n):
        # 아직 방문하지 않은 컴퓨터라면
        if not visited[i]:
            # 해당 컴퓨터에서 DFS 시작
            dfs(i)
            # 새로운 네트워크를 발견했으므로 카운트 증가
            cnt += 1
    
    # 발견된 총 네트워크의 수 반환
    return cnt
```

---
# 소감
나는 많이 바보다