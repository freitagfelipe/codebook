> [!info] Objetivo
> - Fazer a travessia em uma matriz utilizando o mesmo princípio da [[Depth-first search (DFS)]].

> [!note]- Complexidade
> - $O(nm)$

```cpp
int di[] = {1, 0, -1, 0};
int dj[] = {0, 1, 0, -1};
vector<vector<int>> mat;
vector<vector<bool>> visited;

bool is_cell_valid(int i, int j) {
	int l {(int) mat.size()};
	int c {(int) mat[0].size()};

    if (i < 0 || i >= l || j < 0 || j >= c) {
        return false;
    } else if (visited[i][j]) {
        return false;
    }

    return true;
}

// The graph must be 0-indexed
void dfs(int i, int j) {
    visited[i][j] = true;

    for (int k {}; k < 4; ++k) {
        int ni {i + di[k]};
        int nj {j + dj[k]};

        if (is_cell_valid(ni, nj)) {
            dfs(ni, nj);
        }
    }
}

// Call it before call the dfs
void setup(int n, int m) {
	visited.assign(n, vector<bool>(m));
}
```

---
