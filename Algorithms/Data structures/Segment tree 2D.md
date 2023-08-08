> [!info] Objetivo
> - Fazer de maneira eficiente $Q$ operações que podem consistir em perguntar algo sobre uma submatriz da matriz ou fazer um point update em um índice qualquer da matriz. Essas perguntas na submatriz podem, por exemplo, estar relacionada a um dos seguintes temas: mínimo, máximo, etc. A parte da estrutura que muda junto com a necessidade da questão é a classe Node.

> [!note]- Complexidade
> - Build: $O(nm)$
> - Query/update: $O(\log n \cdot \log m)$

```cpp
#define L(x) (x << 1)
#define R(x) (L(x) | 1)

// T is the type that the Node will store
// U is the type that the array will store
template <typename T, typename U>
class SegmentTree2D {
public:
	// Pass the matrix with &mat[0][0]
    void build(int n, int m, U *mat) {
        this->n = n;
        this->m = m;

		this->mat.assign(n + 1, vector<U>(m + 1));
		this->tree.assign(n * 4, vector<Node>(4 * m));

        this->build_x(mat, 1, 1, n);
    }

	// x and y has to be on the interval [1..N]
    void update(int x, int y, U v) {
        this->update_x(1, 1, this->n, x, y, v);
    }

	// Accept queries on the interval [1..N] in both dimensions
    T query(int ix, int ex, int iy, int ey) {
	    // Return the property in the node that is the answer
    }

private:
    struct Node {
		// Node variables

		Node() = default;

        Node operator+(const Node &o) const {
            // Node merge logic
        }
    };

    int n;
    int m;
    vector<vector<U>> mat;
    vector<vector<Node>> tree;

	// lx and ly has to be on the interval [1..N]
	// Because of that we need to do lx - 1, ly - 1
	// To match the interval of mat that goes from [0..N - 1] in both dimensions
    void build_y(U *mat, int nodex, int lx, int rx, int nodey, int ly, int ry) {
        if (ly == ry && lx == rx) {
	        // Build tree and mat logic

            return;
        }

        if (ly == ry) {
            this->tree[nodex][nodey] = this->tree[L(nodex)][nodey] + this->tree[R(nodex)][nodey];

            return;
        }

        int mid {(ly + ry) / 2};

        this->build_y(mat, nodex, lx, rx, L(nodey), ly, mid);
        this->build_y(mat, nodex, lx, rx, R(nodey), mid + 1, ry);

        this->tree[nodex][nodey] = this->tree[nodex][L(nodey)] + this->tree[nodex][R(nodey)];
    }

    void build_x(U *mat, int node, int l, int r) {
        if (l == r) {
            this->build_y(mat, node, l, r, 1, 1, this->m);

            return;
        }

        int mid {(l + r) / 2};

        this->build_x(mat, L(node), l, mid);
        this->build_x(mat, R(node), mid + 1, r);

        this->build_y(mat, node, l, r, 1, 1, this->m);
    }

    void update_y(int nodex, int lx, int rx, int nodey, int ly, int ry, int target_y, U v) {
        if (ly == ry && lx == rx) {
            // Update tree and mat logic

            return;
        }

        if (ly == ry) {
            this->tree[nodex][nodey] = this->tree[L(nodex)][nodey] + this->tree[R(nodex)][nodey];

            return;
        }

        int mid {(ly + ry) / 2};

        if (target_y <= mid) {
            this->update_y(nodex, lx, rx, L(nodey), ly, mid, target_y, v);
        } else {
            this->update_y(nodex, lx, rx, R(nodey), mid + 1, ry, target_y, v);
        }

        this->tree[nodex][nodey] = this->tree[nodex][L(nodey)] + this->tree[nodex][R(nodey)];
    }

    void update_x(int node, int l, int r, int target_x, int target_y, U v) {
        if (l == r) {
            this->update_y(node, l, r, 1, 1, this->m, target_y, v);

            return;
        }

        int mid {(l + r) / 2};

        if (target_x <= mid) {
            this->update_x(L(node), l, mid, target_x, target_y, v);
        } else {
            this->update_x(R(node), mid + 1, r, target_x, target_y, v);
        }

        this->update_y(node, l, r, 1, 1, this->m, target_y, v);
    }

    Node query_y(int nodex, int nodey, int l, int r, int l_target, int r_target) {
        if (l == l_target && r == r_target) {
            return this->tree[nodex][nodey];
        }

        int mid {(l + r) / 2};

        if (r_target <= mid) {
            return this->query_y(nodex, L(nodey), l, mid, l_target, r_target);
        }
        
        if (l_target > mid) {
            return this->query_y(nodex, R(nodey), mid + 1, r, l_target, r_target);
        }

        return this->query_y(nodex, L(nodey), l, mid, l_target, mid) + this->query_y(nodex, R(nodey), mid + 1, r, mid + 1, r_target);
    }

    Node query_x(int node, int l, int r, int target_ix, int target_ex, int target_iy, int target_ey) {
        if (l == target_ix && r == target_ex) {
            return this->query_y(node, 1, 1, this->m, target_iy, target_ey);
        }

        int mid {(l + r) / 2};

        if (target_ex <= mid) {
            return this->query_x(L(node), l, mid, target_ix, target_ex, target_iy, target_ey);
        }
        
        if (target_ix > mid) {
            return this->query_x(R(node), mid + 1, r, target_ix, target_ex, target_iy, target_ey);
        }

        return this->query_x(L(node), l, mid, target_ix, mid, target_iy, target_ey) + this->query_x(R(node), mid + 1, r, mid + 1, target_ex, target_iy, target_ey);
    }
};
```

---