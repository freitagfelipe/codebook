> [!info] Objetivo
> - Resolver o problema da mochila, no qual nos é dado $n$ itens e cada item tem seu peso e valor, dito isso o objetivo é encontrar qual é o valor máximo que conseguimos ganhar carregando qualquer número de itens.

> [!note]- Complexidade
> - $O(ns)$

```cpp
// MAXN is the largest possible number of items
// MAXW is the highest possible backpack weight
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

> [!hint] Melhoria no uso de memória
> - Utilizando a adaptação abaixo ao invés do espaço auxiliar ser $O(ns)$ ele se tornará $O(s)$.

```cpp
// MAXN is the largest possible number of items
// MAXW is the highest possible backpack weight
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