> [!info] Objetivo
> - Tem como objetivo calcular as componentes conexas de um grafo bidirecional.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
vector<vector<int>> g;
vector<int> component;

void dfs(int u, int c) {
	component[u] = c;

	for (int to : g[u]) {
		if (component[to] == -1) {
			dfs(to, c);
		}
	}
}

// The graph must be 0-indexed
int cc(int n) {
	component.assign(n, -1);
	
	int comp {};

	for (int i {}; i < n; ++i) {
		if (component[i] == -1) {
			dfs(i, comp++);
		}
	}

	return comp;
}
```

---