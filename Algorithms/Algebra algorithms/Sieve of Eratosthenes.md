```ad-info
title: Objetivo

- Calcular todos os números primos de um intervalo $[2, n]$. Uma versão em $O(n)$ que também calcula o menor fator primo pode ser encontrada em [[Linear sieve]].
```

```ad-note
title: Complexidade
collapse: true

- Build: $O(n \log \log n)$
- Query: $O(1)$
```

```cpp
int n;
bool is_prime[MAXN];

void build() {
	for (int i {2}; i <= n; ++i) {
		is_prime[i] = true;
	}

	is_prime[0] = is_prime[1] = false;

	for (int i {2}; i * i <= n; ++i) {
		if (is_prime[i]) {
			for (int j {i * i}; j <= n; j += i) {
				is_prime[j] = false;
			}
		}
	}
}

bool prime(int i) {
	return is_prime[i];
}
```

```ad-hint
title: Adaptação

- Podemos usar a adaptação abaixo do Crivo de Erastótenes para encontrar o menor fator primo de cada número de um intervalo $[2, n]$ com a mesma complexidade.
```

```cpp
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