> [!info] Objetivo
> - O objetivo da implementação abaixo é encontrar todos os divisores de um número $n$.

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

> [!info] Objetivo
> - O objetivo da implementação abaixo é encontrar todos os divisores de todos os números em um intervalo $[1, n]$.

> [!note]- Complexidade
> - $O(n \log n)$

```cpp
// MAXN is the largest possible interval
vector<int> divisors[MAXN];

void build(int n) {
	for (int i {1}; i <= n; ++i) {
		for (int j {i}; j <= n; j += i) {
			divisors[j].push_back(i);
		}
	}
}

vector<int> get_divisors(int x) {
	return divisors[x];
}
```

---