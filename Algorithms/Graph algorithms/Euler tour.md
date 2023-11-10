> [!info] Objetivo
> - Tem como objetivo transformar uma árvore em um array para que seja possível fazermos utilizarmos outra estrutura para fazermos consultas e atualizações que podem ser a respeito de um caminho da árvore ou de uma sub-árvore.

> [!note]- Complexidade
> - $O(n)$

```cpp
vector<vector<int>> g;
int timer;

template <bool is_path_query>
void dfs(int u, int p, vector<int> &start, vector<int> &end) {
    start[u] = ++timer;

    for (int to : g[u]) {
        if (to == p) {
            continue;
        }

        dfs<is_path_query>(to, u, start, end);
    }

    if (is_path_query) {
        ++timer;
    }
    
    end[u] = timer;
}

// The graph must be 0-indexed
// The timers of the start and end arrays will be 1-indexed
// For subtree queries:
//     - The start[node] = end[node]
//     - For updates you just need to update the start[node] position
//     - For queries you can query in the [start[node], end[node]] interval
// For path queries:
//     - The start[node] = end[node] + 1
//     - For updates you need to update the start[node] and update the end[node]
//       position with the inverse
//     - For queries you can query in the [start[node], end[node] - 1] interval
template <bool is_path_query = false>
tuple<vector<int>, vector<int>> get_euler_tour(int s, int n) {
    vector<int> start(n), end(n);
    
	timer = 0;

    dfs<is_path_query>(s, -1, start, end);

    return {start, end};
}
```

---