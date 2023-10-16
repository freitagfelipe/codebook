> [!info] Objetivo
> - Tem como objetivo dado uma árvore responder perguntas sobre o menor ancestral comum entre dois vértices $v$ e $u$, mas pode ser adaptado para responder consultas de mínimo, máximo, soma das arestas, etc.

> [!note]- Complexidade
> - Build: $O((V + E) \log V)$
> - Query: $O(\log V)$

```cpp
// L is the ceil(log(n))
int n, l, timer {};
// MAXN is the largest possible number of nodes
vector<int> g[MAXN], tin(MAXN, 0), tout(MAXN, 0);
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

// This function will climb the vertex u until it reaches the vertex v
int go(int u, int v) {
    for (int i {l}; i >= 0; --i) {
        if (tin[v] < up[u][i]) {
            // Answer some question based on a computation made
            // in the build function
            
            u = up[u][l];
        }
    }
}

// You can use this function to answer queries on a path of min, max, etc
int query(int u, int v) {
	int lca_ans {lca(u, v)};

	if (lca_ans == u) {
        return go(v, lca_ans);
    } else if (lca_ans == v) {
        return go(u, lca_ans);
    }

	// Return the ans based on something related with the go(u, lca_ans) and go(v, lca_ans)
}

void build(int root) {
    l = ceil(log2(n));
    up.assign(n, vector<int>(l + 1));
    dfs(root, root);
}
```

---