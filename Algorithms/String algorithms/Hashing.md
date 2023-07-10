> [!info] Objetivo
> - Quando queremos comparar duas strings $a$ e $b$ obtemos uma complexidade de $min(|a|, |b|)$, porém se transformarmos essas strings em números através de um hashing podemos comparar esses números em $O(1)$. O algoritmo utiliza a seguinte fórmula chamada de polynomial rolling hash function:
>  
> $$
> \begin{gathered}
> hash(s) = \sum_{i = 0}^{n - 1} s[i] \cdot p^i \text{ mod } m
> \end{gathered}
> $$ 

> [!attention] Atenção
> - É bom que $p$ seja um número primo maior ou igual ao número de letras do alfabeto da questão. Se o alfabeto contém apenas letras minúsculas, ou seja, letras de [a..z], $p = 31$ é uma boa escolha. Porém, se o alfabeto contém tanto letras minúsculas quanto maiúsculas, ou seja, letras de [a..z] e [A..Z], $p = 53$ é uma boa escolha.
> - É bom que $m$ seja um número grande primo já que a probabilidade de termos uma colisão é de aproximadamente $\dfrac{1}{m}$,  geralmente $m = 1e9 + 9$ ou $m = 1e9 + 7$ são boas escolhas. 
> - Para diminuir a probabilidade de colisão é possível fazer um pair com dois hashes feitos com módulos diferentes

> [!note]- Complexidade
> - $O(n)$

```cpp
typedef unsigned long long ull;

int get_id(char ch) {
	return ch - 'a' + 1;
}

ull compute_hash(const string &s) {
	const int p {31};
	const int m {(int) 1e9 + 9};
	ull hash_value {};
	ull p_pow {1};

	for (char ch : s) {
		hash_value = (hash_value + get_id(ch) * p_pow) % m;
		p_pow = (p_pow * p) % m;
	}

	return hash_value;
}
```

---