> [!info] Objetivo
> Encontrar em um grafo acíclico e conexo, ou seja, uma árvore a distância máxima entre dois vértices desse grafo. A implementação do algoritmo utiliza uma adaptação da [[Depth-first search (DFS)]].

> [!note]- Complexidade
> - $O(V)$

```cpp
typedef pair<int, int> pii;

// MAXN is the largest possible number of nodes
vector<int> g[MAXN];

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

int tree_diameter() {
	return dfs(dfs(0).first).second;
}
```

---