> [!info] Objetivo
> - Fazer a travessia em um grafo.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
// MAXN is the largest possible number of nodes
vector<int> g[MAXN];
bitset<MAXN> visited;

void bfs(int i) {
	queue<int> q;
	
	q.push(i);
	
	while(!q.empty()) {
		int curr {q.front()};

		q.pop();

        visited[curr] = true;
		
		for(int n : g[curr]) {
			if(!visited[n]) {
				q.push(n);

                visited[n] = true;
			}
		}
	}
}
```

> [!hint] Adaptação
> - Pode ser utilizado para saber o grau de distância dos vértices em relação ao nó inicial em termos de arestas.

```cpp
// MAXN is the largest possible number of nodes
int n;
vector<int> g[MAXN];
int dist[MAXN];
bitset<MAXN> visited;

vector<int> bfs(int s) {
	for (int i {}; i < n; ++i) {
		// INF is a distance that can represent the node as unreachable
		dist[i] = INF;
	}

	queue<int> q;

	q.push(s);

	dist[s] = 0;

	while (!q.empty()) {
		int curr {q.front()};

		q.pop();

		visited[curr] = true;

		for (int n : g[curr]) {
			if (!visited[n]) {
				q.push(n);

				dist[n] = dist[curr] + 1;
				visited[n] = true;
			}
		}
	}

	return dist;
}
```

---