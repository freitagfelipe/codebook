> [!info] Objetivo
> - Retorna o bit menos significativo, ou seja, o bit mais a direita de $x$.

> [!note]- Complexidade
> - $O(1)$

```cpp
int lsb(int x) {
	return x & -x;
}
```

---