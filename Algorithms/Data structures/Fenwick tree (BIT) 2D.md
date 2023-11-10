> [!info] Objetivo
> - A Fenwick tree (BIT) tem como objetivo implementar de maneira eficiente consultas de submatrizes que são prefixos, ela pode de maneira simples aceitar atualizações em índice e consultas em intervalo ou atualizações em intervalo e consulta em índice.

> [!note]- Complexidade
> - Build: $O(n \cdot m \cdot \log n \cdot \log m)$
> - Query/update: $O(\log n \cdot \log m)$
> - Range query/update: $O(\log n \cdot \log m)$

> [!hint] Outras operações
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

    int query(int idx, int idy) {
	    for (int x {idx}; x > 0; x -= x & -x) {
		    for (int y {idy}; y > 0; y -= y & -y) {
			    // Query logic	
		    }
	    }
    }

    int range_query(int ix, int iy, int ex, int ey) {
	    // Do the query for (xe, ye) and remove the excess if needed with the queries
	    // (ex, iy - 1), (ix - 1, ey) and then add (ix - 1, iy - 1) because it was removed two times
    }

    void update(int idx, int idy, int k) {
	    for (int x {idx}; x <= n; x += x & -x) {
		    for (int y {idy}; y <= m; y += y & -y) {
			    // Update logic
		    }
	    }
    }

    void range_update(int ix, int iy, int ex, int ey, int k) {
        // Do the update for (ix, iy) with k
        // After that undo the update for r + 1
    }

private:
    int n;
    int m;
    vector<vector<T>> bit;
};
```

```cpp
int n, m;
// MAXN is the largest possible number of rows
// MAXM is the largest possible number of columns
int BIT[MAXN][MAXM];

int query(int idx, int idy) {
	for (int x {idx}; x > 0; x -= x & -x) {
		for (int y {idy}; y > 0; y -= y & -y) {
			// Query logic	
		}
	}
}

int range_query(int ix, int iy, int ex, int ey) {
	// Do the query for (xe, ye) and remove the excess if needed with the queries
	// (ex, iy - 1), (ix - 1, ey) and then add (ix - 1, iy - 1)
}

void update(int idx, int idy, int k) {
	for (int x {idx}; x <= n; x += x & -x) {
		for (int y {idy}; y <= m; y += y & -y) {
			// Update logic
		}
	}
}
```

---