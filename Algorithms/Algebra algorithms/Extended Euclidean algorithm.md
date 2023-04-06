```ad-info
title: Objetivo

- Dados dois números $a, b$ calcular a identidade de Bézout, ou seja, dois números $x, y$ tais que $a \cdot x + b \cdot y = mdc(a, b)$.
```

```ad-note
title: Complexidade
collapse: true

- Complexidade: $O(\log a + \log b)$
```

```cpp
int gcd_extended(int a, int b, int &x, int &y) {
    if (a == 0) {
        x = 0;
        y = 1;

        return b;
    }

    int x1, y1;

    int gcd {gcd_extended(b % a, a, x1, y1)};

    x = y1 - (b / a) * x1;
    y = x1;

    return gcd;
}
```

```ad-hint
title: Resolver equações diofantinas lineares com duas variáveis

- Utilizando o algoritmo de Euclides extendido podemos também resolver equações diofantinas lineares com duas variáveis. Esse tipo de equação tem o seguinte formato: $a \cdot x + b \cdot y = c$ onde $x, y \in \mathbb{Z}$. Supondo que exista uma solução para a equação todas as outras soluções são derivadas dela e seguem o seguinte formato:

$$
\begin{gathered}
(x + k \cdot \dfrac{b}{gcd(a, b)}, y - k \cdot \dfrac{a}{gcd(a, b)})
\end{gathered}
$$
```

```cpp
bool linear_diophantine_solver(int a, int b, int c, int &x, int &y) {
    if (a == 0 && b == 0) {
        if (c == 0) {
            x = y = 0;

            return true;
        }

        return false;
    }

    int gcd {gcd_extended(abs(a), abs(b), x, y)};

    if (a < 0) {
        x = -x; 
    }

    if (b < 0) {
        y = -y;
    }

    if (c % gcd != 0) {
        return false;
    }

    int t {c / gcd};

    x *= t;
    y *= t;

    return true;
}
```

---