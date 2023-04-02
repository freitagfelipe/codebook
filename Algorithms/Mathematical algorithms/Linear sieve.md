```ad-info
title: Objetivo

- Calcular todos os números primos, e seus menores fatores primos, de um intervalo $[2, n]$.
```

```ad-note
title: Complexidade
collapse: true

- 
```

```cpp
int n;
int lpf[MAXN];
vector<int> pr;

void linear_sieve() {
	for (int i {2}; i <= n; ++i) {
		if (lpf[i] == 0) {
			lpf[i] = i;
			pr.push_back(i);
		}

		for (int j {}; i * pr[j] <= n; ++j) {
			lpf[i * pr[j]] = pr[j];

			if (pr[j] == lpf[i]) {
				break;
			}
		}
	}
}
```

---