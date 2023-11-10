> [!info] Objetivo
> - Tem como objetivo descobrir se um grafo é bipartido enquanto adiciona as arestas. Um grafo é bipartido se seus vértices podem ser divididos em dois conjuntos distintos, de forma que todas as arestas do grafo conectem vértices de conjuntos diferentes, ou seja, não pode haver nenhuma aresta que conecte vértices do mesmo conjunto. Ademais, a implementação utiliza uma adaptação do [[Union-find]].

> [!note]- Complexidade
> - Build: $O(n)$
> - Find/Add edge: $O(\alpha(n))$
> - Is bipartite: $O(1)$

```cpp
typedef pair<int, int> pii;

vector<pii> p;
vector<int> h;
vector<bool> bipartite;

pii find(int x) {
    if (x != p[x].first) {
        int parity {p[x].second};

        p[x] = find(p[x].first);
        p[x].second ^= parity;
    }

    return p[x];
}

// U and V must be 0-indexed
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

// U must be 0-indexed
bool is_bipartite(int u) {
    return bipartite[find(u).first];
}

// Call it before call other methods
void setup(int n) {
	p.assign(n, {});
	h.assign(n, 0);
	bipartite.assign(n, true);

    for (int i {}; i < n; ++i) {
        p[i] = {i, 0};
    }
}
```

---