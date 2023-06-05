> [!info] Objetivo
> - Fazer a travessia em um grafo.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
// MAXN is the largest possible number of nodes
vector<int> g[MAXN];
bitset<MAXN> visited;

void dfs(int i) {
    visited[i] = true;

	for(int n : g[i]) {
		if (!visited[n]) {
			dfs(n);
		}
	}
}
```

---