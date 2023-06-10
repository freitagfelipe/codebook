> [!info] Objetivo
> - Calcular as componentes conexas de um grafo bidirecional.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
// MAXN is the largest possible number of nodes
int n;
vector<int> g[MAXN], component(MAXN, -1);

void dfs(int v, int c) {
	component[v] = c;

	for (int u : g[v]) {
		if (component[u] == -1) {
			dfs(u, c);
		}
	}
}

int cc() {
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