> [!info] Objetivo
> - Tem como objetivo encontrar o fluxo máximo de $s$ para $t$.

> [!note]- Complexidade
> - $O(VE^2)$

```cpp
typedef long long ll;

vector<vector<int>> g;
vector<vector<ll>> capacity;

void add_edge(int u, int v, int c) {
	g[u].push_back(v);
	g[v].push_back(u);

	capacity[u][v] += c;
	capacity[v][u] += 0;
}

ll bfs(int s, int t, vector<int> &p) {
    fill(p.begin(), p.end(), -1);

    p[s] = -2;

    queue<pair<int, ll>> q;

	// INF is the numeric limits max of the capacity type
    q.push({s, INF});

    while (!q.empty()) {
        auto [curr, flow] {q.front()};
        
        q.pop();

        for (int to : g[curr]) {
            if (p[to] == -1 && capacity[curr][to]) {
                p[to] = curr;

                ll new_flow {min(flow, capacity[curr][to])};

                if (to == t) {
                    return new_flow;
                }

                q.push({to, new_flow});
            }
        }
    }

    return 0;
}

// The graph must be 0-indexed
ll max_flow(int s, int t, int n) {
    ll flow {};
    ll new_flow {};
    vector<int> p(n);

    while ((new_flow = bfs(s, t, p))) {
        flow += new_flow;

        int curr {t};

        while (curr != s) {
            int prev {p[curr]};

            capacity[prev][curr] -= new_flow;
            capacity[curr][prev] += new_flow;

            curr = prev;
        }
    }

    return flow;
}

void setup(int n) {
	capacity.assign(n, vector<ll>(n));
}
```

---