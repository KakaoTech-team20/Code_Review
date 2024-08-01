## code
``` cpp
#include <vector>
#include <algorithm>

using namespace std;

void dfs(int current ,vector<bool>& isVisited, vector<vector<int>>& computers) {

    // 현재 컴퓨터 위치를 방문 표시
    isVisited[current] = true;
    int n = computers.size();

    for (int i=0; i<n; i++) {
        // 현재 컴퓨터와 연결이 있고 + 방문하지 않은 컴퓨터라면 dfs 실행
        if (computers[current][i] == 1 && !isVisited[i]) {
            dfs(i, isVisited, computers);
        }
    }
}

int solution(int n, vector<vector<int>> computers) {
    int network = 0;
    vector<bool> isVisited(n, false);

    for (int i=0; i<n; i++) {
        // 방문하지 않은 컴퓨터에 대하여 dfs 수행
        if (!isVisited[i]) {
            dfs(i, isVisited, computers);
            // dfs 완료 시 network의 수 +1
            network++;
        }
    }
    return network;
}
```
