> [!note] Objetivo
> - Tornar false um bit na posição $k$.

```cpp
void set_bit_off(int &x, int k) {
    x &= ~(1 << k);
}
```

---