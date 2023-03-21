```ad-note
title: Complexidade
collapse: true

- $O(\alpha(n)) \approx O(1)$
```

```cpp
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