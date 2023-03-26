```ad-info
title: Objetivo

- Dado uma sequência de inteiros não negativos e um valor $K$, determine se existe alguma sequência de números que 
```

```ad-note
title: Complexidade
collapse: true

- $O(\frac{n * k}{wordsize})$
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
