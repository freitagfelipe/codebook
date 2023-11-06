> [!info] Objetivo
> - Dado um número $n$, tem como objetivo calcular todos os divisores de $n$.

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
> - Dado um número $r$, tem como objetivo calcular os divisores de todos os números do intervalo $[1, r]$.

> [!note]- Complexidade
> - Build: $O(r \cdot \log r)$
> - Get divisors: $O(1)$

```cpp
vector<vector<int>> divisors;

void build(int r) {
	for (int i {1}; i <= r; ++i) {
		for (int j {i}; j <= r; j += i) {
			divisors[j].push_back(i);
		}
	}
}

// X must be in the interval [1, r]
vector<int> &get_divisors(int x) {
	return divisors[x];
}

void setup(int r) {
	divisors.assign(r + 1, vector<int>());
}
```

---