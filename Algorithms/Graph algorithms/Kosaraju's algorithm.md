> [!info] Objetivo
> - O algoritmo tem como objetivo encontrar as componentes fortemente conexas de um digrafo é possível também produzir o grafo condensado após o cálculo das componentes formente conexas. Ademais, o algoritmo utiliza ordenação topológica implementada com [[Depth-first search (DFS)]].

> [!info]- Complexidade
> - $O(V + E)$

```cpp
// MAXN is the largest possible number of nodes
int n;
vector<int> g[MAXN], gt[MAXN], ts, component(MAXN, -1);
bitset<MAXN> visited;

void ts_dfs(int v) {
	visited[v] = true;

    for (int u : g[v]) {
        if (!visited[u]) {
            ts_dfs(u);
        }
    }

    ts.push_back(v);
}

void component_dfs(int v, int c) {
    component[v] = c;

    for (int u : gt[v]) {
        if (component[u] == -1) {
            component_dfs(u, c);
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

```cpp
// MAXN is the largest possible number of nodes
int n;
vector<int> g[MAXN], gt[MAXN], ts, component(MAXN, -1), same_comp[MAXN];
bitset<MAXN> visited;

void ts_dfs(int v) {
	visited[v] = true;

    for (int u : g[v]) {
        if (!visited[u]) {
            ts_dfs(u);
        }
    }

    ts.push_back(v);
}

void component_dfs(int v, int c) {
	component[v] = c;
    same_comp[c].push_back(v);

    for (int u : gt[v]) {
        if (component[u] == -1) {
            component_dfs(u, c);
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
		for (int v : same_comp[i]) {
			for (int neigh : g[v]) {
				if (component[v] != component[neigh]) {
					cg[i].push_back(component[neigh]);
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