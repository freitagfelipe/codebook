```ad-note
title: Complexidade
collapse: true

- $O(nm)$
```

```cpp
int l, c;
int di[] = {1, 0, -1, 0};
int dj[] = {0, 1, 0, -1};
int board[MAXN][MAXN];
bool visited[MAXN][MAXN];

bool is_cell_valid(int i, int j) {
    if (i < 0 || i >= l || j < 0 || j >= c) {
        return false;
    } else if (visited[i][j]) {
        return false;
    }

    return true;
}

void DFS(int i, int j) {
    visited[i][j] = true;

    for (int k {}; k < 4; ++k) {
        int ni {i + di[k]};
        int nj {j + dj[k]};

        if (is_cell_valid(ni, nj)) {
            DFS(ni, nj);
        }
    }
}
```

---
