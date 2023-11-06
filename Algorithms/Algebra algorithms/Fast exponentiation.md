> [!info] Objetivo
> - Dado uma base $b$, um expoente $e$ e um módulo $m$, tem como objetivo calcular de maneira eficiente $b^e \text{ mod m}$.

> [!note]- Complexidade
> - $O(\log e)$

```cpp
int fast_exponentiation(int b, int e, int m) {
    if (e == 0) {
        return 1 % m; 
    }

    int answer {fast_exponentiation(b, e / 2, m)};

    answer = (answer * answer) % m;

    if (e % 2 == 0) {
        return answer;
    }

    return (answer * b) % m;
}
```

---