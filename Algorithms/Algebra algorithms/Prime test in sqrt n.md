> [!Info]
> O algoritmo tem como objetivo descobrir se um número é primo ou não.

> [!faq] Como funciona?
> Sabemos dizer se um número é primo checando se ele é divisível por todos os números de $[2..n - 1]$, mas é possível provar que um dos divisores de um número composto é menor ou igual a $\sqrt n$, para provar essa afirmação sabemos que podemos escrever $n = a \cdot b$ e queremos mostrar que $a \leq \sqrt n$ ou $b \leq \sqrt n$, irei utilizar prova por contradição, então tentaremos provar que $a > \sqrt n$ ou $b > \sqrt n$, então temos:
> $$
> \begin{gathered}
> \text{ } a > \sqrt n \\
> \text{ } b > \sqrt n \\
> \end{gathered}
> $$ 
> Multiplicando ambas as funções, temos:
> $$
> \begin{equation}
> \begin{split}
> a \cdot b &> \sqrt n \cdot \sqrt n\\
> n &> n \text{, substituindo } a \cdot b \text{ por n.} \\
> \end{split}
> \end{equation}
> $$
> Com isso chegamos a um absurdo e provamos que a sentença original está correta. Entretanto, calcular $\sqrt n$ não é barato compultacionalmente e por isso iremos utilizar $i \cdot i \leq n$, podemos fazer isso, pois:
> $$
> \begin{equation}
> \begin{split}
> i &\leq \sqrt n\\
> i^2 &\leq (\sqrt n)^2\\
> i^2 &\leq n
> \end{split}
> \end{equation}
> $$

> [!note]- Complexidade
> $O(\sqrt n)$, pois só precisamos fazer um laço até $\sqrt n$.

```cpp
bool is_prime(int n) {
	if (n == 1) {
		return false;
	}

    for (int i {2}; i * i <= n; ++i) {
        if (n % i == 0) {
            return false;
        }
    }

    return true;
}
```

---