> [!info] Objetivo
> - Tem como objetivo encontras as pontes de um grafo, ou seja, as arestas que se removidas fazem com que seja gerado uma nova componente conexa, ou seja, desconectam o grafo.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
typedef pair<int, int> Edge;

int timer;
vector<vector<int>> g;
vector<int> tin, low;
vector<Edge> bridges;
vector<bool> visited;

void dfs(int u, int p = -1) {
    visited[u] = true;

    tin[u] = low[u] = ++timer;

    for (int to : g[u]) {
        if (to == p) {
            continue;
        }

        if (visited[to]) {
            low[u] = min(low[u], tin[to]);
        } else {
            dfs(to, u);

            low[u] = min(low[u], low[to]);

            if (low[to] > tin[u]) {
                bridges.emplace_back(u, to);
            }
        }
    }
}

// The graph must be 0-indexed
void find_bridges(int n) {
	timer = 0;

	tin.assign(n, 0);
	low.assign(n, 0);
	visited.assign(n, false);

	for (int i {}; i < n; ++i) {
		if (!visited[i]) {
			dfs(i);
		}
	}
}
```

> [!hint] Bridge tree (2-Edge connected component)
> - É possível adaptar o algoritmo para calcular a bridge tree,  uma propriedade interessante é a seguinte:
> 	- dados dois vértices em uma 2-Edge connected component, existem pelo menos 2 caminhos disjuntos em arestas entre estes dois vértices.

```cpp
typedef pair<int, int> Edge;

int timer;
vector<vector<int>> g, same_comp;
vector<int> tin, low, comp;
vector<Edge> bridges;
vector<bool> visited;
stack<int> s;

void calculate_comp(int start) {
    same_comp.emplace_back();

    int uc {-1};

    do {
        uc = s.top();

        s.pop();

        comp[uc] = same_comp.size() - 1;

        same_comp.back().push_back(uc);
    } while (uc != start);
}

void dfs(int u, int p = -1) {
    visited[u] = true;

    tin[u] = low[u] = ++timer;

    s.push(u);

    for (int to : g[u]) {
        if (to == p) {
            continue;
        }

        if (visited[to]) {
            low[u] = min(low[u], tin[to]);
        } else {
            dfs(to, u);

            low[u] = min(low[u], low[to]);

            if (low[to] > tin[u]) {
                bridges.emplace_back(u, to);

                calculate_comp(to);
            }
        }
    }
}

vector<vector<int>> get_cg() {
    vector<vector<int>> cg(same_comp.size());

    for (int i {}; i < (int) same_comp.size(); ++i) {
		for (int u : same_comp[i]) {
			for (int to : g[u]) {
				if (comp[u] != comp[to]) {
					cg[i].push_back(comp[to]);
				}
			}
		}
	}

    for (vector<int> &v : cg) {
        sort(v.begin(), v.end());

        v.erase(unique(v.begin(), v.end()), v.end());
    }

    return cg;
}

// The graph must be 0-indexed
void find_bridges(int n) {
	timer = 0;

	tin.assign(n, 0);
	low.assign(n, 0);
	visited.assign(n, false);
    comp.assign(n, -1);

	for (int i {}; i < n; ++i) {
		if (!visited[i]) {
			dfs(i);

            calculate_comp(i);
		}
	}
}
```

---