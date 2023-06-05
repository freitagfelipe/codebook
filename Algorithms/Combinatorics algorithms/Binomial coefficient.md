> [!info] Objetivo
> - Calcular o coeficiente binomial, ou seja, $\binom{n}{k}$.

> [!caution] Atenção
> - $\binom{n}{k}, \forall k$ tal que $k \leq n$.
> - A segunda implementação só funciona se $m$ é primo e $m > n$.

> [!note]- Complexidade
> - Primeira implementação:
>	- Build: $O(n^2)$
>	- Query: $O(1)$
>- Segunda implementação:
>	- Build: $O(n)$
>	- Query: $O(1)$

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

```cpp
typedef long long ll;
typedef __int128_t vll;

// MAXN is the largest possible n
vll factorial[MAXN];
ll factorial_modular_inverse[MAXN];
ll modular_inverse[MAXN];

void build(int n, int m) {
	modular_inverse[0] = factorial[0] = factorial_modular_inverse[0] = 1;
	modular_inverse[1] = factorial[1] = factorial_modular_inverse[1] = 1;

	for (int i {2}; i <= n; ++i) {
		factorial[i] = (factorial[i - 1] * i) % m;

		modular_inverse[i] = (-m / i) * modular_inverse[m % i];
		modular_inverse[i] %= m;

		if (modular_inverse[i] < 0) {
			modular_inverse[i] += m;
		}

		factorial_modular_inverse[i] = (factorial_modular_inverse[i - 1] * modular_inverse[i]) % m;
	}
}

int query(int n, int k, int m) {
	return (factorial[n] * factorial_modular_inverse[k] * factorial_modular_inverse[n - k]) % m;
}
```

---