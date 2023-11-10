> [!info] Objetivo
> - Tem como objetivo encontrar o inverso modular de $a$, ou seja, encontrar um número $x$, tal que $a \cdot x \equiv 1 \text{ mod m}$. O algoritmo utiliza o [[Extended Euclidean algorithm]] durante o cálculo.

> [!note]- Complexidade
> - $O(\log min(a, b))$ 

```cpp
// It will return -1 if the modular inverse don't exists
int get_modular_inverse(int a, int m) {
	int modular_inverse, y;

	int gcd {gcd_extended(a, m, modular_inverse, y)};

	if (gcd != 1) {
		return -1;
	}

	modular_inverse = (modular_inverse % m + m) % m;

	return modular_inverse;
}
```

---