> [!info] Objetivo
> - Tem como objetivo fazer a travessia em um grafo utilizando busca em profundidade.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
vector<vector<int>> g;
vector<bool> visited;

// The graph must be 0-indexed
void dfs(int u) {
    visited[u] = true;

	for(int to : g[u]) {
		if (!visited[to]) {
			dfs(to);
		}
	}
}

// Call it before call the setup
void setup(int n) {
	visited.assign(n, false);
}
```

---