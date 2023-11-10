> [!info] Objetivo
> - Tem como objetivo encontrar para um dado vértice $s$ o menor caminho para todos os outros vértices do grafo. A primeira implementação é melhor para grafos esparsos, já a segunda implementação é melhor para grafos densos, ou seja, quando $E \approx V^2$.

> [!caution] Arestas com pesos negativos
> - O algoritmo de Dijkstra não funciona com grafos que contém arestas com peso negativo, para isso se deve usar [[Bellman-Ford]] ou o [[Floyd-Warshall]].

> [!note]- Complexidade
> - Sparse Dijkstra: $O((V + E) \log V)$
> - Dense Dijkstra:  $O(V^2 + E)$

```cpp
typedef pair<int, int> pii;

vector<int> dijkstra(int s, const vector<vector<pii>> &g) {
	// INF is a distance that can represent the node as unreachable
	vector<int> dists(g.size(), INF);
	vector<bool> marked(g.size());

    priority_queue<pii, vector<pii>, greater<pii>> pq;

    dists[s] = 0;

    pq.push({0, s});

    while (!pq.empty()) {
        int curr {pq.top().second};

        pq.pop();

        if (marked[curr]) {
            continue;
        }

        marked[curr] = true;

        for (auto [w, to] : g[curr]) {
            if (dists[curr] + w < dists[to]) {
                dists[to] = dists[curr] + w;

                pq.push({dists[to], to});
            }
        }
    }

	return dists;
}
```

```cpp
typedef pair<int, int> pii;

void dijkstra(int s, const vector<vector<pii>> &g) {
	// INF is a distance that can represent the node as unreachable
	vector<int> dists(g.size(), INF);
	vector<bool> marked(g.size());

	int n {(int) g.size()};

    dists[s] = 0;

    for (int i {}; i < n; ++i) {
        int curr {-1};

        for (int j {}; j < n; ++j) {
            if (marked[j]) {
                continue;
            }

            if (curr == -1 || dists[j] < dists[curr]) {
                curr = j;
            }
        }

        marked[curr] = true;

        for (auto [w, to] : g[curr]) {
            dists[to] = min(dists[to], dists[curr] + w);
        }
    }

	return dists;
}
```

---
