> [!info] Objetivo
> - Encontrar todos os vértices de um grafo que se removidos causariam a criação de uma ou mais componente conexas.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
int n, timer {};
// MAXN is the largest possible number of nodes
vector<int> g[MAXN], tin(MAXN, 0), low(MAXN, 0);
bitset<MAXN> visited, is_articulation_point;

void dfs(int u, int p = -1) {
    visited[u] = true;

    tin[u] = low[u] = ++timer;

    int children {};

    for (int to : g[u]) {
        if (to == p) {
            continue;
        }

        if (visited[to]) {
            low[u] = min(low[u], tin[to]);
        } else {
            dfs(to, u);

            low[u] = min(low[u], low[to]);

            if (low[to] >= tin[u] && p != -1) {
                is_articulation_point[u] = true;
            }

            ++children;
        }
    }

    if (p == -1 && children > 1) {
        is_articulation_point[u] = true;
    }
}

void find_articulation_points() {
	for (int i {}; i < n; ++i) {
		if (!visited[i]) {
			dfs(i);
		}
	}
}
```

---