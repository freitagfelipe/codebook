> [!info] Objetivo
> - Dado um intervalo $[L, R]$, se $f(l) \cdot f(r) < 0$ encontrar a raíz de $f$ que está no intervalo.

> [!note]- Complexidade
> - $O(80 \cdot f(n))$

```cpp
double f(double x) {
	// calculates f(x)
}

bool has_same_sign(double x, double y) {
	if ((x > 0 && y > 0) || (x < 0 && y < 0)) {
		return true;
	}

	return false;
}

double bisection(double l, double r) {
	for (int i {}; i < 80; ++i) {
		double m {(l + r) / 2};
		double value {f(m)};

		if (value == 0) {
			return m;
		}

		if (has_same_sign(f(l), value)) {
			l = m;
		} else {
			r = m;
		}
	}

	return l;
}
```

---