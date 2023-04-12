```ad-info
title: Objetivo

- Encontrar em um grafo acíclico e conexo, ou seja, uma árvore a distância máxima entre dois vértices desse grafo. Utiliza uma adaptação da [[Depth-first search (DFS)]].
```

```ad-note
title: Complexidade
collapse: true

- $O(V)$
```

```cpp
typedef pair<int, int> pii;

vector<int> g[MAXN];

pii dfs(int curr, int d = 0, int p = -1) {
    pii most_distant {curr, d};

    for (int neigh : g[curr]) {
        if (neigh != p) {
            pii result {dfs(neigh, d + 1, curr)};

            if (result.second > most_distant.second) {
                most_distant = result;
            }
        }
    }

    return most_distant;
}

int tree_diameter() {
	return dfs(dfs(0).first).second;
}
```

---