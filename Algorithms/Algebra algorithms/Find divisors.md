> [!info] Objetivo
> - Tem como objetivo calcular todos os divisores de $n$.

> [!note]- Complexidade
> - $O(\sqrt n)$

```cpp
vector<int> get_divisors(int n) {
	vector<int> divisors;

	for (int i {1}; i * i <= n; ++i) {
		if (n % i == 0) {
			divisors.push_back(i);

			if (n / i != i) {
				divisors.push_back(n / i);
			}
		}
	}

	return divisors;
}
```

---

> [!info] Objetivo
> - Tem como objetivo calcular os divisores de todos os números do intervalo $[1, r]$.

> [!note]- Complexidade
> - $O(r \cdot \log r)$

```cpp
void build(int r) {
	vector<vector<int>> divisors(r + 1);

	for (int i {1}; i <= r; ++i) {
		for (int j {i}; j <= r; j += i) {
			divisors[j].push_back(i);
		}
	}
}
```

---