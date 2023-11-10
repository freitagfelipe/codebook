> [!info] Objetivo
> - Tem como objetivo resolver o problema da mochila, no qual nos é dado $n$ itens e cada item tem seu valor e seu peso, e com isso temos que responder qual é o valor máximo que conseguimos ganhar carregando qualquer número de itens, desde que o peso total de tais itens não seja maior que $s$, o peso que a mochila aguenta carregar.

> [!note]- Complexidade
> - $O(ns)$

```cpp
int knapsack(int n, int s, const vector<int> &v, const vector<int> &w) {
	vector<vector<int>> DP(n + 1, vector<int>(s + 1));

    for (int i {1}; i <= n; ++i) {
        for (int j {1}; j <= s; ++j) {
            if (w[i - 1] > j) {
                DP[i][j] = DP[i - 1][j];
            } else {
                DP[i][j] = max(DP[i - 1][j], DP[i - 1][j - w[i - 1]] + v[i - 1]);
            }
        }
    }

    return DP[n][s];
}
```

> [!hint] Melhoria a complexidade da memória
> - Utilizando a adaptação abaixo ao invés do espaço auxiliar ser $O(ns)$ ele se tornará $O(s)$.

```cpp
int knapsack(int n, int s, const vector<int> &v, const vector<int> &w) {
	vector<int> DP(s + 1);
	
    for (int i {1}; i <= n; ++i) {
        auto [pi, wi] = make_pair(v[i - 1], w[i - 1]);

        for (int j {s}; j >= wi; --j) {
            DP[j] = max(DP[j], DP[j - wi] + pi);
        }
    }

    return DP[s];
}
```

---