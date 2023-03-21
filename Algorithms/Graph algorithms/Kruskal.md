```ad-attention
title: Grafos densos

- O Algoritmo de Kruskal para Minimal Spanning Tree (MST) é melhor para grafos esparsos, caso o grafo seja denso se deve usar o algoritmo de [[Prim]].
```

```ad-note
title: Complexidade
collapse: true

- $O(V + E \log E)$
```

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

int p[MAXN];
int w[MAXN];

int find(int x) {
    if (p[x] == x) {
        return x;
    }

    return p[x] = find(p[x]);
}

void join(int x, int y) {
    x = find(x);
    y = find(y);

    if (x == y) {
        return;
    }

    if (w[x] == w[y]) {
        p[x] = y;

        ++w[y];
    } else if (w[x] > w[y]) {
        p[y] = x;
    } else {
        p[x] = y;
    }
}

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