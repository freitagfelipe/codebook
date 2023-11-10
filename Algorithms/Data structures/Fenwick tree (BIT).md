> [!info] Objetivo
> - A Fenwick tree (BIT) tem como objetivo implementar de maneira eficiente consultas de prefixo, ela pode de maneira simples aceitar atualizações em índice e consultas em intervalo ou atualizações em intervalo e consulta em índice. Entretanto, caso as duas operações sejam em intervalo a [[Segment tree with lazy propagation]] deve ser utilizada.

> [!note]- Complexidade
> - Build: $O(n \log n)$
> - Query/update: $O(\log n)$
> - Range query/update: $O(\log n)$

> [!hint] Outras operações
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

    T query(int idx) {
        T ans {};

        for (; idx > 0; idx -= idx & -idx) {
            // Query logic
        }

        return ans;
    }

    T range_query(int l, int r) {
        // Do the query for r and remove the excess with the query for l - 1
    }

    void update(int idx, int x) {
        for (; idx <= n; idx -= idx & -idx) {
            // Update logic
        }
    }

    void range_update(int l, int r, int x) {
	    // Do the update for l with x
        // After that undo the update for r + 1
    }

private:
    int n;
    vector<T> bit;
};
```

---