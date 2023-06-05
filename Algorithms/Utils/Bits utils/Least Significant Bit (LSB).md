> [!note] Objetivo
> - Retorna o bit menos significativo, ou seja, o bit mais a direita de $x$.

```cpp
int lsb(int x) {
	return x & -x;
}
```

---