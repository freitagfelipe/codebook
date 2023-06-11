> [!info] Objetivo
> - Calcular as componentes conexas de um grafo bidirecional.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
// MAXN is the largest possible number of nodes
int n;
vector<int> g[MAXN], component(MAXN, -1);

void dfs(int u, int c) {
	component[u] = c;

	for (int to : g[u]) {
		if (component[to] == -1) {
			dfs(to, c);
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