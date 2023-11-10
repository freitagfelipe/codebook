> [!info] Objetivo
> - Tem como objetivo decompor uma árvore em centroids para facilitar cálculos a respeito de caminhos em uma árvore utilizando divisão e conquista.

> [!note]- Complexidade
> - $O(n \log n)$

```cpp
vector<vector<int>> g;
vector<int> subtree_size;
vector<bool> is_removed;

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

// The graph must be 0-indexed
int centroid_decomposition(int u) {
    int centroid {get_centroid(u, get_subtree_size(u))};

    is_removed[centroid] = true;
    
    // Do some calculation based on the subtrees and the centroid

    for (int to : g[centroid]) {
        if (is_removed[to]) {
            continue;
        }

        centroid_decomposition(to);
    }

	// Return some answer that was calculated using the centroid decomposition
}

// Call it before call the centroid decomposition
void setup(int n) {
	is_removed.assign(n, false);
	subtree_size.assign(n, 0);
}
```

---