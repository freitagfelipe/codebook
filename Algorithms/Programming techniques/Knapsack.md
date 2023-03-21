```ad-note
title: Complexidade
collapse: true

- $O(nm)$
```

```cpp
int v[MAXN];
int w[MAXN];
int DP[MAXN][MAXW];

int knapsack() {
    int n, s;

    cin >> n >> s;

    for (int i {1}; i <= n; ++i) {
        cin >> v[i] >> w[i];
    }

    for (int i {1}; i <= n; ++i) {
        for (int j {1}; j <= s; ++j) {
            if (w[i] > j) {
                DP[i][j] = DP[i - 1][j];
            } else {
                DP[i][j] = max(DP[i - 1][j], DP[i - 1][j - w[i]] + v[i]);
            }
        }
    }

    return DP[n][s];
}
```

```ad-hint
title: Adaptação

- Utilizando a adaptação abaixo ao invés do espaço auxiliar ser $O(NS)$ ele se torna $O(S)$.
```

```cpp
int v[MAXN];
int w[MAXN];
int DP[MAXW];

int knapsack() {
    int n, s;

    cin >> n >> s;

    for (int i {1}; i <= n; ++i) {
        cin >> v[i] >> w[i];
    }

    for (int i {1}; i <= n; ++i) {
        for (int j {s}; j >= 0; --j) {
            if (w[i] <= j) {
                DP[j] = max(DP[j], DP[j - w[i]] + v[i]);
            }
        }
    }

    return DP[s];
}
```

---