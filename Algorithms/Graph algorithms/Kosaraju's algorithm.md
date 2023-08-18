> [!info] Objetivo
> - O algoritmo tem como objetivo encontrar as componentes fortemente conexas de um digrafo é possível também produzir o grafo condensado após o cálculo das componentes formente conexas. Ademais, o algoritmo utiliza ordenação topológica implementada com [[Depth-first search (DFS)]].

> [!info]- Complexidade
> - $O(V + E)$

```cpp
// MAXN is the largest possible number of nodes
int n;
vector<int> g[MAXN], gt[MAXN], ts, component(MAXN, -1);
bitset<MAXN> visited;

void ts_dfs(int u) {
	visited[u] = true;

    for (int to : g[u]) {
        if (!visited[to]) {
            ts_dfs(to);
        }
    }

    ts.push_back(u);
}

void component_dfs(int u, int c) {
    component[u] = c;

    for (int to : gt[u]) {
        if (component[to] == -1) {
            component_dfs(to, c);
        }
    }
}

int scc() {
	for (int i {}; i < n; ++i) {
		if (!visited[i]) {
			ts_dfs(i);
		}
	}

	reverse(ts.begin(), ts.end());

    int comp {};

    for (int v : ts) {
        if (component[v] == -1) {
            component_dfs(v, comp++);
        }
    }

	return comp;
}
```

> [!hint] Montando o grafo condensado
> - O código abaixo mostrará como montar o grafo condensado.

> [!note]- Complexidade
> - $O(n \log n)$

```cpp
// MAXN is the largest possible number of nodes
int n;
vector<int> g[MAXN], gt[MAXN], ts, component(MAXN, -1), same_comp[MAXN];
bitset<MAXN> visited;

void ts_dfs(int u) {
	visited[u] = true;

    for (int to : g[u]) {
        if (!visited[to]) {
            ts_dfs(to);
        }
    }

    ts.push_back(u);
}

void component_dfs(int u, int c) {
	component[u] = c;
    same_comp[c].push_back(u);

    for (int to : gt[u]) {
        if (component[to] == -1) {
            component_dfs(to, c);
        }
    }
}

vector<vector<int>> scc() {
	for (int i {}; i < n; ++i) {
		if (!visited[i]) {
			ts_dfs(i);
		}
	}

	reverse(ts.begin(), ts.end());

    int comp {};

    for (int v : ts) {
        if (component[v] == -1) {
            component_dfs(v, comp++);
        }
    }

	vector<vector<int>> cg(comp);

	for (int i {}; i < comp; ++i) {
		for (int u : same_comp[i]) {
			for (int to : g[u]) {
				if (component[u] != component[to]) {
					cg[i].push_back(component[to]);
				}
			}
		}
	}

	for (int i {}; i < comp; ++i) {
		sort(cg[i].begin(), cg[i].end());

		cg[i].erase(unique(cg[i].begin(), cg[i].end()), cg[i].end());
	}

	return cg;
}
```

---