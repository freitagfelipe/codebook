> [!info] Objetivo
> - Tem como objetivo fazer a travessia em uma matriz utilizando o mesmo princípio da [[Breadth-first search (BFS)]].

> [!note]- Complexidade
> - $O(nm)$

```cpp
typedef pair<int, int> pii;

int di[] = {1, 0, -1, 0};
int dj[] = {0, 1, 0, -1};
vector<vector<int>> mat;
vector<vector<bool>> visited;

// Add more conditions based on the problem if needed
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
void bfs(int ri, int rj) {
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

// Call it before call the bfs
void setup(int n, int m) {
	visited.assign(n, vector<bool>(m));
}
```

---
