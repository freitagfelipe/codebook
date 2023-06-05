> [!note] Objetivo
> - Verificar se $x$ é uma potência de dois.

```cpp
bool is_power_of_two(int x) {
	return (x & (x - 1)) == 0;
}
```

---