```ad-attention
title: Restrição

- O gráfico deve ser um DAG para ter ordenação topológica.
```

```ad-note
title: Complexidade
collapse: true

- $O(V + E)$
```

```cpp
int n;
int in_degree[MAXN];
vector<int> g[MAXN];

vector<int> topological_sort() {
    for (int i {}; i < n; ++i) {
        for (int v : g[i]) {
            ++in_degree[v];
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

        for (int v : g[curr]) {
            if (--in_degree[v] == 0) {
                q.push(v);
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