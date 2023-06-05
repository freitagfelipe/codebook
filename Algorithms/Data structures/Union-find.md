> [!info] Objetivo
> - Gerenciar uma coleção de conjuntos disjuntos, onde cada conjunto contém elementos distintos. Ele fornece operações eficientes para realizar união (join/merge) de conjuntos e encontrar (find) a representação de um elemento dentro de um conjunto.

> [!note]- Complexidade
> - $O(\alpha(n))$

```cpp
// MAXN is the largest possible number of elements
int p[MAXN];
int weight[MAXN];

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

    if (weight[x] == weight[y]) {
        p[x] = y;

        ++weight[y];
    } else if (weight[x] > weight[y]) {
        p[y] = x;
    } else {
        p[x] = y;
    }
}
```

---