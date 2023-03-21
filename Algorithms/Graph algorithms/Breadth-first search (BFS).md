```ad-note
title: Complexidade
collapse: true

- $O(V + E)$
```

```cpp
vector<int> g[MAXN];
bool visited[MAXN];

void BFS(int i) {
	queue<int> q;
	
	q.push(i);
	
	while(!q.empty()) {
		int curr {q.front()};

		q.pop();

        visited[curr] = true;
		
		for(int n : g[curr]) {
			if(!visited[n]) {
				q.push(n);

                visited[n] = true;
			}
		}
	}
}
```

---