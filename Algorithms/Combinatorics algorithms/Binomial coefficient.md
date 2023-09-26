> [!info] Objetivo
> - Calcular o coeficiente binomial, ou seja, $\binom{n}{k}$.

> [!caution] Atenção
> - $\binom{n}{k}, \forall k$ tal que $k \leq n$.

> [!note]- Complexidade
> - Build: $O(n^2)$
> - Query: $O(1)$

```cpp
// MAXN is the largest possible n
int pascal_triangle[MAXN][MAXN];

void build(int n, int m) {
	pascal_triangle[0][0] = 1;

	for (int i {1}; i <= n; ++i) {
		pascal_triangle[i][0] = pascal_triangle[i][i] = 1;

		for (int j {1}; j < i; ++j) {
			pascal_triangle[i][j] = pascal_triangle[i - 1][j - 1] + pascal_triangle[i - 1][j];
		}
	}
}

int query(int n, int k) {
	return pascal_triangle[n][k];
}
```

---