> [!info] Objetivo
> - Tem como objetivo encontrar a fatoração prima de $n$. Ademais, também é possível adaptar o [[Sieve of Eratosthenes]] para atingir o mesmo objetivo.

> [!note]- Complexidade
> - $O(\sqrt n)$

```cpp
vector<int> get_prime_factor(int n) {
	vector<int> prime_factor;

	for (int i {2}; i * i <= n; ++i) {
	    while (n % i == 0) {
	        prime_factor.push_back(i);

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