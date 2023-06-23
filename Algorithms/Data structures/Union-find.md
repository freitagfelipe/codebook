> [!info] Objetivo
> - Gerenciar uma coleção de conjuntos disjuntos, onde cada conjunto contém elementos distintos. Ele fornece operações eficientes para realizar união de conjuntos e encontrar a representação de um elemento dentro de um conjunto.

> [!note]- Complexidade
> - Build: $O(n)$
> - Find/merge: $O(\alpha(n))$

```cpp
// MAXN is the largest possible number of elements
int p[MAXN];
int h[MAXN];

int find(int x) {
    if (p[x] == x) {
        return x;
    }

    return p[x] = find(p[x]);
}

void join(int x, int y) {
    x = find(x);
    y = find(y);

    if (x == y) {
        return;
    }

    if (h[x] < h[y]) {
        swap(x, y);
    }

    p[y] = x;

    if (h[x] == h[y]) {
        ++h[x];
    }
}

void build(int n) {
	for (int i {}; i < n; ++i) {
		p[i] = i;
	}
}
```

---