> [!info] Objetivo
> - O objetivo da técnica Digit DP é otimizar o processamento de problemas que envolvem dígitos em números grandes, permitindo resolver tais problemas de forma eficiente através do armazenamento de estados intermediários. Abaixo está um exemplo para somar todos os dígitos de todos os números no intervalo $[L, R]$.

> [!note]- Complexidade
> - $O(MAXN * MAXSUM)$

```cpp
typedef long long ll;

// MAXN is the max number of digits
// MAXSUM is the max sum possible of the digits
ll DP[MAXN][MAXSUM][2][2];

// Remember that lower and upper must have the same number of digits
// If they are different you need to put 0s in lower's left
ll solver(int idx, ll sum, bool can_low, bool can_high, const string &lower, const string &upper) {
	if (idx == (int) upper.size()) {
		return sum;
	}

	if (DP[idx][sum][can_low][can_high] != -1) {
		return DP[idx][sum][can_low][can_high];
	}

    int lw {can_low ? 0 : lower[idx] - '0'};
	int up {can_high ? 9 : upper[idx] - '0'};

	ll ans {};

	for (int d {lw}; d <= up; ++d) {
		ans += solver(idx + 1, sum + d, can_low | (d > lw), can_high | (d < up), lower, upper);
	}

	return DP[idx][sum][can_low][can_high] = ans;
}
```

---
