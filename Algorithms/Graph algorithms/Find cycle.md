> [!info] Objetivo
> - Tem como objetivo encontrar ciclos em um grafo, a primeira implementação será para grafos bidirecionais e a segunda para grafos direcionados.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
vector<vector<int>> g;
vector<int> parent;
vector<bool> visited;
int cycle_start, cycle_end;

bool dfs(int u, int p = -1) {
	visited[u] = true;

	for (int to : g[u]) {
		if (to == p) {
			continue;
		}

		if (visited[to]) {
			cycle_end = u;
			cycle_start = to;

			return true;
		}

		parent[to] = u;

		if (dfs(to, parent[to])) {
			return true;
		}
	}

	return false;
}

// The graph must be 0-indexed
vector<int> find_cycle(int n) {
	cycle_start = -1;

	parent.assign(n, -1);
	visited.assign(n, false);

	for (int i {}; i < n; ++i) {
		if (!visited[i] && dfs(i)) {
			break;
		}
	}

	if (cycle_start == -1) {
		return {};
	}

	vector<int> cycle;

	cycle.push_back(cycle_start);

	for (int v {cycle_end}; v != cycle_start; v = parent[v]) {
		cycle.push_back(v);
	}

	cycle.push_back(cycle_start);

	return cycle;
}
```

```cpp
vector<vector<int>> g;
vector<int> parent, color;
int cycle_start, cycle_end;

bool dfs(int u) {
	color[u] = 1;

	for (int to : g[u]) {
		if (color[to] == 0) {
			parent[to] = u;

			if (dfs(to)) {
				return true;
			}
		} else if (color[to] == 1) {
			cycle_end = u;
			cycle_start = to;

			return true;
		}
	}

	color[u] = 2;

	return false;
}

// The graph must be 0-indexed
vector<int> find_cycle(int n) {
	cycle_start = -1;

	parent.assign(n, -1);
	color.assign(n, 0);

	for (int i {}; i < n; ++i) {
		if (color[i] == 0 && dfs(i)) {
			break;
		}
	}

	if (cycle_start == -1) {
		return {};
	}

	vector<int> cycle;

	cycle.push_back(cycle_start);

	for (int v {cycle_end}; v != cycle_start; v = parent[v]) {
		cycle.push_back(v);
	}

	cycle.push_back(cycle_start);

	reverse(cycle.begin(), cycle.end());

	return cycle;
}
```

---