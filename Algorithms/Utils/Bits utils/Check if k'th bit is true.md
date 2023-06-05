> [!note] Objetivo
> - Checar se o bit na posição $k$ está ativo.

```cpp
bool is_setted(int x, int k) {
    return (x & (1 << k)) != 0;
}
```

---