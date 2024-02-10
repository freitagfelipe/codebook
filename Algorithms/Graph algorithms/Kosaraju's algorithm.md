> [!info] Objetivo
> - Tem como objetivo encontrar as componentes fortemente conexas de um digrafo também é possível produzir o grafo condensado após o cálculo das componentes formente conexas. Ademais, o algoritmo utiliza ordenação topológica implementada com [[Depth-first search (DFS)]].

> [!note]- Complexidade
> - $O(V + E)$

```cpp
// tg is the transpose graph
vector<vector<int>> g, tg;
vector<int> ts, component;
vector<bool> visited;

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

    for (int to : tg[u]) {
        if (component[to] == -1) {
            component_dfs(to, c);
        }
    }
}

// The graph must be 0-indexed
int scc(int n) {
	component.assign(n, -1);
	visited.assign(n, false);

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

	ts.clear();

	return comp;
}
```

> [!hint] Montando o grafo condensado
> - O código abaixo mostrará como montar o grafo condensado com a mesma complexidade, porém com alguns processos a mais.

```cpp
// tg is the transpose graph
vector<vector<int>> g, tg, same_comp;
vector<int> ts, component;
vector<bool> visited;

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

    for (int to : tg[u]) {
        if (component[to] == -1) {
            component_dfs(to, c);
        }
    }
}

// The graph must be 0-indexed
vector<vector<int>> scc(int n) {
	component.assign(n, -1);
	visited.assign(n, false);

	for (int i {}; i < n; ++i) {
		if (!visited[i]) {
			ts_dfs(i);
		}
	}

	reverse(ts.begin(), ts.end());

    int comp {};

    for (int v : ts) {
        if (component[v] == -1) {
			same_comp.emplace_back();
			
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

	for (vector<int> &v : cg) {
        sort(v.begin(), v.end());

        v.erase(unique(v.begin(), v.end()), v.end());
    }

	ts.clear();

	return cg;
}
```

---