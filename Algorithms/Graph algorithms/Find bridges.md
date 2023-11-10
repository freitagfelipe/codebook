> [!info] Objetivo
> - Tem como objetivo encontras as pontes de um grafo, ou seja, as arestas que se removidas fazem com que seja gerado uma nova componente conexa, ou seja, desconectam o grafo.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
typedef pair<int, int> Edge;

int timer;
vector<vector<int>> g;
vector<int> tin, low;
vector<Edge> bridges;
vector<bool> visited;

void dfs(int u, int p = -1) {
    visited[u] = true;

    tin[u] = low[u] = ++timer;

    for (int to : g[u]) {
        if (to == p) {
            continue;
        }

        if (visited[to]) {
            low[u] = min(low[u], tin[to]);
        } else {
            dfs(to, u);

            low[u] = min(low[u], low[to]);

            if (low[to] > tin[u]) {
                bridges.emplace_back(u, to);
            }
        }
    }
}

// The graph must be 0-indexed
void find_bridges(int n) {
	timer = 0;

	tin.assign(n, 0);
	low.assign(n, 0);
	visited.assign(n, false);

	for (int i {}; i < n; ++i) {
		if (!visited[i]) {
			dfs(i);
		}
	}
}
```

---