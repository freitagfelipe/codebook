> [!info] Objetivo
> - Tem como objetico encontrar o máximo divisor comum de $a$ e $b$.

> [!note]- Complexidade
> - $O(\log min(a, b))$ 

```cpp
int gcd(int a, int b) {
    if (b == 0) {
       return a; 
    }

    return gcd(b, a % b);
}
```

> [!hint] Encontrar o mmc
> - Utilizando a propriedade que envolve o máximo divisor comum (mdc) e o mínimo múltiplo comum (mmc) que é: $mmc(a, b) \cdot mdc(a, b) = a \cdot b$, podemos concluir que $mmc(a, b) = \dfrac{a \cdot b}{mdc(a, b)}$. Com isso, conseguimos computar o $mmc(a, b)$ com a mesma complexidade do $mdc(a, b)$.

```cpp
int lcm(int a, int b) {
    return a * b / gdc(a, b);
}
```

---