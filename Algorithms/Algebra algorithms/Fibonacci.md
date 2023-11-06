> [!info] Objetivo
> - Dado um número $n$, tem como objetivo calcular de maneira eficiente o n-ésimo número da sequência fibonacci.

> [!note]- Complexidade
> - $O(\log n)$

```cpp
typedef long long ll;

// Returns a pair that the first element is the Fn number and the second element is Fn+1 number
pair<ll, ll> fibonacci(ll n, ll m) {
    if (n == 0) {
        return {0, 1};
    }

    auto [f, s] {fibonacci(n >> 1, m)};

    ll c {(f * (2 * s - f + m)) % m};
    ll d {((f * f) % m + (s * s) % m) % m};

    if (n & 1) {
        return {d, (c + d) % m};
    }

    return {c, d};
}
```

---