> [!note] Objetivo
> - Tem como objetivo dividir uma árvore em vários caminhos para que consultas e atualizações a respeito de caminhos de uma árvore e/ou sub-árvores sejam feitas de maneira eficiente.

> [!note]- Complexidade
> - Considere $f$ como sendo a complexidade da operação utilizando a estrutura de dados auxiliar.
> - Build: $O(n)$
> - Query path: $O(\log n \cdot f)$
> - Update path: $O(\log n \cdot)$
> - Update vertex: $O(f)$
> - Query subtree: $O(f)$
> - Update subtree: $O(f)$

```cpp
// MAXN is the largest possible number of nodes
vector<int> g[MAXN], p, depth, heavy, head, pos, sz;
int curr_pos;

int dfs(int u) {
    sz[u] = 1;
    int max_to_size {};

    for (int to : g[u]) {
        if (to != p[u]) {
            p[to] = u;
            depth[to] = depth[u] + 1;
            
            int to_size {dfs(to)};

            sz[u] += to_size;

            if (to_size > max_to_size) {
                max_to_size = to_size;
                heavy[u] = to;
            }
        }
    }

    return sz[u];
}

void decompose(int u, int h) {
    head[u] = h;
    pos[u] = ++curr_pos;

    if (heavy[u] != -1) {
        decompose(heavy[u], h);
    }

    for (int to : g[u]) {
        if (to != p[u] && to != heavy[u]) {
            decompose(to, to);
        }
    }
}

// The graph must be 0-indexed
// The positions of each vertex will be 1-indexed for future data structure uses
void build(int root, int n) {
    p.assign(n, -1);
    heavy.assign(n, -1);
    depth.assign(n, 0);
    head.assign(n, 0);
    pos.assign(n, 0);
    sz.assign(n, 0);

    curr_pos = 0;

    dfs(root);
    decompose(root, root);
}

int query_path(int u, int v) {
    if (pos[u] < pos[v]) {
        swap(u, v);
    }

    if (head[u] == head[v]) {
        int val {}; // Do some query on the interval [pos[v], pos[u]]

        return val;
    }

    // Do some query x on the interval [pos[head[u]], pos[u]]
    // and a recursive call to the query_path(p[head[u]], v) that will return some value y
    // and after that you call calculate the answer with x and y
    int result {};

    return result;
}

void update_path(int u, int v, int x) {
    if (pos[u] < pos[v]) {
        swap(u, v);
    }

    if (head[u] == head[v]) {
        // Update the interval [pos[v], pos[u]] with the value x

        return;
    }

    // Update the interval [pos[head[u]], pos[u]] with the value x
    
    update_path(p[head[u]], v, x);
}

void update_vertex(int u, int x) {
    // Do a simple point update in the position pos[u] with x
}

int query_subtree(int u) {
    // Do a simple query on the interval [pos[u], pos[u] + sz[u] - 1]
}

void update_subtree(int u, int x) {
    // Do a simple update on the interval [pos[u], pos[u] + sz[u] - 1] with the value x
}
```

---