> [!info] Objetivo
> - Descobrir se um grafo é bipartido enquanto adiciona as arestas. Um grafo é bipartido se seus vértices podem ser divididos em dois conjuntos distintos, de forma que todas as arestas do grafo conectem vértices de conjuntos diferentes, ou seja, não pode haver nenhuma aresta que conecte vértices do mesmo conjunto. Ademais, a implementação utiliza uma adaptação do [[Union-find]].

> [!info]- Complexidade
> - Build: $O(n)$
> - Find/Add edge: $O(\alpha(n))$
> - Is bipartite: $O(1)$

```cpp
typedef pair<int, int> pii;

// MAXN is the largest possible number of nodes
pii p[MAXN];
int h[MAXN], bipartite[MAXN];

pii find(int x) {
    if (x != p[x].first) {
        int parity {p[x].second};

        p[x] = find(p[x].first);
        p[x].second ^= parity;
    }

    return p[x];
}

void add_edge(int u, int v) {
    auto [x, x_parity] {find(u)};
    auto [y, y_parity] {find(v)};

    if (x == y) {
        if (x_parity == y_parity) {
            bipartite[x] = false;
        }

        return;
    }

    if (h[x] < h[y]) {
        swap (x, y);
    }

    p[y] = {x, x_parity ^ y_parity ^ 1};
    bipartite[x] &= bipartite[y];

    if (h[x] == h[y]) {
        ++h[x];
    }
}

bool is_bipartite(int v) {
    return bipartite[find(v).first];
}

void build(int n) {
    for (int i {}; i < n; ++i) {
        p[i] = {i, 0};
        bipartite[i] = true;
    }
}
```

---