```ad-info
title: Objetivo

- Dado um intervalo $[L, R]$, se $f(l) \cdot f(r) < 0$ encontrar a raíz de $f$ que está no intervalo.
```

```ad-note
title: Complexidade
collapse: true

- $O(80n)$
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

`````ad-example
title: Encontrar a raíz quadrada de um número $n$.

- Dado um número $n < 10^6$ encontre $x$ tal que $x = \sqrt n$. Essa raíz com certeza estará no intervalo $[0, 1000]$.

```cpp
#include <bits/stdc++.h>

using namespace std;

double n;

double f(double x) {
	return x * x - n;
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

int main() {
	cin >> n;

	cout << bisection(0, 1000) << '\n';

	return 0;
}
```
`````

---