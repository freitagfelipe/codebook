> [!info] Objetivo
> - É uma estrutura de dados que suporta consultas sobre intervalos e atualizações em apenas um índice ou atualizações em um intervalo e perguntas sobre um índice. A primeira implementação é para range query e point update, já a segunda é para point query e range update.

> [!note]- Complexidade
> - Build: $O(n \cdot m \cdot \log n \cdot \log m)$
> - Query/update: $O(\log n \cdot \log m)$

```cpp
int n, m;
// MAXN is the largest possible number of rows
// MAXM is the largest possible number of columns
int BIT[MAXN][MAXM];

int query(int x, int y) {
	for (; x > 0; x -= x & -x) {
		for (; y > 0; y -= y & -y) {
			// Query logic	
		}
	}
}

int range_query(int xi, int yi, int xe, int ye) {
	// Do the query for xe, ye and remove the excess with the query for xi - 1, yi - 1
}

void update(int x, int y, int k) {
	for (; x <= n; x += x & -x) {
		for (; y <= m; y += y & -y) {
			// Update logic
		}
	}
}
```

```cpp
int n, m;
// MAXN is the largest possible number of rows
// MAXM is the largest possible number of columns
int BIT[MAXN][MAXM];

void update(int x, int y, int k) {
	for (; x <= n; x += x & -x) {
		for (; y <= m; y += y & -y) {
			// Update logic
		}
	}
}

void range_update(int xi, int yi, int xe, int ye, int k) {
	int undo {};

	update(xi, yi, k);
	update(xe + 1, ye + 1, undo);
}

int point_query(int x, int y) {
	for (; x > 0; x -= x & -x) {
		for (; y > 0; y -= y & -y) {
			// Query logic
		}
	}
}
```

---