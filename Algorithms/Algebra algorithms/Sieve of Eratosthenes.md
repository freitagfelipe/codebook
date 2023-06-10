> [!info] Objetivo
> - Calcular todos os números primos de um intervalo $[2, n]$. Uma versão em $O(n)$ que também calcula o menor fator primo pode ser encontrada em [[Linear sieve]].

> [!note]- Complexidade
> - Build: $O(n \log \log n)$
> - Query: $O(1)$

```cpp
// MAXN is the largest possible interval
int n;
bool prime[MAXN];

void build() {
	for (int i {2}; i <= n; ++i) {
		prime[i] = true;
	}

	prime[0] = prime[1] = false;

	for (int i {2}; i * i <= n; ++i) {
		if (prime[i]) {
			for (int j {i * i}; j <= n; j += i) {
				prime[j] = false;
			}
		}
	}
}

bool is_prime(int i) {
	return is_prime[i];
}
```

> [!hint] Adaptação
> - Podemos usar a adaptação abaixo do Crivo de Erastótenes para encontrar o menor fator primo de cada número de um intervalo $[2, n]$ com a mesma complexidade.

```cpp
// MAXN is the largest possible interval
int n;
int spf[MAXN];

void build() {
	for (int i {2}; i <= n; ++i) {
		spf[i] = i;
	}

	for (int i {2}; i * i <= n; ++i) {
		if (spf[i] == i) {
			for (int j {i * i}; j <= n; j += i) {
				spf[j] = min(spf[j], i);
			}
		}
	}
}

int get_spf(int i) {
	return spf[i];
}
```

---