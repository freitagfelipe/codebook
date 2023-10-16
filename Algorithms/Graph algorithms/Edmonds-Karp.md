> [!info] Objetivo
> - Dado um grafo e a capacidade de fluxo de cada aresta, tem como objetivo encontrar o fluxo máximo de $s$ para $t$.

> [!note]- Complexidade
> - $O(VE^2)$

```cpp
typedef long long ll;
typedef pair<int, ll> pil;

int n;
// MAXN is the largest possible number of nodes
vector<int> g[MAXN];
vector<vector<ll>> capacity;

ll bfs(int s, int t, vector<int>& p) {
    fill(p.begin(), p.end(), -1);

    p[s] = -2;

    queue<pil> q;

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

ll max_flow(int s, int t) {
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
```

---