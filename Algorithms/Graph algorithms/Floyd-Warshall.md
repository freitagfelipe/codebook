> [!info] Objetivo
> - Encontrar o menor caminho de todos os nós para todos os nós.

> [!note]- Complexidade
> - $O(n^3)$

```cpp
// MAXN is the largest possible number of nodes
int dp[MAXN][MAXN];
int n, m;

void floyd_warshall() {
    cin >> n >> m;

    for (int i {}; i < n; ++i) {
        for (int j {}; j < n; ++j) {
            if (i == j) {
                dp[i][j] = 0;
            } else {
				// INF is a distance that can represent the node as unreachable
                dp[i][j] = INF;
            }
        }
    }

    for (int i {}; i < m; ++i) {
        int x, y, w;

        cin >> x >> y >> w;

        dp[x][y] = w;
        dp[y][x] = w;
    }

    for (int k {}; k < n; ++k) {
        for (int i {}; i < n; ++i) {
            for (int j {}; j < n; ++j) {
                if (dp[i][k] + dp[k][j] < dp[i][j]) {
                    dp[i][j] = dp[i][k] + dp[k][j];
                }
            }
        }
    }
}
```

---