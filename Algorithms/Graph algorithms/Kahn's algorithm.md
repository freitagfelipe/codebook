> [!info] Objetivo
> - Tem como objetivo realizar a ordenação topológica de um grafo, ou seja, uma ordem linear de seus nós em que cada nó vem antes de todos nós para os quais este tenha arestas de saída.

> [!caution] Atenção
> - O gráfico deve ser um DAG (Directed Acyclic Graph) para ter ordenação topológica.
> - Um DAG pode ter mais de uma ordenação topológica.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
vector<vector<int>> g;

// The graph must be 0-indexed
vector<int> topological_sort(int n) {
	vector<int> in_degree(n);

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