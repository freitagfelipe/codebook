> [!info] Objetivo
> - Tem como objetivo calcular algumas informaçõs úteis a respeito de um grafo funcional que podem ser utilizadas para resolver algum problema.

> [!note]- Complexidade
> - $O(V)$

```cpp
// closest_in_cycle[i] -> returns the closest vertex of the i-th vertex that is in a cycle
// vertex_cycle[i] -> returns the index of the cycle that the i-th vertex reaches
// cycle_distance[i] -> returns the distance from the i-th vertex to the closest_in_cycle
// in_cycle[i] -> returns if the i-th vertex is in a cycle
// cycle_start[i] -> returns in which vertex the i-th cycle starts
// cycle_size[i] -> returns the size of the i-th cycle
// to_cycle[i] -> returns which neighbor vertex of the i-th vertex is going towards the cycle and -1 if the i-th vertex is in the cycle
int current_cycle_id;
vector<vector<int>> g;
vector<int> closest_in_cycle, vertex_cycle, cycle_distance, cycle_start, cycle_size, to_cycle;
vector<bool> in_cycle, visited;

int find_next(int u) {
    for (int to : g[u]) {
        if (!visited[to]) {
            return to;
        }
    }

    return -1;
}

void process_cycle(int u) {
    int cycle_id {current_cycle_id++};

    cycle_start.push_back(u);
    cycle_size.emplace_back();

    while (u != -1 && !visited[u]) {
        visited[u] = true;
        in_cycle[u] = true;
        closest_in_cycle[u] = u;
        vertex_cycle[u] = cycle_id;
        cycle_distance[u] = 0;
        ++cycle_size[cycle_id];

        u = find_next(u);
    }
}

template <bool is_directed>
void calculate(int n) {
    vector<int> degree(n), inverse;

    for (int i {}; i < n; ++i) {
        for (int to : g[i]) {
            ++degree[to];
        }
    }

    queue<int> q;

    for (int i {}; i < n; ++i) {
        if (degree[i] == !is_directed) {
            q.push(i);
            visited[i] = true;
        }
    }

    while (!q.empty()) {
        int u {q.front()};

        inverse.push_back(u);

        q.pop();

        int to {find_next(u)};

        to_cycle[u] = to;

        --degree[to];

        if (degree[to] == !is_directed) {
            q.push(to);
            visited[to] = true;
        }
    }

    for (int i {}; i < n; ++i) {
        if (!visited[i]) {
            process_cycle(i);
        }
    }

    for (int i {(int) inverse.size() - 1}; i >= 0; --i) {
        int u {inverse[i]};
        int to {to_cycle[u]};

        closest_in_cycle[u] = closest_in_cycle[to];
        vertex_cycle[u] = vertex_cycle[to];
        cycle_distance[u] = cycle_distance[to] + 1;
        in_cycle[u] = false;
    }
}

// The graph must be 0-indexed
template <bool is_directed = true>
void build(int n) {
	current_cycle_id = 0;

    closest_in_cycle.assign(n, -1);
    vertex_cycle.assign(n, -1);
    cycle_distance.assign(n, 0);
    to_cycle.assign(n, -1);
    cycle_start.clear();
    cycle_size.clear();

    in_cycle.assign(n, false);
    visited.assign(n, false);

    calculate<is_directed>(n);
}
```

---