> [!info] Objetivo
> - O objetivo das duas implementações abaixo é encontrar o inverso modular de um número. Podemos usar o [[Extended Euclidean algorithm]] para encontrá-lo ou o [[Fast exponentiation]].

> [!caution] Atenção
> - O algoritmo apresentado supõe que já foi verificado se o número possui inverso modular, ou seja, $mdc(a, m) = 1$.

> [!note]- Complexidade
> - $O(\log a + \log b)$

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

---