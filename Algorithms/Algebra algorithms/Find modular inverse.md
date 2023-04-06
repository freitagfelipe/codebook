```ad-info
title: Objetivo

- O objetivo das duas implementações abaixo é encontrar o inverso modular de um número. Podemos usar o [[Extended Euclidean algorithm]] para encontrá-lo ou o [[Fast exponentiation]].
```

```ad-caution
title: Atenção

- Os algoritmos apresentados supõem que já foi verificado se o número possui inverso modular, ou seja, $mdc(a, m) = 1$.
- O algoritmo utilizando [[Fast exponentiation]] só funciona se $m$ for primo. Porém, nem todo $a \text{ mod } m$ é primo, só sera primo se $a \text{ mod } m < m$.
```

```cpp
int get_modular_inverse(int a, int m) {
	int modular_inverse, y;

	int gcd {gcd_extended(a, m, modular_inverse, y)};

	modular_inverse %= m;

	if (modular_inverse < 0) {
		inv += m;
	}

	return modular_inverse;
}
```

```cpp
int get_modular_inverse(int a, int m) {
	return fast_exponentiation(a, m - 2, m);
}
```

```ad-info
title: Objetivo

- O objetivo da implementação abaixo é encontrar o inverso modular de cada número em um intervalo $[1, m - 1]$.
```

```ad-attention
title: Atenção

- O algoritmo abaixo só funciona quando $m$ é primo, pois quando $m$ é primo todos os número de $[1, m - 1]$ são coprimos de $m$.
```

```ad-note
title: Complexidade
collapse: true

- Build: $O(m)$
- Query: $O(1)$
```

```cpp
int m;
int modular_inverse[MAXM];

void build() {
	modular_inverse[1] = 1;

	for (int i {2}; i < m; ++i) {
		inv[i] = (-m / i) * inv[m % i];
		inv[i] %= m;

		if (inv[i] < 0) {
			inv[i] += m;
		}
	}
}

int get_modular_inverse(int n) {
	return modular_inverse[n];
}
```

---