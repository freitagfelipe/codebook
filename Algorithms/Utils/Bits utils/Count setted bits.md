> [!info] Objetivo
> - Contar quantos bits ligados o número $n$ possui usando [[Least Significant Bit (LSB)]].

> [!note]- Complexidade
> - $O(\log n)$

```cpp
int count_setted_bits(int n) {
	int ans {};

	while (n != 0) {
		++ans;

		n -= n & -n;
	}

    return ans;
}
```

---