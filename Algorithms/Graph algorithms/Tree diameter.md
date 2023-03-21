```ad-info
title: Objetivo

- Encontrar em um grafo acíclico e conexo, ou seja, uma árvore a distância máxima entre dois vértices desse grafo.
```

```ad-note
title: Complexidade
collapse: true

- $O(V)$
```

```cpp
int n;
vector<int> g[MAXN];
int dist[MAXN];
bool visited[MAXN];

void dfs(int curr) {
    visited[curr] = true;

    for (int v : g[curr]) {
        if (!visited[v]) {
            dist[v] = dist[curr] + 1;

            dfs(v);
        }
    }
}

int get_farthest(int s) {
    dist[s] = 0;

    dfs(s);

    int max_dist {};
    int farthest_node {s};

    for (int i {}; i < n; ++i) {
        if (max_dist < dist[i]) {
            max_dist = dist[i];
            farthest_node = i;
        }
    }

    return farthest_node;
}

int get_diameter() {
    int x {get_farthest(0)};

    memset(dist, 0, sizeof(dist));
    memset(visited, 0, sizeof(visited));

    int y {get_farthest(x)};

    return dist[y];
}
```
