```ad-attention
title: Grafos esparsos

- O algoritmo de Prim para Minimal Spanning Tree (MST) é melhor para grafos densos, caso o grafo seja esparso se deve usar o algoritmo de [[Kruskal]].
```

```ad-note
title: Complexidade
collapse: true

- $O((V + E) \log V)$
```

```cpp
typedef pair<int, int> pii;

int n;
vector<pii> g[MAXN];
int weight[MAXN];
bool marked[MAXN];

int prim() {
    for (int i {}; i < n; ++i) {
        weight[i] = INF;
    }

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

        for (auto [w, v] : g[curr]) {
            if (w < weight[v]) {
                weight[v] = w;

                pq.push({weight[v], v});
            }
        }
    }

    return mst_cost;
}
```

---