> [!info] Objetivo
> - Tem como objetivo encontrar para todos os vértices $v$ de um grafo o menor caminho de $v$ para todos os outros vértices do grafo.

> [!note]- Complexidade
> - $O(n^3)$

```cpp
typedef pair<int, int, int> Edge;

// The graph must be 0-indexed
vector<vector<int>> floyd_warshall(int n, const vector<Edge> &edges) {
	// INF is a distance that can represent the node as unreachable
	vector<vector<int>> dp(n, vector<int>(n, INF));

	for (int i {}; i < n; ++i) {
		dp[i][i] = 0;
	}

	for (auto [u, v, w] : edges) {
		dp[u][v] = w;
	}

    for (int k {}; k < n; ++k) {
        for (int i {}; i < n; ++i) {
            for (int j {}; j < n; ++j) {
	            if (dp[i][k] < INF && dp[k][j] < INF) {
		            dp[i][j] = min(dp[i][j], dp[i][k] + dp[k][j]);
	            }
            }
        }
    }

	return dp;
}
```

---