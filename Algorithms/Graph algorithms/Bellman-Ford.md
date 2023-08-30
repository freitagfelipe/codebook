> [!info] Objetivo
> - Dado um grafo ele tem como objetivo encontrar o menor caminho de $s$ para todos os outros nós do grafo.

> [!note]- Complexidade
> - $O(VE)$

```cpp
struct Edge {
    int u;
    int v;
    int w;
};

// MAXN is the largest possible number of nodes
int n;
int dist[MAXN];
vector<Edge> edges;

void bellman_ford(int s) {
    for (int i {}; i < n; ++i) {
	    // INF is a distance that can represent the node as unreachable
        dist[i] = INF;
    }

    dist[s] = 0;

    for (int i {}; i < n - 1; ++i) {
        for (auto [u, v, w] : edges) {
            if (dist[u] != INF) {
                dist[v] = min(dist[v], dist[u] + w);
            }
        }
    }

    for (auto [u, v, w] : edges) {
        if (dist[u] + w < dist[v]) {
            throw runtime_error("Has negative cycle");
        }
    }
}
```

>[!hint] Encontrando ciclo negativos
> - O algoritmo de Bellman-Ford consegue detectar se o grafo contém ciclos negativos e retornar os vértices que estão nesse ciclo utilizando a seguinte adaptação.

```cpp
typedef pair<bool, vector<int>> pbvi;

struct Edge {
    int u;
    int v;
    int w;
};

// MAXN is the largest possible number of nodes
int n;
int dist[MAXN];
vector<Edge> edges;

pbvi bellman_ford() {
	vector<int> p(n + 1);
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