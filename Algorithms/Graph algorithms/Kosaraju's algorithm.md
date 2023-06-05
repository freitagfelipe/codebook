> [!info] Objetivo
> - O algoritmo tem como objetivo encontrar as componentes fortemente conexas de um digrafo. Utiliza o algoritmo de [[Topological sort - DFS]].

> [!info]- Complexidade
> - $O(V + E)$

```cpp
// MAXN is the largest possible number of nodes
// The nodes are 0-indexed
int n;
vector<int> g[MAXN], gt[MAXN], component(MAXN, -1);

void component_dfs(int v, int c) {
    component[v] = c;

    for (int u : gt[v]) {
        if (component[u] == -1) {
            component_dfs(u, c);
        }
    }
}

void scc() {
	vector<int> ts {topological_sort()};

    int comp {};

    for (int v : ts) {
        if (component[v] == -1) {
            component_dfs(v, comp++);
        }
    }
}
```

---