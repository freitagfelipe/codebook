> [!info] Objetivo
> - Tem como objetivo dado uma árvore responder perguntas sobre o menor ancestral comum entre dois vértices $v$ e $u$.

> [!note]- Complexidade
> - Build: $O(n \log n)$
> - Query: $O(\log n)$

```cpp
// L is the ceil(log(n))
int n, l, timer {};
// MAXN is the largest possible number of nodes
vector<int> g[MAXN], tin(MAXN), tout(MAXN);
vector<vector<int>> up;

void dfs(int u, int p) {
    tin[u] = ++timer;
    up[u][0] = p;

    for (int i {1}; i <= l; ++i) {
        up[u][i] = up[up[u][i - 1]][i - 1];
    }

    for (int to : g[u]) {
        if (to != p) {
            dfs(to, u);
        }
    }

    tout[u] = ++timer;
}

// Checks if u is ancestor of v
bool is_ancestor(int u, int v) {
    return tin[u] <= tin[v] && tout[v] <= tout[u];
}

int lca(int u, int v) {
    if (is_ancestor(u, v)) {
        return u;
    } else if (is_ancestor(v, u)) {
        return v;
    }

    for (int i {l}; i >= 0; --i) {
        if (!is_ancestor(up[u][i], v)) {
            u = up[u][i];
        }
    }

    return up[u][0];
}

void build(int root) {
    l = ceil(log2(n));
    up.assign(n, vector<int>(l + 1));
    dfs(root, root);
}
```

---