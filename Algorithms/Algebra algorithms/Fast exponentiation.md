```ad-note
title: Complexidade
collapse: true

- $O(\log e)$
```

```cpp
int fast_exponentiation(int b, int e, int m) {
    if (e == 0) {
        return 1 % m; 
    }

    long long int answer {fast_exponentiation(b, e / 2, m)};

    answer = (answer * answer) % m;

    if (e % 2 == 0) {
        return answer;
    }

    return (answer * b) % m;
}
```

```ad-attention
title: Limites grandes

- Caso os limites dos número das entradas $a, b, m$ sejam muito grandes se torna necessário utilizar o algoritmo de [[Fast multiplication]]. Entretudo, isso aumentará a complexidade do algoritmo para $O(\log e + \log x)$.
```

```cpp
typedef long long ll;

ll fast_exponentiation(ll b, ll e, ll m) {
    if (e == 0) {
        return 1 % m; 
    }

    ll answer {fast_exponentiation(b, e / 2, m)};

    answer = fast_multiplication(answer, answer, m);

    if (e % 2 == 0) {
        return answer;
    }

    return fast_multiplication(answer, b, m);
}
```

---