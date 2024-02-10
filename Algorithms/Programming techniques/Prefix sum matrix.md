> [!info] Objetivo
> - A técnica PSM tem como objetivo calcular a soma de todas as submatrizes que são prefixos de $m$. Caso seja necessário realizar atualizações alguma estrutura de dados deve se utilizada como, por exemplo, a [[Fenwick tree (BIT) 2D]].

> [!note]- Complexidade
> - Build: $O(n^2)$
> - Query: $O(1)$

```cpp
vector<vector<int>> psm;

void build(const vector<vector<int>> &mat) {
	psm.assign(mat.size() + 1, vector<int>(mat[0].size() + 1));

	for (int i {1}; i <= n; ++i) {
        for (int j {1}; j <= n; ++j) {
            PSM[i][j] = PSM[i - 1][j] + PSM[i][j - 1] - PSM[i - 1][j - 1] + mat[i - 1][j - 1];
        }
    }
}

// 1-indexed
int query(int x, int y) {
	return psm[x][y];
}

// 1-indexed
int range_query(int xi, int yi, int xe, int ye) {
	return query(xe, ye) - query(xi - 1, ye) - query(xe, yi - 1) + query(xi - 1, yi - 1);
}
```

---