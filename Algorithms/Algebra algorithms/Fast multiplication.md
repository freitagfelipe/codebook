> [!info] Objetivo
> - Tem como objetivo calcular de maneira rápida $(x \cdot y) \text{ mod m}$.

> [!note]- Complexidade
> - $O(\log x)$

```cpp
typedef long long ll;

ll fast_multiplication(ll x, ll y, ll m) {
    if (x == 0) {
        return 0;
    }

    ll answer {fast_multiplication(x / 2, y, m)};

    answer = (2 * answer) % m;

    if (x % 2 == 0) {
        return answer;
    }

    return (answer + y) % m;
}
```

---