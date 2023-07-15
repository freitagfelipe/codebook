> [!info] Objetivo
> - É uma estrutura de dados que suporta consultas sobre intervalos e atualizações em apenas um índice ou atualizações em um intervalo e perguntas sobre um índice. Caso as duas operações sejam para fazer em intervalos a [[Segment tree with lazy propagation]] é uma escolha melhor. A primeira implementação é para range query e point update, já a segunda é para point query e range update.

> [!note]- Complexidade
> - Build: $O(n \log n)$
> - Query/update: $O(\log n)$

```cpp
int n;
// MAXN is the largest possible number of elements
int BIT[MAXN];

int query(int idx) {
	for (; idx > 0; idx -= idx & -idx) {
		// Query logic
	}
}

int range_query(int l, int r) {
	// Do the query for r and remove the excess with the query for l - 1
}

void update(int idx, int k) {
	for (; idx <= n; idx += idx & -idx) {
		// Update logic
	}
}
```

```cpp
int n;
// MAXN is the largest possible number of elements
int BIT[MAXN];

void update(int idx, int k) {
	for (; idx <= n; idx += idx & -idx) {
		// Update logic
	}
}

void range_update(int l, int r, int k) {
	int undo {};

	update(l, k);
	update(r + 1, undo);
}

int point_query(int idx) {
	for (; idx > 0; idx -= idx & -idx) {
		// Query logic
	}
}
```

---