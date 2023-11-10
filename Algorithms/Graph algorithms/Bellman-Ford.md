> [!info] Objetivo
> - Tem como objetivo encontrar para um dado vértice $s$ o menor caminho para todos os outros vértices do grafo.

> [!note]- Complexidade
> - $O(VE)$

```cpp
typedef tuple<int, int, int> Edge;

// The graph must be 0-indexed
vector<int> bellman_ford(int s, int n, const vector<Edge> &edges) {
	// INF is a distance that can represent the node as unreachable
	vector<int> dists(n, INF);

    dists[s] = 0;

    for (int i {}; i < n - 1; ++i) {
        for (auto [u, v, w] : edges) {
            if (dists[u] != INF) {
                dists[v] = min(dists[v], dists[u] + w);
            }
        }
    }

    for (auto [u, v, w] : edges) {
        if (dists[u] + w < dists[v]) {
            throw runtime_error("Has negative cycle");
        }
    }

	return dists;
}
```

>[!hint] Encontrando ciclo negativos
> - O algoritmo de Bellman-Ford consegue detectar se o grafo contém ciclos negativos e retornar os vértices que estão nesse ciclo utilizando a seguinte adaptação.

```cpp
typedef tuple<int, int, int> Edge;

// The graph must be 0-indexed
pair<bool, vector<int>> bellman_ford(int n, const vector<Edge> &edges) {
	vector<int> p(n), dists(n);
	int x {-1};

    for (int i {}; i < n; ++i) {
        x = -1;

        for (auto [u, v, w] : edges) {
            if (dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
                p[v] = u;
                x = v;
            }
        }
    }

	if (x == -1) {
		return {false, {}};
	}

	for (int i {}; i < n; ++i) {
		x = p[x];
	}

	vector<int> cycle;

	for (int u {x};; u = p[u]) {
		cycle.push_back(u);

		if (u == x && cycle.size() > 1) {
			break;
		}
	}

	reverse(cycle.begin(), cycle.end());

	return {true, cycle};
}
```

---