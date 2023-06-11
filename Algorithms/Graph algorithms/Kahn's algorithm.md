> [!info] Objetivo
> - Realizar a ordenação topológica de um grafo, ou seja, uma ordem linear de seus nós em que cada nó vem antes de todos nós para os quais este tenha arestas de saída.

> [!caution] Atenção
> - O gráfico deve ser um DAG (Directed Acyclic Graph) para ter ordenação topológica.
> - Um DAG pode ter mais de uma ordenação topológica.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
// MAXN is the largest possible number of nodes
int n;
int in_degree[MAXN];
vector<int> g[MAXN];

vector<int> topological_sort() {
    for (int i {}; i < n; ++i) {
        for (int to : g[i]) {
            ++in_degree[to];
        }
    }

    queue<int> q;

    for (int i {}; i < n; ++i) {
        if (in_degree[i] == 0) {
            q.push(i);
        }
    }

    vector<int> ans;

    while (!q.empty()) {
        int curr {q.front()};

        q.pop();

        ans.push_back(curr);

        for (int to : g[curr]) {
            if (--in_degree[to] == 0) {
                q.push(to);
            }
        }
    }

    if (ans.size() != n) {
        throw runtime_error("No topological sort");
    }

    return ans;
}
```

---