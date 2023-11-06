> [!info] Objetivo
> - Dado um número $n$, tem como objetivo contar quantos divisores um número $n$ tem, para isso podemos utilizar a seguinte fórmula, considere a fatoração prima de $n$:  $p_1^{\alpha_1} \cdot p_2^{\alpha_2} \cdot \ldots \cdot p_n^{\alpha_n}$. Com ela, temos a seguinte função para saber a quantidade de divisores $d(n) = (\alpha_1 + 1) \cdot (\alpha_2 + 1) \cdot \ldots \cdot (\alpha_n + 1)$. O código abaixo é uma adaptação do [[Prime factor]].

> [!note]- Complexidade
> - $O(\log n)$

```cpp
int get_divisors_count(int n) {
	int ans {1};
	
    for (int i {2}; i * i <= n; ++i) {
        int exp {};
        
        while (n % i == 0) {
            ++exp;
            
            n /= i;
        }
        
        ans *= (exp + 1);
    }
    
    if (n > 1) {
        ans *= 2;
    }
    
    return ans;
}
```

---