### 1260

```c
#include <iostream>
#include <queue>
using namespace std;

#define MAX_VALUE 1001
int mat[MAX_VALUE][MAX_VALUE];
int visit[MAX_VALUE];
int n, m, v, x, y;

void dfs(int v){
	cout << v << ' ';
	visit[v] = 1;
	for(int i=1; i<=n; i++){
		if(visit[i] == 1 || mat[v][i] == 0)
			// 방문했거나 갈 곳이 아니라면 Pass
			continue;
		dfs(i);
	}
}

void bfs(int v){
	queue<int> q;
	q.push(v);
	visit[v]=0; //dfs로 visit가 모두 1이기 때문에
	while(!q.empty()){
		v=q.front();
		cout << q.front() << ' ';;
		q.pop();
		for(int i=1; i<=n; i++){
			if(visit[i]==0 || mat[v][i]==0)
				continue;
			q.push(i);
			visit[i]=0;
		}
	}
}

int main() {
	cin >> n >> m >> v;
	for(int i=1; i<=5; i++){
		cin >> x >> y;
		mat[x][y] = mat[y][x] = 1; //인접행렬
	}
	dfs(v);
	cout << endl;
	bfs(v);
	
	return 0;
}
