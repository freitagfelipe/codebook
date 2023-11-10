> [!info] Objetivo
> - Tem como objetivo encontrar em uma árvore um ou dois vértices que minimizam a distância máxima entre ele e todos os outros vértices, ou seja, o vértice que está no centro. Ademais, o algoritmo utiliza uma adaptação da [[Depth-first search (DFS)]] e utiliza a ideia do [[Tree diameter]] para encontrar os vértices que estão na ponta do diâmetro.

> [!note]- Complexidade
> - $O(V)$

```cpp
typedef pair<int, int> pii;
typedef tuple<int, int, int> tiii;

// MAXN is the largest possible number of nodes
vector<vector<int>> g;
vector<int> parent;

pii dfs(int u, int d = 0, int p = -1) {
    pii most_distant {u, d};

	parent[u] = p;

    for (int to : g[u]) {
        if (to != p) {
            pii result {dfs(to, d + 1, u)};

            if (result.second > most_distant.second) {
                most_distant = result;
            }
        }
    }

    return most_distant;
}

tiii get_most_distants() {
	int x {dfs(0).first};
	auto [y, d] = dfs(x);
	
	return {x, y, d};
}

// The graph must be 0-indexed
vector<int> get_center(int n) {
	parent.assign(n, -1);

	auto [x, y, k] = get_most_distants();

	vector<int> path;

	for (; x != y; y = parent[y]) {
		path.push_back(y);
	}

    path.push_back(x);

	if (k % 2 == 0) {
        return {path[k / 2]};
    }

    return {path[k / 2], path[(k + 1) / 2]};
}
```

---