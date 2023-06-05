> [!info] Objetivo
> - Fazer a travessia em um grafo.

> [!hint] Adaptação
> - Pode ser utilizado para saber o grau de distância dos vértices em relação ao nó inicial.

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

---