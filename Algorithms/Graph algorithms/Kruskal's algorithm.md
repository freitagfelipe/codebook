> [!info] Objetivo
> - Tem como objetivo dado um grafo bidirecional, encontrar a árvore geradora do grafo que tenha menor custo, ou seja, a Minimal Spanning Tree (MST) do grafo. Ademais, o algoritmo de Kruskal utiliza o [[Union-find]].

> [!caution] Grafos densos
> - O algoritmo de Kruskal é melhor para grafos esparsos, caso o grafo seja denso é melhor usar o [[Prim's algorithm]].

> [!note]- Complexidade
> - $O(V + E \log E)$

> [!hint] Encontrando a Maximal Spanning Tree
> - Para encontrar a Maximal Spanning Tree basta ao invés de ordenar do menor para o maior peso ordenar do maior para o menor peso.

```cpp
typedef tuple<int, int, int> Edge;

// The graph must be 0-indexed
int kruskal(int n, const vector<Edge> &edges) {
	UnionFind uf(n);

    sort(edges.begin(), edges.end());

    int mst_cost {};

    for (auto [u, v, w] : edges) {
        if (uf.find(u) != uf.find(v)) {
            uf.join(u, v);

            mst_cost += w;
        }
    }

    return mst_cost;
}
```

---