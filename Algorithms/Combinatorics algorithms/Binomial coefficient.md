> [!info] Objetivo
> - Dado dois inteiros $n$ e $k$, tem como objetivo calcular o $\binom{n}{k}$.

> [!note]- Complexidade
> - $O(k)$

```cpp
ll binom(int n, int k) {
	ll res {1};
	
	for (int i {1}; i <= k; ++i) {
		res = (res * (n - k + i)) / i;
	}
	
	return res;
}
```

---

> [!info] Objetivo
> - Dado um inteiro $n$, tem como objetivo calcular até a n-ésima linhas do triângulo de pascal.

> [!note]- Complexidade
> - $O(n^2)$

```cpp
vector<vector<int>> build(int n) {
	vector<vector<int>> pascal_triangle(n + 1);
	
	pascal_triangle[0].push_back(1);

	for (int i {1}; i <= n; ++i) {
		pascal_triangle[i].push_back(1);

		for (int j {1}; j < i; ++j) {
			pascal_triangle[i].push_back(pascal_triangle[i - 1][j - 1] + pascal_triangle[i - 1][j]);
		}
		
		pascal_triangle[i].push_back(1);
	}

	return pascal_triangle;
}
```

---