> [!info] Objetivo
> - Tem como objetivo descobrir se um grafo é bipartido. Um grafo é bipartido se seus vértices podem ser divididos em dois conjuntos distintos, de forma que todas as arestas do grafo conectem vértices de conjuntos diferentes, ou seja, não pode haver nenhuma aresta que conecte vértices do mesmo conjunto.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
vector<vector<int>> g;
vector<int> color;

// The graph must be 0-indexed
bool is_bipartite(int u, int c = 1) {
    color[u] = c;

    for (int to : g[u]) {
        if (color[to] == -1 && !is_bipartite(to, 1 - c)) {
            return false;
        } else if (color[to] == c) {
            return false;
        }
    }

    return true;
}

// Call it before call is_bipartite
void setup(int n) {
	color.assign(n, -1);
}
```

---