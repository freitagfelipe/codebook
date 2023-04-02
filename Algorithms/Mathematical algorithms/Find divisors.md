```ad-info
title: Objetivo

- O objetivo da implementação abaixo é encontrar todos os divisores de um número $n$.
```

```ad-note
title: Complexidade
collapse: true

- $O(\sqrt n)$
```

```cp
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

```ad-info
title: Objetivo

- O objetivo da implementação abaixo é encontrar todos os divisores de todos os números em um intervalo $[1, n]$.
```

```ad-note
title: Complexidade
collapse: true

- $O(n \log n)$
```

```cpp
vector<int> divisors[MAXN];

void build(int r) {
	for (int i {1}; i <= n; ++i) {
		for (int j {i}; j <= n; j += i) {
			divisors[j].push_back(i);
		}
	}
}
```

---