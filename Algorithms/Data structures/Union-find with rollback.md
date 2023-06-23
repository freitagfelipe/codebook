> [!info] Objetivo
> - Possui o mesmo objetivo do [[Union-find]], porém essa implementação permite com que seja possível desfazer operações de merge. Entretanto, para atingir esse feito é necessário remover a compressão de caminho da função find.

> [!note]- Complexidade
> - Build: $O(n)$
> - Find/merge: $O(\log n)$

```cpp
// MAXN is the largest possible number of elements
int p[MAXN];
int h[MAXN];
vector<tuple<int, int, int, int>> op;

int find(int x) {
    if (p[x] == x) {
        return x;
    }

    return find(p[x]);
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

	op.emplace_back(x, h[x], y, p[y]);

    p[y] = x;

    if (h[x] == h[y]) {
        ++h[x];
    }
}

void rollback(int t) {
	while ((int) op.size() > t) {
		auto [x, hx, y, py] = op.back();

		h[x] = hx;
		p[y] = py;

		op.pop_back();
	}	
}

int time() {
	return (int) op.size();
}
```

---