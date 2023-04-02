```ad-info
title: Objetivo

- Encontrar a fatoração prima de um número $n$. Você também pode adaptar o [[Sieve of Eratosthenes]] ou o [[Linear sieve]] para atingir o mesmo resultado.
```

```ad-note
title: Complexidade
collapse: true

- $O(\log n)$
```

```cpp
vector<int> get_prime_factor(int n) {
	vector<int> prime_factor;

	for (int i {2}; i * i <= n; ++i) {
		if (n % i != 0) {
			continue;
		}

		prime_factor.push_back(i);

		while (n % i == 0) {
			n /= i;
		}
	}

	if (n > 1) {
		prime_factor.push_back(n);
	}

	return prime_factor;
}
```

---