```ad-info
title: Objetivo

- Dados dois números $a, b$ encontrar o máximo divisor comum (mdc).
```

```ad-note
title: Complexidade
collapse: true

- $O(\log a + \log b)$ 
```

```cpp
int gcd(int a, int b) {
    if (a == 0) {
       return b; 
    }

    return gcd(b % a, a);
}
```

```ad-hint
title: Encontrar o mmc

- Utilizando a propriedade que envolve o máximo divisor comum (mdc) e o mínimo múltiplo comum (mmc) que é: $mmc(a, b) \cdot mdc(a, b) = a \cdot b$, ou seja, podemos concluir que $mmc(a, b) = \dfrac{a \cdot b}{mdc(a, b)}$. O código está logo abaixo.
```

```cpp
int lcm(int a, int b) {
    return a * b / gdc(a, b);
}
```

---