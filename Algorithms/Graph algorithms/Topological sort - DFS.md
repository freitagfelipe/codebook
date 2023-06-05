> [!info] Objetivo
> - Realizar a ordenação topológica de um grafo, ou seja, uma ordem linear de seus nós em que cada nó vem antes de todos nós para os quais este tenha arestas de saída.

> [!caution] Atenção
> - O gráfico deve ser um DAG (Directed Acyclic Graph) para ter ordenação topológica.
> - Um DAG pode ter mais de uma ordenação topológica.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
// MAXN is the largest possible number of nodes
int n;
vector<int> g[MAXN], ts;
bitset<MAXN> visited;

void dfs(int v) {
    visited[v] = true;

    for (int u : g[v]) {
        if (!visited[u]) {
            ts_dfs(u);
        }
    }

    ts.push_back(v);
}

vector<int> topological_sort() {
	for (int i {}; i < n; ++i) {
		if (!visited[i]) {
			dfs(i);
		}
	}

	reverse(ts.begin(), ts.end());

	return move(ts);
}
```

---