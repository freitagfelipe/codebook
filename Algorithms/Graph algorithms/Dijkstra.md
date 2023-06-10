> [!info] Objetivo
> - Dado um grafo ele tem como objetivo encontrar o menor caminho de $s$ para todos os outros nós do grafo.

> [!caution] Restrição
> - Não funciona com grafos que contém arestas com peso negativo, para isso se deve usar [[Bellman-Ford]] ou o [[Floyd-Warshall]].

> [!note]- Complexidade
> - $O((V + E) \log V)$

```cpp
typedef pair<int, int> pii;

// MAXN is the largest possible number of nodes
int n;
int dist[MAXN];
bitset<MAXN> marked;
vector<pii> g[MAXN];

void dijkstra(int s) {
    for (int i {}; i < n; ++i) {
		// INF is a distance that can represent the node as unreachable
        dist[i] = INF;
    }

    priority_queue<pii, vector<pii>, greater<pii>> pq;

    dist[s] = 0;

    pq.push({0, s});

    while (!pq.empty()) {
        int curr {pq.top().second};

        pq.pop();

        if (marked[curr]) {
            continue;
        }

        marked[curr] = true;

        for (auto [w, v] : g[curr]) {
            if (dist[curr] + w < dist[v]) {
                dist[v] = dist[curr] + w;

                pq.push({dist[v], v});
            }
        }
    }
}
```

> [!caution] Atenção
> - Caso o grafo seja denso, ou seja, $E \approx V^2$, é melhor utilizar a adaptação abaixo.

> [!note]- Complexidade
> - $O(V^2 + E)$

```cpp
typedef pair<int, int> pii;

// MAXN is the largest possible number of nodes
int n;
int dist[MAXN];
bitset<MAXN> marked;
vector<pii> g[MAXN];

void dijkstra(int s) {
    for (int i {}; i < n; ++i) {
		// INF is a distance that can represent the node as unreachable
        dist[i] = INF;
    }

    dist[s] = 0;

    for (int i {}; i < n; ++i) {
        int curr {-1};

        for (int j {}; j < n; ++j) {
            if (marked[j]) {
                continue;
            }

            if (curr == -1 || dist[j] < dist[curr]) {
                curr = j;
            }
        }

        marked[curr] = true;

        for (auto [w, v] : g[curr]) {
            dist[v] = min(dist[v], dist[curr] + w);
        }
    }
}
```

---
