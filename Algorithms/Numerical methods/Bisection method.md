```ad-info
title: Objetivo

- Dado um intervalo $[L, R]$, se $f(l) \cdot f(r) < 0$ encontrar a raíz de $f$ que está no intervalo.
```

```ad-note
title: Complexidade
collapse: true

- A complexidade do algoritmo é dada pela complexidade da função $f(x)$.
```

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
	for (int i {1}; i <= 80; ++i) {
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