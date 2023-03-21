```ad-note
title: Complexidade
collapse: true

- $O(V + E)$
```

```cpp
vector<int> g[MAXN];
bool visited[MAXN];

void DFS(int i) {
    visited[i] = true;

	for(int n : g[i]) {
		if (!visited[n]) {
			DFS(n);
		}
	}
}
```

---