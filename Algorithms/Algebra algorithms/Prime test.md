> [!Info] Objetivo
> Dado um número $n$, tem como objetivo responser se $n$ é ou não primo.

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