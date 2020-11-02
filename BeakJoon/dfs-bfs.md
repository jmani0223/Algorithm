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
```
### 2606

```c
#include <iostream>
using namespace std;

#define MAX_VALUE 1001
#define start 1

int map[MAX_VALUE][MAX_VALUE];
int visit[MAX_VALUE];
int n, m, x, y, count =0;

void dfs(int v){
	visit[v] = 1; 
	count +=1;
	for(int i=1; i<=n; i++){
		if(visit[i]==1 || map[v][i]==0)
			continue;
		dfs(i);
	}
}
int main() {
	cin >> n >> m;
	int i=0;
	for(i=0; i<m; i++){
		cin >> x >> y;
		map[x][y] = map[y][x] = 1;
	}
	dfs(start);
	cout << count-1; 
	return 0;
}
```
### 2667

```c
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
using namespace std;

#define MAX_VALUE 25
int map[MAX_VALUE][MAX_VALUE];
int visit[MAX_VALUE][MAX_VALUE];
int dx[4]={-1,1,0,0}; //4방
int dy[4]={0,0,1,-1};
int cnt=0, n;

vector<int> cnt_vec;

void dfs(int x, int y){
	cnt++;
	visit[x][y]=true;
	
	for(int i=0; i<4; i++){
		int nx=x+dx[i]; //현재 자리에서 위, 아래, 옆
		int ny=y+dy[i];
		if(nx < 0 || nx >= n || ny < 0 || ny >= n) //배열의 범주를 벗어났다면
			continue;
		if(map[nx][ny]==1 && visit[nx][ny]==false) //가야할 곳이고 안가봤다면
			dfs(nx, ny);
	}
}

int main() {
	//입력값 처리
	string input;
	cin >> n;
	for(int i=0; i<n; i++){
		for(int j=0; j<n; j++){
			scanf("%1d", &map[i][j]);
		}
	}
	
	//solution
	for(int i=0; i<n; i++){
		for(int j=0; j<n; j++){
			if(map[i][j]==1 && visit[i][j]==false){ //가야할 곳(1)이거나 안가본 곳이라면(이전 단지는 안가야함)
				cnt=0;
				dfs(i,j);
				cnt_vec.push_back(cnt);
			}
		}
	}
	
	//출력값 처리
	sort(cnt_vec.begin(), cnt_vec.end());
	cout << cnt_vec.size() << endl;
	for(int i=0;i<cnt_vec.size(); i++){
		cout << cnt_vec[i]<< endl;
	}
	return 0;
}
```
