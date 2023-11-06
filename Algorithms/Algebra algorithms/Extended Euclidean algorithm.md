> [!info] Objetivo
> - Dados dois números $a$ e $b$, tem como objetivo calcular a identidade de Bézout, ou seja, dois números $x$ e $y$ tal que $a \cdot x + b \cdot y = mdc(a, b)$.

> [!note]- Complexidade
> - $O(\log min(a, b))$ 

```cpp
int gcd_extended(int a, int b, int &x, int &y) {
    if (b == 0) {
        x = 1;
        y = 0;

        return a;
    }

    int x1, y1;

    int gcd {gcd_extended(b, a % b, x1, y1)};

    x = x1;
    y = x1 - y1 * (a / b);

    return gcd;
}
```

---