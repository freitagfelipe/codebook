> [!info] Objetivo
> - Encontrar em um grafo acíclico e conexo, ou seja, uma árvore um ou dois vértices que minimizam a distância máxima entre ele e todos os outros vértices. Utiliza uma adaptação da [[Depth-first search (DFS)]].

> [!note]- Complexidade
> - $O(V)$

```cpp
typedef pair<int, int> pii;
typedef tuple<int, int, int> tiii;

// MAXN is the largest possible number of nodes
vector<int> g[MAXN];
int parent[MAXN];

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

vector<int> get_center() {
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