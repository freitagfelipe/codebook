> [!info] Objetivo
> - Tem como objetivo encontrar em uma árvore a distância máxima entre dois vértices desse grafo. A implementação do algoritmo utiliza uma adaptação da [[Depth-first search (DFS)]].

> [!note]- Complexidade
> - $O(V)$

```cpp
typedef pair<int, int> pii;

vector<vector<int>> g;

pii dfs(int u, int d = 0, int p = -1) {
    pii most_distant {u, d};

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

// The graph must be 0-indexed
int tree_diameter() {
	return dfs(dfs(0).first).second;
}
```

---