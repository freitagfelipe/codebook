> [!info] Objetivo
> Tem como objetivo dado um grafo bidirecional, encontrar a árvore geradora do grafo que tenha menor custo, ou seja, a Minimal Spanning Tree (MST) do grafo.

> [!caution] Grafos esparsos
> - O algoritmo de Prim para Minimal Spanning Tree (MST) é melhor para grafos densos, caso o grafo seja esparso se deve usar o algoritmo de [[Kruskal's algorithm]].

> [!note]- Complexidade
> - $O((V + E) \log V)$

> [!hint] Encontrando a Maximal Spanning Tree
> - Para encontrar a Maximal Spanning Tree basta ao invés de ordenar do menor para o maior peso ordenar do maior para o menor peso.

```cpp
typedef pair<int, int> pii;

// The graph must be 0-indexed
int prim(int n, const vector<vector<int>> &g) {
	// INF is an absurd weight
	vector<int> weight(n, INF);
	vector<bool> marked(n, false);

    priority_queue<pii, vector<pii>, greater<pii>> pq;

    weight[0] = 0;

    pq.push({0, 0});

    int mst_cost {};

    while (!pq.empty()) {
        int curr {pq.top().second};

        pq.pop();

        if (marked[curr]) {
            continue;
        }

        marked[curr] = true;
        mst_cost += weight[curr];

        for (auto [w, to] : g[curr]) {
            if (w < weight[to]) {
                weight[to] = w;

                pq.push({weight[to], to});
            }
        }
    }

    return mst_cost;
}
```

---