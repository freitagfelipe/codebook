> [!Info] Objetivo
> O algoritmo tem como objetivo descobrir se um número é primo ou não.

> [!note]- Complexidade
> - $O(\sqrt n)$

```cpp
bool is_prime(int n) {
	if (n == 1) {
		return false;
	}

    for (int i {2}; i * i <= n; ++i) {
        if (n % i == 0) {
            return false;
        }
    }

    return true;
}
```

---