## 프로그래머스 : 네트워크

---

- 접근법
  - DFS 방식으로 탐색
  - n개의 컴퓨터들을 돌면서 해당 컴퓨터번호를 기점으로 2차원 배열을 참고하여 DFS 탐색 수행
  - 방문할때마다 방문여부 visited 배열에 기록하여 중복으로 방문 방지
  - 시간 복잡도 n^2
```java
class Solution {
    public int solution(int n, int[][] computers) {
        int answer = 0;
        int[] visited = new int[n];
        for (int k = 0; k < n; k++){
            if (visited[k]==0){
                dfs(k, visited, computers);
                answer+=1;
            }
        }
        return answer;
    }
    private static void dfs(int start, int[] visited, int[][] computers){
        visited[start] = 1;
        for(int i = 0; i< visited.length; i++){
            if (computers[start][i]==1 && visited[i]==0){
                dfs(i, visited, computers);
            }
        }
    }
}
```
---

- 다른 접근법
  - union-find 알고리즘을 사용하여 네트워크 개수를 구할 수 있습니다.
