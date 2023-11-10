> [!info] Objetivo
> -  A técnica de PSA tem como objetivo calcular a soma de todos os prefixos de $v$. Caso seja necessário realizar atualizações alguma estrutura de dados deve se utilizada como, por exemplo, a [[Fenwick tree (BIT)]].

> [!note]- Complexidade
> - Build: $O(n)$
> - Query: $O(1)$

> [!hint] Outras operações
> - A técnica também pode ser alterada para outras operações, mas para utilizar a função de consulta de intervalo deve ser possível desfazer essa operação como, por exemplo, operações de xor. Contudo, operações que não possuem tal propriedade ainda podem ser utilizadas, desde que todas as consultas tenham $l = 1$, um exemplo de operação assim é a de $max$.

```cpp
vector<int> psa;

void build(const vector<int> &v) {
	psa.assign(v.size() + 1, 0);

	for (int i {}; i < (int) v.size(); ++i) {
		psa[i + 1] = psa[i] + v[i];
	}
}

// 1-indexed
int query(int idx) {
	return psa[idx];
}

// 1-indexed
int range_query(int l, int r) {
	return query(r) - query(l - 1);
}
```

---