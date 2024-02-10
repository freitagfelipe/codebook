> [!info] Objetivo
> - A Fenwick tree (BIT) tem como objetivo implementar de maneira eficiente consultas de prefixo, ela pode de maneira simples aceitar atualizações em índice e consultas em intervalo ou atualizações em intervalo e consulta em índice. Entretanto, caso as duas operações sejam em intervalo a [[Segment tree with lazy propagation]] deve ser utilizada. 

> [!note]- Complexidade
> - Build: $O(n \log n)$
> - Query/update: $O(\log n)$
> - Range query/update: $O(\log n)$

> [!hint] Outras operações além da soma
> - Essa estrutura aceita várias operações, mas para utilizar a função de consulta de intervalo deve ser possível desfazer essa operação como, por exemplo, operações de xor. Contudo, operações que não possuem tal propriedade ainda podem ser utilizadas, desde que todas as consultas tenham $l = 1$, um exemplo de operação assim é a de $max$.

```cpp
template <typename T>
class BIT {
public:
    BIT(int n) {
        this->n = n;
        this->bit.assign(n + 1, (T) 0);
    }

    BIT(int n, const vector<T> &v) {
        this->n = n;
        this->bit.assign(n + 1, (T) 0);

        for (int i {}; i < n; ++i) {
            this->update(i + 1, v[i]);
        }
    }

	// 1-indexed
    T query(int idx) {
        T ans {};

        for (; idx > 0; idx -= idx & -idx) {
	        // Query logic
        }

        return ans;
    }
    
	// 1-indexed
    T range_query(int l, int r) {
	    // Do a query for r and remove the excess
	    // with a query for l - 1
    }

	// 1-indexed
    void update(int idx, T x) {
        for (; idx <= n; idx += idx & -idx) {
	        // Update logic
        }
    }

	// 1-indexed
    void range_update(int l, int r, T x) {
	    // Do an update for l and
	    // undo the update for r + 1
    }

private:
    int n;
    vector<T> bit;
};
```

---