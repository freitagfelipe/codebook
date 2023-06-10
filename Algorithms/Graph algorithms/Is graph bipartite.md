> [!info] Objetivo
> - Um grafo é bipartido se seus vértices podem ser divididos em dois conjuntos distintos, de forma que todas as arestas do grafo conectem vértices de conjuntos diferentes, ou seja, não pode haver nenhuma aresta que conecte vértices do mesmo conjunto.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
// MAXN is the largest possible number of nodes
int color[MAXN];
vector<int> g[MAXN];

bool is_bipartite(int v, int c = 1) {
	color[v] = c;
	bool ans {true};

	for (int neigh : g[v]) {
		if (color[neigh] == -1) {
			ans &= is_bipartite(neigh, 1 - c, g);
		} else if (color[neigh] != 1 - c) {
			return false;
		}

		if (!ans) {
			return false;
		}
	}

	return true;
}
```

---