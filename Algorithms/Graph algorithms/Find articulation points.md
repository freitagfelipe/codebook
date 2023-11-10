> [!info] Objetivo
> - Tem como objetivo encontrar os pontos de articulação de um grafo, ou seja, os vértices que se removidos do grafo causariam a criação de uma ou mais componentes conexas.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
int timer;
vector<vector<int>> g;
vector<int> tin, low;
vector<bool> visited, is_articulation_point;

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

// The graph must be 0-indexed
void find_articulation_points(int n) {
	timer = 0;

	tin.assign(n, 0);
	low.assign(n, 0);
	visited.assign(n, false);
	is_articulation_point.assign(n, false);

	for (int i {}; i < n; ++i) {
		if (!visited[i]) {
			dfs(i);
		}
	}
}
```

---