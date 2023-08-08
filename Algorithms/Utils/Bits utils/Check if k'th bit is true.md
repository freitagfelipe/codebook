> [!note] Objetivo
> - Checar se o bit na posição $k$ está ativo.

> [!note]- Complexidade
> - $O(1)$

```cpp
bool is_setted(int x, int k) {
    return (x & (1 << k)) != 0;
}
```

---