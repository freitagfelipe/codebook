> [!info] Objetivo
> - Dado um grafo ele tem como objetivo encontrar o menor caminho de $s$ para todos os outros nós do grafo.

>[!hint] Ciclo negativos
> - O algoritmo de Bellman-Ford consegue detectar se o grafo contém ciclos negativos.

> [!note]- Complexidade
> - $O(VE)$

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
};

// MAXN is the largest possible number of nodes
int n;
int dist[MAXN];
vector<Edge> edges;

void bellman_ford(int s) {
    for (int i {}; i < n; ++i) {
	    // INF is a distance that can represent the node as unreachable
        dist[i] = INF;
    }

    dist[s] = 0;

    for (int i {}; i < n - 1; ++i) {
        for (auto [u, v, w] : edges) {
            if (dist[u] != INF) {
                dist[v] = min(dist[v], dist[u] + w);
            }
        }
    }

    for (auto [u, v, w] : edges) {
        if (dist[u] + w < dist[v]) {
            throw runtime_error("Has negative cycle");
        }
    }
}
```

---