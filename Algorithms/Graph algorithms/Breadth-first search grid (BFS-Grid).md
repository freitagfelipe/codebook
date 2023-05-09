```ad-note
title: Complexidade
collapse: true

- $O(nm)$
```

```cpp
typedef pair<int, int> pii;

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

void BFS(int ri, int rj) {
    queue<pii> q;

    q.push({ri, rj});

    while (!q.empty()) {
        auto [ci, cj] = q.front();

        q.pop();

        visited[ci][cj] = true;

        for (int i {}; i < 4; ++i) {
            int ni {ci + di[i]};
            int nj {cj + dj[i]};

            if (is_cell_valid(ni, nj)) {
                visited[ni][nj] = true;

                q.push({ni, nj});
            }
        }
    }
}
```

---
