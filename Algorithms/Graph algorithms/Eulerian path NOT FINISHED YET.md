> [!info] Objetivo
> - Um caminho euleriano é um caminho que passa por todas as arestas do grafo, já um ciclo euleriano é um caminho que passa por todas as arestas do grafo e volta para o mesmo vértice que começou.

> [!attention] Condições
> - Grafos bidirecionais:
> 	- Eulerian cycle: todos os vértices possuem um grau par.
> 	- Eulerian path: exatamente dois vértices possuem grau ímpar.
> - Grafos direcionados:
> 	- Eulerian cycle: todos os vértices possuem um grau de entrada e de saída par.
> 	- Eulerian path: no máximo um vértice possui $out\_degree - in\_degree = 1$ e no máximo um vértice possui $in\_degree - out\_degree = 1$ e todos os outros vértices possuem possuem grau de entrada igual ao grau de saída.
> - Independente de sobre qual grafo estamos falando é necessário que todos os vértices com um grau diferente de zero estejam na mesma componente.

> [!note]- Complexidade
> - $O(V + E)$

```cpp
typedef pair<int, int> pii;

int n, m;
// MAXN is the largest possible number of nodes
vector<pii> g[MAXN];
vector<int> path, stage(MAXN);
vector<bool> used;

void add_edge(int u, int v) {
	int idx {(int) used.size()};

    used.emplace_back();

	g[u].emplace_back(v, idx);
	g[v].emplace_back(u, idx);
}

void dfs(int u) {
    stack<int> s;

    s.push(u);

    while (!s.empty()) {
        int curr {s.top()};

        if (stage[curr] < (int) g[curr].size()) {
            auto [to, idx] = g[curr][stage[curr]];

            ++stage[curr];

            if (!used[idx]) {
                used[idx] = true;

                s.push(to);
            }
        } else {
            path.push_back(curr);

            s.pop();
        }
    }
}

bool eulerian_path(int s, bool is_cycle) {
	int odd_c {};

	for (int i {}; i < n; ++i) {
		if (g[i].size() % 2 != 0) {
			++odd_c;
		}
	}
    
	if ((is_cycle && odd_c != 0) || (!is_cycle && odd_c > 2)) {
		return false;
	}

	dfs(s);

	if ((int) path.size() != m + 1) {
		return false;
	}

	reverse(path.begin(), path.end());

	return true;
}
```

```cpp
```

---