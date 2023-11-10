> [!info] Objetivo
> - Tem como objetivo determinar quais números podem ou não ser formados por uma soma de alguns elementos de $v$.

> [!note]- Complexidade
> - $O(\dfrac{n \cdot k}{wordsize})$

```cpp
// MAXK is the max size of K
bitset<MAXK> dp;

void build(const vector<int> &v, int maxk) {
	dp[0] = true;

	for (int n : v) {
		dp |= (dp << n);
	}
}

bool query(int k) {
	return dp[k];
}
```

---
