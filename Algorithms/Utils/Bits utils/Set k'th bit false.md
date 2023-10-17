> [!info] Objetivo
> - Tornar false um bit na posição $k$.

> [!note]- Complexidade
> - $O(1)$

```cpp
void set_bit_off(int &x, int k) {
    x &= ~(1 << k);
}
```

---