> [!info] Objetivo
> O algoritmo de Kruskal tem como objetivo dado um grafo bidirecional, encontrar a árvore geradora do grafo que tenha menor custo, ou seja, a Minimal Spanning Tree (MST) do grafo. Além disso, o algoritmo de Kruskal utiliza o [[Union-find]].

> [!caution] Grafos densos
> O algoritmo de Kruskal é melhor para grafos esparsos, caso o grafo seja denso é melhor usar o algoritmo de [[Prim]].

> [!faq] Como funciona?
> O algoritmo de Kruskal funciona com uma ideia gulosa, dado uma lista de arestas é necessário ordená-las em ordem crescente de peso e inicalizar [[Union-find]] para cada nó, após isso, para cada nó checaremos utilizando o [[Union-find]] se adicionar a aresta de $u$ para $v$ não causa um cíclo, pois se causar não iremos considerar essa aresta para a MST e pelo fato das arestas estarem ordenadas sabemos que se uma aresta de $u$ para $v$ causar ciclos é porque já encontramos um conjunto de arestas que conecta $u$ até $v$.

> [!note] Complexidade
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