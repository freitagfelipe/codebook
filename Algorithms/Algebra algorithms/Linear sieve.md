> [!info] Objetivo
> - Calcular todos os números primos, e seus menores fatores primos, de um intervalo $[2, n]$.

> [!note]- Complexidade
> - $O(n)$

```cpp
// MAXN is the largest possible interval
int n;
int lpf[MAXN];

vector<int> linear_sieve() {
	vector<int> pr;

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

	return pr;
}

int get_lpf(int n) {
	return lpf[n];
}
```

---