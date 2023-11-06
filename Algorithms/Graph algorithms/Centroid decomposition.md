> [!info] Objetivo
> - Decompor uma árvore em centroids para facilitar consultas a respeito de caminhos na árvore.

> [!note]- Complexidade
> - $O(n \log n)$

```cpp
int n;
// MAXN is the largest possible number of nodes
vector<int> g[MAXN], subtree_size;
bitset<MAXN> is_removed;

int get_subtree_size(int u, int p = -1) {
    subtree_size[u] = 1;

    for (int to : g[u]) {
        if (to != p && !is_removed[to]) {
            subtree_size[u] += get_subtree_size(to, u);
        }
    }

    return subtree_size[u];
}

int get_centroid(int u, int tree_size, int p = -1) {
    for (int to : g[u]) {
		if (to == p || is_removed[to]) {
            continue;
        }

        if (subtree_size[to] * 2 > tree_size) {
			return get_centroid(to, tree_size, u);
        }
    }

    return u;
}

int centroid_decomposition(int u) {
    int centroid {get_centroid(u, get_subtree_size(u))};

    is_removed[centroid] = true;
    
    // do something with the centroid

    for (int to : g[centroid]) {
        if (is_removed[to]) {
            continue;
        }

        centroid_decomposition(to);
    }

	// return some answer that was calculated using the centroid decomposition
}
```

---