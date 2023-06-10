> [!info]
> - Dado uma sequência de inteiros não negativos e um valor $K$, determine se existe algum subconjunto de números que somem $K$.

> [!note]- Complexidade
> - $O(\dfrac{n \cdot k}{wordsize})$

```cpp
// MAXK is the max size of K
bitset<MAXK> bits;

void build(const vector<int> &v) {
	bits[0] = true;

	for (int n : v) {
		bits |= (bits << n);
	}
}

bool subset_sum(int k) {
	return bits[k];
}
```

---
