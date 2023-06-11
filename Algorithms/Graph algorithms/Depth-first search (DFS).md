> [!info] Objetivo
> - Fazer a travessia em um grafo.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
// MAXN is the largest possible number of nodes
vector<int> g[MAXN];
bitset<MAXN> visited;

void dfs(int u) {
    visited[u] = true;

	for(int to : g[i]) {
		if (!visited[to]) {
			dfs(to);
		}
	}
}
```

---