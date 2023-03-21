```ad-note
title: Complexidade
collapse: true

- $O(n^3)$
```

```cpp
int dp[MAXN][MAXN];
int n, m;

void floyd_warshall() {
    cin >> n >> m;

    for (int i {}; i < n; ++i) {
        for (int j {}; j < n; ++j) {
            if (i == j) {
                dp[i][j] = 0;
            } else {
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