```ad-note
title: Complexidade
collapse: true

- $O(\sqrt{n})$
```

```cpp
bool is_prime(int n) {
    for (int i {2}; i * i <= p; ++i) {
        if (p % i == 0) {
            return false;
        }
    }

    return true;
}
```

```ad-hint
title: Responder todos os primos em uma sequência

- O algoritmo [[Sieve of Eratosthenes]] é capaz de calcular todos os primos em uma sequência e depois responder em tempo constante se um número da sequência é primo ou não.
```

---