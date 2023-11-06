> [!info] Objetivo
> - Dado um número $r$, tem como objetivo calcular todos os números primos do intervalo $[2, r]$

> [!note]- Complexidade
> - Build: $O(n \log \log n)$
> - Query: $O(1)$

```cpp
vector<bool> build(int r) {
	vector<bool> is_prime(r + 1, true);

	is_prime[0] = is_prime[1] = false;

	for (int i {2}; i * i <= r; ++i) {
		if (is_prime[i]) {
			for (int j {i * i}; j <= r; j += i) {
				is_prime[j] = false;
			}
		}
	}

	return is_prime;
}
```

> [!hint] Adaptação
> - O Crivo de Erastótenes pode ser adaptado para encontrar o menor fator primo de cada número no intervalo $[1, r]$ com a mesma complexidade.

```cpp
vector<int> build(int r) {
	vector<int> spf(r + 1);
	
	for (int i {2}; i <= r; ++i) {
		spf[i] = i;
	}

	for (int i {2}; i * i <= r; ++i) {
		if (spf[i] == i) {
			for (int j {i * i}; j <= r; j += i) {
				spf[j] = min(spf[j], i);
			}
		}
	}

	return spf;
}
```

---