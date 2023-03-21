```ad-note
title: Complexidade
collapse: true

- $O(\log n)$
```

```cpp
int v[MAXN];

bool binary_search(int x, int n) {
    int start {0}, end {n - 1};

    while (start <= end) {
        int mid {(start + end) / 2};

        if (v[mid] == x) {
            return true;
        } else if (v[mid] > x) {
            end = mid - 1;
        } else {
            start = mid + 1;
        }
    }

    return false;
}
```

---