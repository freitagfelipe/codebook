> [!info] Objetivo
> - A Fenwick tree (BIT) tem como objetivo implementar de maneira eficiente consultas de submatrizes que são prefixos, ela pode de maneira simples aceitar atualizações em índice e consultas em intervalo ou atualizações em intervalo e consulta em índice.

> [!note]- Complexidade
> - Build: $O(n \cdot m \cdot \log n \cdot \log m)$
> - Query/update: $O(\log n \cdot \log m)$
> - Range query/update: $O(\log n \cdot \log m)$

> [!hint] Outras operações além da soma
> - Essa estrutura aceita várias operações, mas para utilizar a função de consulta de intervalo deve ser possível desfazer essa operação como, por exemplo, operações de xor. Contudo, operações que não possuem tal propriedade ainda podem ser utilizadas, desde que todas as consultas tenham $l = 1$, um exemplo de operação assim é a de $max$.

```cpp
template <typename T>
class BIT2D {
public:
    BIT2D(int n) {
        this->n = n;
        this->bit.assign(n + 1, (T) 0);
    }

    BIT2D(int n, int m, const vector<vector<T>> &mat) {
        this->n = n;
        this->m = m;
        this->bit.assign(n + 1, vector<T>(m + 1));

        for (int i {}; i < n; ++i) {
            for (int j {}; j < m; ++j) {
                this->update(i + 1, j + 1, mat[i][j]);
            }
        }
    }

    T query(int idx, int idy) {
		T ans {};

	    for (int x {idx}; x > 0; x -= x & -x) {
		    for (int y {idy}; y > 0; y -= y & -y) {
			    // Query logic
		    }
	    }

		return ans;
    }

    T range_query(int ix, int iy, int ex, int ey) {
	    // Do a query for (xe, ye) and remove the excess
	    // with queries for (ex, iy - 1) and (ix - 1, ey)
	    // after that you need to add the part that you
	    // removed two times i.e (ix - 1, iy - 1)
    }

    void update(int idx, int idy, T k) {
	    for (int x {idx}; x <= n; x += x & -x) {
		    for (int y {idy}; y <= m; y += y & -y) {
			    // Update logic
		    }
	    }
    }

    void range_update(int ix, int iy, int ex, int ey, T k) {
	    // Do an update for (ix, iy) and
	    // undo the update for (ex + 1, ey + 1)
    }

private:
    int n;
    int m;
    vector<vector<T>> bit;
};
```

---