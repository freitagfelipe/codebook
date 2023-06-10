> [!info] Objetivo
> - Contar quantos bits ligados o número $n$ possui.

> [!note]- Complexidade
> - $O(\log n)$

```cpp
int count_setted_bits(int n) {
    if (n == 0) {
        return 0;
    }

    return (n & 1) + count_setted_bits(n >> 1);
}
```

---