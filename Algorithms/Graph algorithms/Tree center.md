```ad-info
title: Objetivo

- Encontrar em um grafo acíclico e conexo, ou seja, uma árvore um ou dois vértices que minimizam a distância máxima entre ele e todos os outros vértices.
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
int parent[MAXN];
bool visited[MAXN];

void dfs(int curr) {
    visited[curr] = true;

    for (int v : g[curr]) {
        if (!visited[v]) {
            dist[v] = dist[curr] + 1;
            parent[v] = curr;
            
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

vector<int> get_center() {
    int x {get_farthest(0)};

    memset(dist, 0, sizeof(dist));
    memset(visited, 0, sizeof(visited));

    int y {get_farthest(x)};

    int k {dist[y]};

    vector<int> path;

    while (x != y) {
        path.push_back(y);

        y = parent[y];
    }

    path.push_back(x);

    if (k % 2 == 0) {
        return {path[k / 2]};
    }

    return {path[k / 2], path[(k + 1) / 2]};
}
```

---