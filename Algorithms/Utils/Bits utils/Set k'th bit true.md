> [!info] Objetivo
> - Tornar true um bit na posição $k$.

> [!note]- Complexidade
> - $O(1)$

```cpp
void set_bit_true(int &x, int k) {
	x |= (1 << k);
}
```

---