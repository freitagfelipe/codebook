> [!info] Objetivo
> - Encontrar arestas em um grafo direcionado que se removidas fazem com que seja gerada uma nova componente conexa, ou seja, desconectam o grafo.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
struct Edge {
    int u;
    int v;

	Edge(int u, int v) {
		this->u = u;
		this->v = v;
	}
};

int n, timer {};
// MAXN is the largest possible number of nodes
vector<int> g[MAXN], tin, low;
vector<Edge> bridges;
bitset<MAXN> visited;

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

            if (low[to] > tin[to]) {
                bridges.emplace_back(u, to);
            }
        }
    }
}

void find_bridges() {
	for (int i {}; i < n; ++i) {
		if (!visited[i]) {
			dfs(i);
		}
	}
}
```

---