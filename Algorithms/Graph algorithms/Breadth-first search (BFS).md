> [!info] Objetivo
> - Fazer a travessia em um grafo.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
// MAXN is the largest possible number of nodes
vector<int> g[MAXN];
bitset<MAXN> visited;

void bfs(int s) {
	queue<int> q;
	
	q.push(s);

	visited[s] = true;
	
	while(!q.empty()) {
		int curr {q.front()};

		q.pop();
		
		for(int to : g[curr]) {
			if(!visited[to]) {
				q.push(to);

                visited[to] = true;
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
int dist[MAXN];
vector<int> g[MAXN];
bitset<MAXN> visited;

void bfs(int s) {
	for (int i {}; i < n; ++i) {
		// INF is a distance that can represent the node as unreachable
		dist[i] = INF;
	}

	queue<int> q;

	q.push(s);

	dist[s] = 0;
	visited[s] = true;

	while (!q.empty()) {
		int curr {q.front()};

		q.pop();

		for (int to : g[curr]) {
			if (!visited[to]) {
				q.push(to);

				dist[to] = dist[curr] + 1;
				visited[to] = true;
			}
		}
	}
}
```

---