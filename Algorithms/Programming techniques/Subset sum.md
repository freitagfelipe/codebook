```ad-info
title: Objetivo

- Dado uma sequência de inteiros não negativos e um valor $k$, determine se existe algum subconjunto de números que somem $k$.
```

```ad-note
title: Complexidade
collapse: true

- $O(\dfrac{nk}{wordsize})$
```

```cpp
bool subset_sum(int k) {
    bitset<MAXN> bits;

    bits[0] = 1;

    for (int i {}; i < n; ++i) {
        bits |= (bits << v[i]);
    }

    return bits[k];
}
```

---
