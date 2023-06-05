> [!info] Objetivo
> O algoritmo de Kruskal tem como objetivo dado um grafo bidirecional, encontrar a árvore geradora do grafo que tenha menor custo, ou seja, a Minimal Spanning Tree (MST) do grafo. Além disso, o algoritmo de Kruskal utiliza o [[Union-find]].

> [!caution] Grafos densos
> O algoritmo de Kruskal é melhor para grafos esparsos, caso o grafo seja denso é melhor usar o algoritmo de [[Prim's algorithm]].

> [!note]- Complexidade
> $O(V + E \log E)$, gastaremos $V$ para inicializar o [[Union-find]] e $E \log E$ para ordenar a lista de arestas.

```cpp
struct Edge {
    int u;
    int v;
    int w;

    Edge(int u, int v, int w) {
        this->u = u;
        this->v = v;
        this->w = w;
    }

    bool operator<(const Edge &e) const {
        return this->w < e.w;
    }
};

int n;
vector<Edge> edges;

int kruskal() {
    sort(edges.begin(), edges.end());

    for (int i {}; i < n; ++i) {
        p[i] = i;
    }

    int mst_cost {};

    for (auto [u, v, w] : edges) {
        if (find(u) != find(v)) {
            join(u, v);

            mst_cost += w;
        }
    }

    return mst_cost;
}
```

---