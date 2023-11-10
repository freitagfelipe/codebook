> [!info] Objetivo
> - Tem como objetivo fazer a travessia em um grafo utilizando busca em largura.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
// The graph must be 0-indexed
void bfs(int s, const vector<vector<int>> &g) {
	vector<bool> visited(g.size());
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
// The graph must be 0-indexed
vector<int> bfs(int s, const vector<vector<int>> &g) {
	// INF is a distance that can represent the node as unreachable
	vector<int> dists(g.size(), INF);
	vector<bool> visited(g.size());

	queue<int> q;

	q.push(s);

	dists[s] = 0;
	visited[s] = true;

	while (!q.empty()) {
		int curr {q.front()};

		q.pop();

		for (int to : g[curr]) {
			if (!visited[to]) {
				q.push(to);

				dists[to] = dists[curr] + 1;
				
				visited[to] = true;
			}
		}
	}

	return dists;
}
```

---