> [!info] Objetivo
> - Tem como objetivo calcular de maneira eficiente $b^e \text{ mod m}$.

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